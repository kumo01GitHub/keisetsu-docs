# keisetsu Docs

[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/kumo01GitHub/keisetsu-docs/pulls)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

keisetsu 全体の設計意図と運用方針を横断して整理するドキュメントハブです。

この `keisetsu-docs` は、各実装リポジトリ（admin / database / mobile）をまたいだ
仕様の前提、運用ルール、更新手順を一元管理するための場所です。

- どのリポジトリが何を責務として持つかを明確にする
- 配布フローと検証フローを、実装から独立して文書化する
- 仕様変更時に参照すべき共通の判断軸を維持する

## コンセプト

keisetsu は、学習データの保管方法や配布経路を公開し、利用者が自分で教材を保持して使える OSS 単語帳です。

- 目標
  - 誰もがスマートフォン一つで学べる環境をつくること
- 必要性
  - データの非公開化、オンライン依存、更新経路の不透明さといった既存課題を解消する
- 優位性
  - 仕様・データ・配布フローをすべて公開し、透明性を担保している
  - OSS であり、誰もが無料でデータを更新・利用できる
- 実現方針
  - 公開スキーマでデータ構造を揃え、公開 catalog で配布経路を明示し、オフライン対応アプリで学習できる構成にする
  - 制作（admin）・配布（database）・利用（mobile）を分離し、更新しやすく再利用しやすい形で運用する

## 実装・運用の設計原則

- Open by Default
  - データ仕様と配布構造を公開し、ブラックボックス化しない
- Local First
  - 端末内で完結できる体験を優先し、学習継続性を守る
- Contract Driven
  - スキーマ契約と manifest 契約で、実装間の前提を明文化する
- Small, Composable Repos
  - 責務分離で開発速度と保守性を両立する
- Validate Before Release
  - 配布前に形式検証・整合性検証を必ず通す

## リポジトリの関係

```text
[keisetsu-admin]
  deck編集 / kdb生成 / manifest生成
            |
            v
[keisetsu-database]
  schema + databases + catalog を公開
            |
            v
[keisetsu-mobile]
  catalog取得 -> kdb取得 -> 学習/テスト

[keisetsu-docs]
  コンセプト・運用・手順を横断管理
```

## リポジトリ説明とリンク

- [keisetsu-admin](https://github.com/kumo01GitHub/keisetsu-admin)
  - Next.js ベースの deck 編集UI
  - CSV取り込み、kdb取り込み、kdb再出力
  - deck manifest（JSON）と zip バンドル出力

- [keisetsu-database](https://github.com/kumo01GitHub/keisetsu-database)
  - 配布対象 `databases/*.kdb` の保管
  - スキーマ契約 `schema.sql`
  - 配布インデックス `catalog/catalog.json`
  - catalog更新・形式検証・整合性検証スクリプト

- [keisetsu-mobile](https://github.com/kumo01GitHub/keisetsu-mobile)
  - Expo + React Native の学習アプリ
  - GitHub catalog から deck 一覧を取得
  - kdbダウンロード / ローカル取り込み
  - 学習モードとテストモード

## 標準ワークフロー

1. `keisetsu-admin` でカードを作成・編集し、`.kdb` と deck manifest を生成する
2. `keisetsu-database` に `.kdb` と manifest を配置する
3. `keisetsu-database` で `npm run build` を実行し、`catalog/catalog.json` を再生成する
4. `keisetsu-database` で `npm run validate` を実行し、形式と整合性を検証する
5. GitHub に push または tag を作成して配布する
6. `keisetsu-mobile` で catalog 経由の deck 取得と学習動作を確認する

## 配布モデル

- 公開URLは GitHub Raw 形式を利用
- deck 一覧は `catalog/catalog.json` を起点に各 deck の manifest を参照する
- 利用側は catalog から manifest を辿り、manifest から `.kdb` を取得する
- 実データは `databases/*.kdb`

```text
https://raw.githubusercontent.com/{owner}/{repo}/{ref}/catalog/catalog.json
https://raw.githubusercontent.com/{owner}/{repo}/{ref}/catalog/decks/{deck-id}.json
manifest の path を使って .kdb を取得
例: https://raw.githubusercontent.com/{owner}/{repo}/{ref}/databases/starter-basic.kdb
```

## 利用者向けガイド

### keisetsu モバイルアプリの使い方

- [Expo Go (iOS/Android)](https://expo.dev/client) をインストール
- Expo Go で [URL](https://u.expo.dev/e7aad213-54f2-490d-8cc3-7e06ea89c3d9) を開くとすぐ使えます
- deck 一覧の取得・ダウンロード・学習・テストが可能
- 詳細は [keisetsu-mobile](https://github.com/kumo01GitHub/keisetsu-mobile#アプリの使い方) を参照

### keisetsu 管理画面の使い方

- [keisetsu-admin 公開ページ](https://keisetsu-admin.vercel.app) から、Webブラウザ上で deck の新規作成・編集・CSV/kdb 取り込み・エクスポートが可能です。
- 詳細は [keisetsu-admin](https://github.com/kumo01GitHub/keisetsu-admin#利用方法) を参照してください。

## ドキュメント運用メモ

- 初回リリースまでは、設計見直しに伴う破壊的変更が繰り返し入る前提で運用する
- 初回リリース前の仕様・データ形式・UI は安定版ではないため、互換性を保証しない
- スキーマ変更時は mobile/admin/database の README を同時更新する
- 初回リリース後は、互換性に影響する変更について配布タグと更新履歴を明記する
- **注意: Expo Go での配布は本来推奨されていません。** Expo Go は学習・検証用途向けであり、[公式FAQ](https://docs.expo.dev/faq/#what-can-i-do-or-cannot-do-with-expo-go) でも本番配布には development build の利用が推奨されています。

## 今後のTODO

- 開発者向け、単語帳製作者向け、利用者向けに分けたドキュメントを整備する
- 開発者向けドキュメントを英語にする
- README を多言語対応し、日本語・英語など複数言語で閲覧できるようにする
- PR テンプレートと Issue テンプレートを追加し、変更提案と不具合報告の粒度を揃える
