# ファイル構成

## プラグインの構成

```
cc-company/
├── .claude-plugin/
│   └── marketplace.json        ← マーケットプレース登録情報
├── .github/
│   └── workflows/
│       └── deploy-docs.yml     ← ドキュメント自動デプロイ
├── plugins/
│   └── company/
│       ├── .claude-plugin/
│       │   └── plugin.json     ← プラグインメタデータ
│       └── skills/
│           └── company/
│               ├── SKILL.md    ← スキル定義（ワークフロー全体）
│               └── references/
│                   ├── departments.md         ← 部署テンプレート集
│                   ├── claude-md-template.md  ← CLAUDE.md 生成テンプレート
│                   └── state-template.json    ← state.json の雛形
├── docs/                       ← ドキュメントサイト（VitePress）
├── package.json
├── README.md
└── LICENSE
```

## 生成される組織構成

`/company` 実行後に作られる `.company/` フォルダの構成です。

### 初期状態

```
.company/
├── CLAUDE.md              ← 組織ルール・オーナー情報
├── state.json             ← 部署一覧・提案状態・ルーティングヒント
└── secretary/
    ├── CLAUDE.md           ← 秘書の振る舞いルール
    ├── inbox/              ← クイックキャプチャ
    ├── todos/              ← 日次タスク管理
    │   └── YYYY-MM-DD.md
    └── notes/              ← 壁打ち・相談メモ
```

### 部署追加後の例

```
.company/
├── CLAUDE.md
├── secretary/
│   ├── CLAUDE.md
│   ├── inbox/
│   ├── todos/
│   └── notes/
├── research/              ← 追加された部署
│   ├── CLAUDE.md
│   └── topics/
└── pm/                    ← 追加された部署
    ├── CLAUDE.md
    ├── projects/
    └── tickets/
```

## ファイル命名規則

| パターン | 形式 | 例 |
|---------|------|-----|
| 日次ファイル | `YYYY-MM-DD.md` | `2026-03-16.md` |
| トピックファイル | `kebab-case.md` | `competitor-analysis.md` |
| 意思決定ログ | `YYYY-MM-DD-decisions.md` | `2026-03-16-decisions.md` |
| テンプレート | `_template.md` | `_template.md` |

## TODO形式

```markdown
- [ ] タスク内容 | 優先度: 高/通常/低 | 期限: YYYY-MM-DD
- [x] 完了タスク | 完了: YYYY-MM-DD
```

## state.json

```json
{
  "version": 3,
  "departments": ["secretary"],
  "routing_hints": {
    "pm": 0,
    "research": 0,
    "marketing": 0,
    "engineering": 0,
    "finance": 0,
    "sales": 0,
    "creative": 0,
    "hr": 0
  },
  "last_active_date": "YYYY-MM-DD",
  "pending_proposals": []
}
```

- `departments`: 現在有効な部署一覧
- `routing_hints`: 同じ領域の依頼が続いた回数
- `pending_proposals`: 提案中の部署や保留中の整理事項

## 運用ルール

- **同日1ファイル**: 日次ファイル（todos / inbox / decisions / learnings）は同じ日付なら追記する
- **1トピック1ファイル**: 相談メモや部署ファイルは同じテーマなら既存ファイルに追記する
- **日付チェック**: ファイル操作前に必ず今日の日付を確認
- **上書き禁止**: 既存ファイルは追記のみ
- **迷ったら inbox**: 分類に迷ったら `secretary/inbox/` に入れる
