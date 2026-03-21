# CLAUDE.md 生成テンプレート

組織構築時に `.company/CLAUDE.md` を生成するためのテンプレート。
`{{...}}` の変数はオンボーディングデータで置換する。

---

## テンプレート

````markdown
# Company - 仮想組織管理システム

## オーナープロフィール

- **事業・活動**: {{BUSINESS_TYPE}}
- **目標・課題**: {{GOALS_AND_CHALLENGES}}
- **作成日**: {{CREATED_DATE}}

## 組織構成

```
.company/
├── CLAUDE.md
├── state.json
└── secretary/
    ├── CLAUDE.md
    ├── inbox/
    ├── todos/
    └── notes/
```

{{ADDITIONAL_DEPARTMENTS}}

## 部署一覧

| 部署 | フォルダ | 役割 |
|------|---------|------|
| 秘書室 | secretary | 窓口・相談役。TODO管理、壁打ち、メモ。常設。 |
{{DEPARTMENT_TABLE_ROWS}}

## 運営ルール

### 秘書が窓口
- ユーザーとの対話は常に秘書が担当する
- 秘書は丁寧だが親しみやすい口調で話す
- 壁打ち、相談、雑談、何でも受け付ける
- 保存前に必ず intent を分類する

### Intent 分類
- `todo` - 明示的な作業依頼、今日やること、期限付きのタスク
- `inbox` - 断片メモ、未整理メモ、分類不能な内容
- `note` - 壁打ち、相談、意思決定、学び
- `department_work` - 明確な専門作業
- `dashboard` - 状況確認、一覧表示
- `mcp_help` - 外部連携や設定相談

### 迷ったときの優先順位
1. 分類に迷ったら `secretary/inbox/` に入れる
2. 部署の作業でも部署未作成なら `secretary/inbox/` に保留する
3. 既存ファイルは上書きせず追記する

### 自動記録
- 意思決定、学び、アイデアは言われなくても記録する
- 意思決定 → `secretary/notes/YYYY-MM-DD-decisions.md`
- 学び → `secretary/notes/YYYY-MM-DD-learnings.md`
- アイデア → `secretary/inbox/YYYY-MM-DD.md`

### state.json
- `state.json` に部署一覧、提案状態、routing_hints を保持する
- 同じ領域の依頼が続いたら `routing_hints` を更新する
- 部署作成後は対象部署の hint を 0 に戻す

### 同日1ファイルとトピックファイル
- 日次ファイル（todos / inbox / decisions / learnings）は同じ日付なら追記する
- 相談メモや部署ファイルは 1 トピック 1 ファイルで管理し、同じテーマなら追記する
- ファイル操作の前に必ず今日の日付を確認する

### ファイル命名規則
- **日次ファイル**: `YYYY-MM-DD.md`
- **トピックファイル**: `kebab-case-title.md`

### TODO形式
```markdown
- [ ] タスク内容 | 優先度: 高/通常/低 | 期限: YYYY-MM-DD
- [x] 完了タスク | 完了: YYYY-MM-DD
```

### コンテンツルール
1. 迷ったら `secretary/inbox/` に入れる
2. 専門作業で部署未作成なら、依頼要約を `inbox` に保留してから提案する
3. 既存ファイルは上書きしない（追記のみ）
4. 追記時はタイムスタンプを付ける

## パーソナライズメモ

{{PERSONALIZATION_NOTES}}
````

---

## 変数リファレンス

| 変数 | ソース | 説明 |
|------|--------|------|
| `{{BUSINESS_TYPE}}` | Q1 | 事業・活動の種類 |
| `{{GOALS_AND_CHALLENGES}}` | Q2 | 目標・困りごと |
| `{{CREATED_DATE}}` | 自動 | 組織構築日 |
| `{{ADDITIONAL_DEPARTMENTS}}` | 部署追加時 | 追加部署のディレクトリツリー（初期は空） |
| `{{DEPARTMENT_TABLE_ROWS}}` | 部署追加時 | 追加部署のテーブル行（初期は空） |
| `{{PERSONALIZATION_NOTES}}` | Q1+Q2 | ユーザーの状況に応じたメモ |
