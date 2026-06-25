# Claude Code を steering する

Claude Code の挙動を制御する **7つの仕組み**（CLAUDE.md・Rules・Skills・Subagents・Hooks・Output Styles・append-system-prompt）を、
**「どこに置くか（配置場所）」** と **「いつ使うか（ユースケース）」** の観点から、初心者向けに解説する Marp デッキです。

元ネタ: [Steering Claude Code: skills, hooks, rules, subagents, and more](https://claude.com/ja/blog/steering-claude-code-skills-hooks-rules-subagents-and-more)

## ねらい

- MECE であることよりも **分かりやすさ優先**。説明が多少重複しても、初学者がつまずかないことを重視。
- 各仕組みについて必ず **「正体 → 📁 置き場所 → 使いどころ」** の順で触れる。
- 最後に **決定フレームワーク**（やりたいこと → 選ぶ道具 → 置き場所）で全体を1枚に統合。

## 構成（セクション）

| # | セクション | 扱う仕組み |
|---|---|---|
| 00 | 全体像 | なぜ steering か / 7つの道具早見表 / 3つの評価軸 / `.claude/` 置き場所マップ |
| 01 | CLAUDE.md | プロジェクトの常識・200行ルール |
| 02 | Rules | `paths:` で限定する規約 |
| 03 | Skills | 呼び出して使う手順書 |
| 04 | Subagents | 別働隊に任せる専門エージェント |
| 05 | Hooks | イベントで確実に動く自動処理 |
| 06 | Output Styles / append-system-prompt | システムプロンプト操作 |
| 07 | まとめ | 決定フレームワーク / 段階化の原則 / 出典 |

## 配置場所チートシート

```text
your-project/
├── CLAUDE.md                        # 常に読まれる基盤メモ（200行以下）
└── .claude/
    ├── rules/        <名前>.md       # paths: で対象を限定する規約
    ├── skills/       <名前>/SKILL.md # 手順書（呼び出し時に展開）
    ├── agents/       <名前>.md       # サブエージェント定義
    ├── output-styles/<名前>.md       # 出力スタイル
    └── settings.json                # hooks などの設定

~/.claude/  … 同じ構成の「自分の全プロジェクト共通」版（個人設定）
```

`--append-system-prompt` だけはファイルではなく CLI フラグ（`claude --append-system-prompt "..."`）。

## ビルド

```bash
# PDF
npx -y @marp-team/marp-cli@latest --theme themes/minedia.css slides.md -o build/claude-code-steering.pdf

# HTML
npx -y @marp-team/marp-cli@latest --theme themes/minedia.css slides.md -o build/claude-code-steering.html

# PNG（各スライドを画像化・崩れ確認用）
npx -y @marp-team/marp-cli@latest --theme themes/minedia.css --images png slides.md -o build/preview.png
```

> VS Code の「Marp for VS Code」拡張を入れると、`slides.md` をその場でプレビューできます。
