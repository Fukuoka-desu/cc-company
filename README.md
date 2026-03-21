# cc-company

Claude Code で仮想組織を構築・運営するプラグインです。

`/company` を実行すると、秘書があなた専用の窓口になります。最初は秘書室だけで始まり、入力は安定したルールで整理されます。迷った内容は `inbox` に保留し、必要な部署だけを後から追加できます。

## インストール

```
/plugin marketplace add Shin-sibainu/cc-company
/plugin install company@cc-company
```

## コンセプト

```
あなた → 秘書（窓口） → 各部署（必要に応じて追加）
```

- **秘書**: 常に窓口。TODO管理、壁打ち、メモ、部署提案を担当
- **部署**: 本当に必要になったときだけ追加。PM、リサーチ、開発など

最初は秘書だけ。シンプルに始めて、必要になったら部署を追加。

## ルーティングの基本

- 入力はまず `todo / inbox / note / department_work / dashboard / mcp_help` に分類
- 分類に迷ったら必ず `secretary/inbox/YYYY-MM-DD.md` に記録
- 部署がまだない専門作業は `inbox` に保留し、勝手に部署を増やさない
- 部署追加の提案根拠は `.company/state.json` に保持する

## 使い方

### 初回セットアップ（3ステップ）

```
> /company

秘書: はじめまして！あなたの秘書になります。
      まず、事業や活動を教えてください。
あなた: フリーランスのWeb開発やってます

秘書: 今の目標や困りごとは？
あなた: SaaSを作って月10万目指してる。タスクが散らかるのが悩み

→ .company/secretary/ と .company/state.json が自動生成される（完了！）
```

### 日常の運営

```
> /company
秘書: おはようございます！何かありますか？

> 今日やること教えて
秘書: 今日のTODOです:
  - [ ] クライアントAへ見積もり送付
  - [ ] LP設計書のレビュー

> 競合サービスについて調べて
秘書: リサーチ系の依頼として扱えそうです。
      まだリサーチ部門がないので、まずは inbox に整理しておきますね。
  → secretary/inbox/2026-03-21.md に記録

> 海外のトレンドも知りたい
秘書: リサーチ系の依頼が続いています。
      リサーチ部門を作ると topics/ に分けて管理できます。作りましょうか？
あなた: 作って
  → research/ が自動生成される
```

## 部署（必要に応じて追加）

| 部署 | 担当領域 |
|------|---------|
| 秘書室 | TODO管理、壁打ち、メモ、相談（常設） |
| PM | プロジェクト進捗、チケット管理 |
| リサーチ | 市場調査、競合分析、技術調査 |
| マーケティング | コンテンツ企画、SNS、キャンペーン |
| 開発 | 技術ドキュメント、設計、デバッグ |
| 経理 | 請求書、経費、売上管理 |
| 営業 | クライアント管理、提案書 |
| クリエイティブ | デザインブリーフ、ブランド管理 |
| 人事 | 採用管理、チーム管理 |

## 初期構成

```
.company/
├── CLAUDE.md              ← 組織ルール
├── state.json             ← 部署一覧と提案状態
└── secretary/
    ├── CLAUDE.md           ← 秘書の振る舞い
    ├── inbox/
    ├── todos/
    │   └── YYYY-MM-DD.md   ← 今日のTODO
    └── notes/
```

## v3 への移行

既存の v1 / v2 組織がある場合、`/company` 実行時に v3 への移行を提案します。

- 迷った入力 → `secretary/inbox/` に統一
- 部署提案の根拠 → `.company/state.json` に保存
- legacy の `ceo/` / `reviews/` → 削除対象
- 使用中の部署 → そのまま引き継ぎ

## ファイル構成

```
cc-company/
├── .claude-plugin/
│   └── marketplace.json
├── plugins/
│   └── company/
│       ├── .claude-plugin/
│       │   └── plugin.json
│       └── skills/
│           └── company/
│               ├── SKILL.md
│               └── references/
│                   ├── departments.md
│                   ├── claude-md-template.md
│                   └── state-template.json
├── README.md
└── LICENSE
```

## ライセンス

MIT
