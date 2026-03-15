# keisetsu Docs

keisetsu 全体の設計意図と、各リポジトリの関係を整理するドキュメントハブです。

## コンセプト

keisetsu の中心は、無料で使える OSS 単語帳です。

- 学習データを SQLite（`.kdb`）で公開し、誰でも取得できる
- モバイルで軽量に動作し、オフライン学習を可能にする
- データ管理（生成）と学習（利用）を別リポジトリで分離する
- 配布の再現性を `schema.sql` と `catalog`、検証スクリプトで担保する

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

- [keisetsu-admin](../keisetsu-admin/README.md)
  - Next.js ベースの deck 編集UI
  - CSV取り込み、kdb取り込み、kdb再出力
  - deck manifest（JSON）と zip バンドル出力

- [keisetsu-database](../keisetsu-database/README.md)
  - 配布対象 `databases/*.kdb` の保管
  - スキーマ契約 `schema.sql`
  - 配布インデックス `catalog/catalog.json`
  - catalog更新・形式検証・整合性検証スクリプト

- [keisetsu-mobile](../keisetsu-mobile/README.md)
  - Expo + React Native の学習アプリ
  - GitHub catalog から deck 一覧を取得
  - kdbダウンロード / ローカル取り込み
  - 学習モードとテストモード

## 標準ワークフロー

1. `keisetsu-admin` でカードを作成・編集し、`.kdb` と deck manifest を生成する
2. `keisetsu-database` に `.kdb` と manifest を配置する
3. `npm run build` で `catalog/catalog.json` を再生成する
4. `npm run validate` で形式と整合性を検証する
5. GitHub に push または tag を作成して配布する
6. `keisetsu-mobile` で catalog 経由の deck 取得と学習動作を確認する

## 配布モデル

- 公開URLは GitHub Raw 形式を利用
- deck 一覧は `catalog/catalog.json` を起点に manifest 参照
- 実データは `databases/*.kdb`

```text
https://raw.githubusercontent.com/{owner}/{repo}/{ref}/catalog/catalog.json
https://raw.githubusercontent.com/{owner}/{repo}/{ref}/catalog/decks/{deck-id}.json
https://raw.githubusercontent.com/{owner}/{repo}/{ref}/databases/{deck-file}.kdb
```

## ドキュメント運用メモ

- 初回リリースまでは、設計見直しに伴う破壊的変更が繰り返し入る前提で運用する
- 初回リリース前の仕様・データ形式・UI は安定版ではないため、互換性を保証しない
- スキーマ変更時は mobile/admin/database の README を同時更新する
- 互換性に影響する変更は配布タグと更新履歴を明記する
- 例示SQLは `keisetsu-database/schema.sql` と必ず一致させる

## 今後のTODO

- mobile（Expo）アプリを公開し、配布ページとインストール導線を整備する
- admin（Vercel）を公開し、外部ユーザーがすぐに deck を編集できる状態にする
- モバイルアプリと管理画面のUI文言を多言語化し、言語切り替え機能を実装する
- README を多言語対応し、日本語・英語など複数言語で閲覧できるようにする
- 単体テスト・E2Eテストの対象範囲を主要機能まで拡大し、正常系と異常系のテストを追加して CI で毎回実行する
- README に CI 状態・リリース・ライセンスなどのバッジを追加して、状態を可視化する
- PR テンプレートと Issue テンプレートを追加し、変更提案と不具合報告の粒度を揃える