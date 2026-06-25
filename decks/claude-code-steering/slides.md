---
marp: true
theme: minedia
paginate: false
size: 16:9
title: Claude Code を steering する
author: Minedia, Inc.
description: Skills・Hooks・Rules・Subagents・CLAUDE.md など、Claude Code の挙動を制御する7つの仕組みを、配置場所とユースケースから初心者向けに解説する
---

<!-- _class: cover -->

<p class="eyebrow">MINEDIA / CLAUDE CODE — 2026</p>

# Claude Code を steering する

## 〜Skills・Hooks・Rules・Subagents で「思いどおり」に動かす〜

<p class="eyebrow" style="margin-top:2em">7つの仕組み × 置き場所 × 使いどころ</p>

---

<!-- _class: section -->

<p class="eyebrow">SECTION</p>
<div class="section-number">00</div>

# 全体像 — なぜ steering なのか

---

## なぜ Claude Code を「steering（操舵）」するのか

- **毎回プロンプトに書くのは限界がある** — 忘れる・人によってぶれる・会話のコンテキストを食いつぶす。

- **「どう動くか」をファイルとして外に置く** → いつ呼んでも同じ品質で動く。これが steering の発想。

- **プロジェクトに置けばチーム全員で共有できる** — 一度書けば、全員 × 何度でも再利用できる。

<div class="callout">

steering とは、**Claude の振る舞いをプロンプトの「外側」に設計しておく**こと。
道具は7つあり、それぞれ「置き場所」と「得意な場面」が違う。

</div>

---

<!-- _class: dense -->

## steering の7つの道具 — 置き場所つき早見表

| 道具 | 置き場所 | ひとことで |
|---|---|---|
| **CLAUDE.md** | `./CLAUDE.md` | 常に効くプロジェクトの常識 |
| **Rules** | `./.claude/rules/*.md` | 特定フォルダだけの規約 |
| **Skills** | `./.claude/skills/<名前>/SKILL.md` | 呼び出して使う手順書 |
| **Subagents** | `./.claude/agents/<名前>.md` | 別働隊に任せる専門エージェント |
| **Hooks** | `./.claude/settings.json` | イベントで確実に動く自動処理 |
| **Output Styles** | `./.claude/output-styles/<名前>.md` | 役割・口調をまるごと変える |
| **append-system-prompt** | CLIフラグ（ファイル無し） | その場限りで指示を足す |

---

## 道具を選ぶ「3つのものさし」

- **① いつ読まれる？（When loaded）** — 常にか、特定フォルダに触れた時か、呼んだ時か。

- **② 長い会話で残る？（Compaction）** — 会話が伸びて履歴が要約されても、その指示が消えないか。

- **③ どれだけ重い？（Context cost）** — 使うトークン量。**常に読み込む＝高コスト**。

<div class="callout">

迷ったら **「常に必要か／特定の時だけか／呼んだ時だけか」** を自問する。
答えがそのまま、選ぶべき道具に対応する。

</div>

---

## すべては `.claude/` に集まる — 置き場所マップ

```text
your-project/
├── CLAUDE.md                       # 常に読まれる基盤メモ
└── .claude/
    ├── rules/        api.md        # paths: で対象を限定するルール
    ├── skills/       <名前>/SKILL.md # 手順書（呼び出し時に展開）
    ├── agents/       <名前>.md      # サブエージェント定義
    ├── output-styles/<名前>.md      # 出力スタイル
    └── settings.json               # hooks などの設定

~/.claude/  … 同じ構成の「自分の全プロジェクト共通」版（個人設定）
```

> プロジェクト直下の `.claude/` はチーム共有（git管理）、ホームの `~/.claude/` は自分専用。

---

<!-- _class: section -->

<p class="eyebrow">SECTION</p>
<div class="section-number">01</div>

# CLAUDE.md — プロジェクトの常識

---

## CLAUDE.md とは / どこに置く

- **正体** — プロジェクトの「常識」を書いたマークダウン。セッション開始時に**自動で読まれ、会話中ずっと保持**される。最も確実に効くが、最も重い。

- **📁 置き場所**
  - `./CLAUDE.md` — プロジェクト直下。チーム共有の基盤。
  - `./<サブフォルダ>/CLAUDE.md` — そのフォルダのファイルを触った時だけ読まれる。
  - `~/.claude/CLAUDE.md` — 自分の全プロジェクト共通。

<div class="callout">

一度読むと**キャッシュ（memoized）**され、同じセッション中は読み直さない。

</div>

---

## CLAUDE.md の使いどころ

- **書くと良いもの** — ビルド/テストのコマンド、ディレクトリ構成、命名規則、チームの約束ごと。**「毎回知っていてほしい前提」**。

