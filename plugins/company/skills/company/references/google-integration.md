# Google 連携ガイド

cc-company の秘書と Google カレンダー・タスクを連携させる手順です。

---

## 選択肢

| やりたいこと | おすすめの MCP サーバー |
|---|---|
| カレンダーだけ | `@cocal/google-calendar-mcp` |
| カレンダー + タスク + Gmail など全部 | `google_workspace_mcp`（Python） |

---

## 方法A: Google カレンダーだけ使う（かんたん）

### 1. Google Cloud Console で認証情報を作る

1. [Google Cloud Console](https://console.cloud.google.com/) にアクセス
2. プロジェクトを作成（または既存のものを選択）
3. 「APIとサービス」→「ライブラリ」→ **Google Calendar API** を有効化
4. 「APIとサービス」→「認証情報」→「認証情報を作成」→ **OAuth 2.0 クライアントID**
5. アプリの種類: **デスクトップアプリ**
6. 作成後、JSONファイルをダウンロード → `~/gcp-oauth.keys.json` として保存
7. 「OAuth 同意画面」でテストユーザーに自分のGmailを追加

### 2. Claude Code に MCP サーバーを設定

`claude mcp add` コマンドで追加:

```bash
claude mcp add google-calendar -- npx -y @cocal/google-calendar-mcp
```

または `~/.claude.json` に直接書く:

```json
{
  "mcpServers": {
    "google-calendar": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@cocal/google-calendar-mcp"],
      "env": {
        "GOOGLE_OAUTH_CREDENTIALS": "~/gcp-oauth.keys.json"
      }
    }
  }
}
```

### 3. 認証する

Claude Code を起動して「Googleカレンダーを認証して」と言うと、ブラウザが開きます。Googleアカウントでログインすれば完了。

---

## 方法B: カレンダー + タスク + Gmail をまとめて使う

### 1. 同じく Google Cloud Console で認証情報を作る（方法Aと同じ手順）

追加で有効にするAPI:
- **Google Calendar API**
- **Google Tasks API**
- **Gmail API**（メールも使う場合）

### 2. Python の uv をインストール

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### 3. Claude Code に MCP サーバーを設定

```bash
claude mcp add google-workspace -- uvx workspace-mcp
```

または `~/.claude.json` に直接書く:

```json
{
  "mcpServers": {
    "google-workspace": {
      "type": "stdio",
      "command": "uvx",
      "args": ["workspace-mcp"],
      "env": {
        "GOOGLE_OAUTH_CLIENT_ID": "あなたのクライアントID",
        "GOOGLE_OAUTH_CLIENT_SECRET": "あなたのクライアントシークレット"
      }
    }
  }
}
```

### 3. 認証する

Claude Code を起動して「Google連携を認証して」と言えばブラウザが開きます。

---

## 連携後にできること

秘書に話しかけるだけで、Google と連携します:

```
> 明日の予定を教えて
秘書: Google カレンダーを確認しますね。
      - 10:00 クライアントA ミーティング
      - 14:00 デザインレビュー

> 来週の水曜に打ち合わせ入れて
秘書: Google カレンダーに追加しました。TODOにもリマインダーを入れておきますね。

> このタスクをGoogleタスクにも追加して
秘書: Google Tasks に追加しました。
```

---

## トラブルシューティング

| 症状 | 対処 |
|---|---|
| 認証画面が出ない | OAuth 同意画面でテストユーザーに自分を追加したか確認 |
| API エラー | Google Cloud Console で対象 API が有効か確認 |
| MCP サーバーが起動しない | `npx -y @cocal/google-calendar-mcp` を直接実行してエラーを確認 |
