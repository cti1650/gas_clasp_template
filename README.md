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

## 開発方法

詳細は[Document](https://developers.google.com/apps-script/guides/clasp)を参照

[claspを使ってGoogle Apps Scriptの開発環境を構築してみた | DevelopersIO](https://dev.classmethod.jp/articles/vscode-clasp-setting/)  
[GASをgit管理したいので、Clasp環境を作る](https://zenn.dev/marusho/scraps/3579309aabf5eb)  




### ログイン

```
clasp login
```

### 既存スクリプトをcloneする

```
clasp clone {scriptId} --rootDir ./src
```

### GAS を開く

```
clasp open
```

- Staging環境
  ```
  yarn open
  ```

- Prod環境
  ```
  yarn open:prod
  ```

### スクリプトをpushする

```
clasp push
```

- Staging環境
  ```
  yarn push
  ```

- Prod環境
  ```
  yarn push:prod
  ```

### スクリプトをpullする

```
clasp pull
```

- Staging環境
  ```
  yarn pull
  ```

- Prod環境
  ```
  yarn pull:prod
  ```

### デプロイをアップデートする(初回は手動でデプロイ要)

```
clasp deploy
```

- Staging環境
  ```
  yarn deploy
  ```

- Prod環境
  ```
  yarn deploy:prod
  ```

### 状況確認

#### バージョン一覧

```
clasp versions
```

#### デプロイ一覧

```
clasp deployments
```

### 更新処理

#### 新規バージョン発行

```
clasp version "new version"
```