- **使用例** — 「テストは `npm test`」「`src/` がアプリ本体」「コミットメッセージは日本語」。

<div class="callout">

⚠️ **200行以下に保つ**のが目安。常に読まれる＝行数がそのままコスト。
ふくらんできたら、手順は **Skills** へ、特定フォルダだけの規約は **Rules** へ引っ越す。

</div>

---

<!-- _class: section -->

<p class="eyebrow">SECTION</p>
<div class="section-number">02</div>

# Rules — 必要なときだけ効く規約

---

## Rules とは / どこに置く

- **正体** — 制約・規約を書いたマークダウン。CLAUDE.md より細かく、**特定のフォルダに触れた時だけ**読み込める。

- **📁 置き場所** — `./.claude/rules/<名前>.md`

- **限定のしかた** — 先頭の `paths:` で対象を指定する。

```yaml
---
paths:
  - "src/api/**"
---
APIハンドラでは、入力を必ず Zod で検証すること。
```

> `paths:` を書かなければ CLAUDE.md と同じく常に読まれる。書けば「関係する時だけ」。

---

## Rules の使いどころ

- **特定フォルダ限定の決まりごと** に最適。関係ない作業の間は**コンテキストを1トークンも使わない**。

- **使用例**
  - `src/api/**` … 入力は Zod で検証
  - `**/*.test.ts` … テストは AAA パターンで書く
  - `db/migrations/**` … 破壊的変更には必ずコメント

<div class="callout">

CLAUDE.md は「プロジェクト全体の常識」、Rules は「**この場所ではこうする**」。
同じ規約でも、効く範囲が狭いなら Rules のほうが軽い。

</div>

---

<!-- _class: section -->

<p class="eyebrow">SECTION</p>
<div class="section-number">03</div>

# Skills — 呼び出して使う手順書

---

## Skills とは / どこに置く

- **正体** — 名前・説明・手順をまとめた**再利用できる手順書**。開始時は**名前と説明だけ**読まれ、本体は**呼んだ時に展開**される（だから軽い）。

- **📁 置き場所**
  - `./.claude/skills/<名前>/SKILL.md` — プロジェクト共有。
  - `~/.claude/skills/<名前>/SKILL.md` — 個人用。

- **呼び出し方** — `/<名前>` のスラッシュコマンド、または説明文にマッチして**自動起動**。

> 1スキル＝1フォルダ。中の `SKILL.md` が本体（手順）。

---

## Skills の使いどころ

- **手順が決まった作業**を丸ごと部品化する。コードレビュー、デプロイ手順、リリースのチェックリストなど。

- **使用例** — `/code-review` で定型レビュー、`/release` でリリース作業を一気に。

<div class="callout">

記事の原則: **「手続き的な指示は CLAUDE.md ではなく Skills に置く」**。
本体は使う時しか読まれないので、いくつ作っても**普段のコストは増えない**。

</div>

---

<!-- _class: section -->

<p class="eyebrow">SECTION</p>
<div class="section-number">04</div>

# Subagents — 別働隊に任せる

---

## Subagents とは / どこに置く

- **正体** — 独立した専門エージェント。**自分専用のコンテキスト**で動き、メインに返すのは**最終結果だけ**。途中経過でメイン会話を散らかさない。

- **📁 置き場所**
  - `./.claude/agents/<名前>.md` — プロジェクト共有。
  - `~/.claude/agents/<名前>.md` — 個人用。

- **読み込み** — 開始時は名前・説明・使えるツールだけ。呼ぶと Agent ツール経由で別働隊として走る。

> Skills は「メイン会話の中で手順を実行」、Subagents は「**別室で完結させて結論だけ持ち帰る**」。

---

## Subagents の使いどころ

- **過程が長いが、欲しいのは結論だけ**の作業に最適。深い検索、大量ログの解析、依存関係の監査など。

- **使用例** — 「このログを解析して原因だけ教えて」をサブエージェントに丸投げ → メインには結論の一行だけ返る。

<div class="callout">

中間出力が多くてメイン会話を埋めてしまう側タスクは、Subagent に隔離する。
**並列で複数の別働隊**を走らせることもできる。

</div>

---

<!-- _class: section -->

<p class="eyebrow">SECTION</p>
<div class="section-number">05</div>

# Hooks — 確実に動く自動処理

---

## Hooks とは / どこに置く

- **正体** — ファイル編集・ツール実行・セッション開始などの**イベントで発火**する自動処理。AIの判断ではなく**決定論的（必ず動く）**なのが本質。

