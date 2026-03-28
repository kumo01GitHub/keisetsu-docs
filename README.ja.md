# keisetsu ドキュメント

keisetsu 全体の設計意図と運用方針を横断して整理するドキュメントハブです。

この `keisetsu-docs` は、各実装リポジトリ（publisher / database / mobile）をまたいだ仕様の前提、運用ルール、更新手順を一元管理するための場所です。

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

## 利用者向けガイド

### keisetsu モバイルアプリの使い方

1. スマートフォンでExpo Go アプリをインストールしてください。
    - [Expo Go (iOS)](https://apps.apple.com/app/expo-go/id982107779)
    - [Expo Go (Android)](https://play.google.com/store/apps/details?id=host.exp.exponent)
2. QRコードを読み取り、keisetsu アプリを起動してください。

![Expo QR](assets/eas-update.svg)

これで keisetsu アプリをすぐに利用開始できます。

### keisetsu 単語帳編集Webアプリの使い方

1. [keisetsu-publisher 公開ページ](https://keisetsu-publisher.vercel.app) にアクセス
2. 新規 deck を作成、または CSV / 既存 kdb を取り込む
3. カードや deck 情報（ID、タイトル、言語など）を編集
4. 「ダウンロード」でZIPをダウンロード
5. ダウンロードした ZIP を展開し、生成物を keisetsu-database に配置して、[追加・編集申請](https://github.com/kumo01GitHub/keisetsu-database/issues)

### 対応言語

- English (`en`)
- 日本語 (`ja`)

## 開発者向けガイド

詳細なリポジトリ構成・運用ルール・技術情報は [DEVELOPER.md](./DEVELOPER.md) を参照。
