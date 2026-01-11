# GAS Clasp Template

## 目的

GASでスクリプトを作成するにあたり都度設定していた内容をすぐに使い始めれるようにテンプレート化し開発の効率化を図る

## GitHub Secrets 設定

GitHub Actionsでclasp push/pullを実行するには、以下のシークレットを設定してください。

### シークレットの取得方法

1. ローカルで `clasp login` を実行
2. `~/.clasprc.json` を開き、以下の値を取得

```json
{
  "token": {
    "access_token": "→ ACCESS_TOKEN",
    "refresh_token": "→ REFRESH_TOKEN",
    "id_token": "→ ID_TOKEN"
  },
  "oauth2ClientSettings": {
    "clientId": "→ CLIENT_ID",
    "clientSecret": "→ CLIENT_SECRET"
  }
}
```

3. SCRIPT_ID は GASエディタのURLから取得: `https://script.google.com/home/projects/{SCRIPT_ID}/edit`

### 必要なシークレット一覧

| シークレット名 | 説明 |
|---------------|------|
| ACCESS_TOKEN | OAuth アクセストークン |
| REFRESH_TOKEN | OAuth リフレッシュトークン |
| ID_TOKEN | OAuth IDトークン |
| CLIENT_ID | OAuth クライアントID |
| CLIENT_SECRET | OAuth クライアントシークレット |
| SCRIPT_ID | GASスクリプトID |

### 環境別プリフィックス

複数環境を使い分ける場合は、以下のプリフィックスを付けてシークレットを登録してください。

| 環境 | プリフィックス | 例 |
|------|---------------|-----|
| Development | `DEV_` | `DEV_SCRIPT_ID` |
| Staging | `STAGING_` | `STAGING_SCRIPT_ID` |
| Production | `PROD_` | `PROD_SCRIPT_ID` |

## セットアップ

### 1. 依存関係のインストール

```bash
yarn install
```

### 2. Claspログイン

```bash
yarn init-serve
# または
clasp login
```

### 3. 環境変数の設定

```bash
yarn env:copy  # .env.example → .env をコピー
```

`.env` を編集して SCRIPT_ID を設定：

```bash
SCRIPT_ID=your_script_id
```

SCRIPT_ID は GASエディタのURLから取得: `https://script.google.com/home/projects/{SCRIPT_ID}/edit`

### 4. 既存スクリプトをcloneする（任意）

```bash
clasp clone {scriptId} --rootDir ./src
```

## 開発方法

詳細は[Document](https://developers.google.com/apps-script/guides/clasp)を参照

- [claspを使ってGoogle Apps Scriptの開発環境を構築してみた | DevelopersIO](https://dev.classmethod.jp/articles/vscode-clasp-setting/)
- [GASをgit管理したいので、Clasp環境を作る](https://zenn.dev/marusho/scraps/3579309aabf5eb)

### コマンド一覧

| コマンド | 環境 | 説明 |
|----------|------|------|
| `yarn push` | ローカル | .env の SCRIPT_ID を使用 |
| `yarn push:staging` | Staging | .clasp-staging.json を使用 |
| `yarn push:prod` | Production | .clasp-prod.json を使用 |

同様に `pull` / `open` / `deploy` も各環境に対応しています。

### GAS を開く

```bash
yarn open            # ローカル環境
yarn open:staging    # Staging環境
yarn open:prod       # Production環境
```

### スクリプトをpushする

```bash
yarn push            # ローカル環境
yarn push:staging    # Staging環境
yarn push:prod       # Production環境
```

### スクリプトをpullする

```bash
yarn pull            # ローカル環境
yarn pull:staging    # Staging環境
yarn pull:prod       # Production環境
```

### デプロイをアップデートする（初回は手動でデプロイ要）

```bash
yarn deploy          # ローカル環境
yarn deploy:staging  # Staging環境
yarn deploy:prod     # Production環境
```

### 状況確認

```bash
clasp versions      # バージョン一覧
clasp deployments   # デプロイ一覧
```

### 新規バージョン発行

```bash
clasp version "new version"
```