- **📁 置き場所**
  - `./.claude/settings.json` の `hooks` キー — プロジェクト共有。
  - `./.claude/settings.local.json` — 自分だけ（git管理外）。
  - `~/.claude/settings.json` — 全プロジェクト共通。

- **種類** — command（コマンド実行）/ HTTP / prompt（LLMに判断させる）など。

> コンテキストの外で動くので軽く、長い会話で履歴が要約されても**挙動がぶれない**。

---

## Hooks の使いどころ

- **「毎回かならず起きてほしい」処理**に最適。AIの気まぐれを排除できる。

- **使用例**
  - 編集後に自動で Prettier をかける
  - コミット前にテストを走らせ、落ちたら止める
  - 危険なコマンドをブロックする／完了時に Slack 通知

<div class="callout">

原則: **決定論的に起きるべきことは Hooks**。
「お願いベース」では時々忘れる処理を、仕組みで固定する。

</div>

---

<!-- _class: section -->

<p class="eyebrow">SECTION</p>
<div class="section-number">06</div>

# Output Styles & append-system-prompt

---

## Output Styles とは / どこに置く

- **正体** — **システムプロンプトそのもの**に指示を注入し、役割や口調をまるごと変える。常に読まれ、要約でも消えず、**最も指示が強く効く**。

- **📁 置き場所**
  - `./.claude/output-styles/<名前>.md` — プロジェクト共有。
  - `~/.claude/output-styles/<名前>.md` — 個人用。
  - 切り替え: `/output-style`

<div class="callout">

強力ゆえ既定の指示を**上書き**しうる。自作の前に、まず**組み込みスタイル**
（Explanatory・Learning など）で足りないか確認するのが定石。

</div>

---

## append-system-prompt とは / どう使う

- **正体** — CLIフラグで、その起動時だけシステムプロンプトに指示を**追記**する。**ファイルに残らない**、呼び出し単位の手段。

- **📁 置き場所** — ファイル無し。コマンドで渡す。

```bash
claude --append-system-prompt "回答は必ず日本語。コードにはコメントを付ける"
```

<div class="callout">

上書きではなく**加算的**なので、既定の指示を壊さず安全。
役割ごと変えたいなら Output Styles、その場で一言足したいだけなら append。

</div>

---

<!-- _class: section -->

<p class="eyebrow">SECTION</p>
<div class="section-number">07</div>

# まとめ — どれを選ぶか

---

<!-- _class: dense -->

## 決定フレームワーク — 必要なこと → 選ぶ道具

| やりたいこと | 選ぶ道具 | 置き場所 |
|---|---|---|
| 常に効く基盤情報 | **CLAUDE.md** | `./CLAUDE.md` |
| 特定フォルダだけの規約 | **Rules** | `./.claude/rules/` |
| 決まった手順を再利用 | **Skills** | `./.claude/skills/<名前>/` |
| 結論だけ欲しい重い作業 | **Subagents** | `./.claude/agents/` |
| 毎回かならず動かす | **Hooks** | `./.claude/settings.json` |
| 役割・口調を変える | **Output Styles** | `./.claude/output-styles/` |
| その場で一言足す | **append-system-prompt** | CLIフラグ |

---

## 段階化の原則 — まず CLAUDE.md、ふくらんだら引っ越す

- **スタートは CLAUDE.md** に基盤を書く。ただし**200行以下**を守る。

- ふくらんできたら切り出す：
  - 特定フォルダ限定の規約 → **Rules**（`paths:` で限定）
  - 決まった手順 → **Skills**（呼び出し時だけ展開）

- さらに、**結論だけ欲しい重作業は Subagents**、**必ず動かす処理は Hooks**、**役割変更は Output Styles**。

<div class="callout">

合言葉は **「常時 / 特定の場所 / 呼んだ時 / 別働隊 / 自動 / 役割変更」**。
このどれかを問えば、置き場所まで一直線に決まる。

</div>

---

## 出典 / もっと学ぶ

- **元記事** — Steering Claude Code: skills, hooks, rules, subagents, and more
  https://claude.com/ja/blog/steering-claude-code-skills-hooks-rules-subagents-and-more

- **公式ドキュメント**
  - Memory（CLAUDE.md）: https://docs.claude.com/en/docs/claude-code/memory
  - Skills: https://docs.claude.com/en/docs/claude-code/skills
  - Subagents: https://docs.claude.com/en/docs/claude-code/sub-agents
  - Hooks: https://docs.claude.com/en/docs/claude-code/hooks
  - Output Styles: https://docs.claude.com/en/docs/claude-code/output-styles

---

<!-- _class: closing -->

# 置き場所が分かれば、steering は怖くない

## まず `CLAUDE.md` を1枚。ふくらんだら `.claude/` に引っ越そう。
