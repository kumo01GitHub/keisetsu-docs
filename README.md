# keisetsu Docs

[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/kumo01GitHub/keisetsu-docs/pulls)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

keisetsu 全体の設計意図と運用方針を横断して整理するドキュメントハブです。

この `keisetsu-docs` は、各実装リポジトリ（publisher / database / mobile）をまたいだ
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
  - 制作（publisher）・配布（database）・利用（mobile）を分離し、更新しやすく再利用しやすい形で運用する
  - 公開スキーマでデータ構造を揃え、公開 catalog で配布経路を明示し、オフライン対応アプリで学習できる構成にする

## リポジトリの関係

```text
[keisetsu-publisher]
  kdb + deck manifest を生成
            |
            v
[keisetsu-database]
  schema + catalog + kdb + deck manifest を公開
            |
            v
[keisetsu-mobile]
  catalog 取得 -> kdb 取得 -> 学習/テスト

[keisetsu-docs]
  コンセプト・運用・手順を横断管理
```

## リポジトリ

- [keisetsu-publisher](https://github.com/kumo01GitHub/keisetsu-publisher)
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

1. `keisetsu-publisher` でカードを作成・編集し、`.kdb` と deck manifest を生成する
2. `keisetsu-database` に `.kdb` と manifest を配置する
3. `keisetsu-database` で `npm run build` を実行し、`catalog/catalog.json` を再生成する
4. `keisetsu-database` で `npm run validate` を実行し、形式と整合性を検証する
5. `keisetsu-database` で push または tag を作成して配布する
6. `keisetsu-mobile` で catalog 経由の deck 取得と学習動作を確認する

## 配布モデル

- 公開URLは GitHub Raw 形式を利用
- deck 一覧は `catalog/catalog.json` を起点に各 deck manifest を参照する
- 利用側は catalog から deck manifest を辿り、deck manifest から `.kdb` を取得する
- 実データは `databases/*.kdb`

```text
https://raw.githubusercontent.com/{owner}/{repo}/{ref}/catalog/catalog.json
https://raw.githubusercontent.com/{owner}/{repo}/{ref}/catalog/decks/{deck-id}.json

deck manifest の path を使って .kdb を取得
例: https://raw.githubusercontent.com/{owner}/{repo}/{ref}/databases/starter-basic.kdb
```

## 利用者向けガイド

### keisetsu モバイルアプリの使い方

1. スマートフォンでExpo Go アプリをインストールしてください。
    - [Expo Go (iOS)](https://apps.apple.com/app/expo-go/id982107779)
    - [Expo Go (Android)](https://play.google.com/store/apps/details?id=host.exp.exponent)
2. Expo Go アプリを開き、下記のいずれかの方法で keisetsu アプリを起動してください。

**公開URL**

[https://u.expo.dev/e7aad213-54f2-490d-8cc3-7e06ea89c3d9](https://u.expo.dev/e7aad213-54f2-490d-8cc3-7e06ea89c3d9)

**QRコード**

![Expo QR](assets/keisetsu-expo-qr.png)

これで keisetsu アプリをすぐに利用開始できます。

### keisetsu 単語帳編集Webアプリの使い方

1. [keisetsu-publisher 公開ページ](https://keisetsu-publisher.vercel.app) にアクセス
2. 新規 deck を作成、または CSV / 既存 kdb を取り込む
3. カードや deck 情報（ID、タイトル、言語など）を編集
4. 「kdbのみ」「deck manifestのみ」「同梱ZIP」いずれかをダウンロード
5. 生成物を keisetsu-database に配置して、[追加・編集申請](https://github.com/kumo01GitHub/keisetsu-database/pulls)
    - `.kdb` -> `keisetsu-database/databases/`
    - `{deck-id}.json` -> `keisetsu-database/catalog/decks/`

### 対応言語

- English (`en`)
- 日本語 (`ja`)

## ドキュメント運用メモ

- 初回リリースまでは、設計見直しに伴う破壊的変更が繰り返し入る前提で運用する
- 初回リリース前の仕様・データ形式・UI は安定版ではないため、互換性を保証しない
- スキーマ変更時は mobile/publisher/database の README を同時更新する
- 初回リリース後は、互換性に影響する変更について配布タグと更新履歴を明記する
- **注意: Expo Go での配布は本来推奨されていません。** Expo Go は学習・検証用途向けであり、[公式FAQ](https://docs.expo.dev/faq/#what-can-i-do-or-cannot-do-with-expo-go) でも本番配布には development build の利用が推奨されています。

## 今後のTODO

- 開発者向け、単語帳製作者向け、利用者向けに分けたドキュメントを整備する
- README を多言語対応し、日本語・英語など複数言語で閲覧できるようにする
