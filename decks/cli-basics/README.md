# AI時代のコマンドライン入門 〜エンジニアだけの道具から、AIを使う全員の道具へ〜

> [CLI オンボーディング登壇資料シリーズ](../../README.md) の1デッキ（`cli-basics`）です。

Minedia社員向け（社外公開可）の UNIX / CLI 入門ハンズオン講座。

完成版スライド（PDF / PPTX / HTML）は [GitHub Releases](https://github.com/minedia/cli-onboarding/releases/latest) からダウンロードできます。

## なぜこの講座をやるのか

> 1000個のファイル名を一括で変えたい。
> GUIなら **2時間**。CLIなら **3秒**。

普段の業務で「同じ作業を100回繰り返している」「Claude Codeを使いたいけどターミナルが怖い」「Pythonスクリプトをもらったけど動かし方がわからない」――こうした"あと一歩"の壁は、ほとんどがCLI（コマンドラインインターフェース）の基礎知識で解決します。

GUIだけでPCを使うのは、カーナビしか付いていない車で出張するようなもの。行ける場所は限られるし、寄り道もできません。CLIを覚えると、あなたのPCは**自分で運転できる車**に変わります。

この講座のゴールは、受講後に「Claude CodeやPythonスクリプトを"自分で動かせる人"になる」こと。たった60分です。

---

## 対象者

**Claude Code は既に使っている。でも、もっと使いこなしたい人** のための講座です。

**こんな人向け：**
- Claude Code に頼んで出てきたコマンドの**意味がわからない**
- 「ターミナルでこれを実行してください」で**詰まる**
- 「カレントディレクトリ」「環境変数」「パス」と聞いてピンと来ない
- 100ファイルの処理を GUI で1個ずつクリックしている

**前提：**
- Claude Code がインストール済み（簡単な使い方は知っている）
- ノートPC（Windows / Mac いずれも対応）
- **Windowsユーザーは Git Bash を使います**（事前にGit for Windowsをインストール）。Mac は標準ターミナル（zsh）。
- こうすることで、講座中に登場するコマンドが Windows / Mac 両方でほぼ同じになり、方言の差を気にする必要がなくなります。

---

## ゴール

受講後、以下ができるようになります。

1. ターミナル（Git Bash on Windows / macOSターミナル）を自分で開ける
2. カレントディレクトリ・ホームディレクトリの概念を説明できる（`~` の意味も）
3. 基本的なファイル/ディレクトリ操作コマンドが打てる（`cd` / `ls` / `mkdir` / `cp` / `mv` / `rm`）
4. `find` / `grep` でファイルや中身を**探せる**（= AIエージェントの心臓部と同じこと）
5. 環境変数 `PATH` を覗いて意味がわかる
6. **Claude Code を自分のターミナルから起動して、業務を任せられる**

---

## 開催概要

| 項目 | 内容 |
|------|------|
| 形式 | 対面・ハンズオン |
| 所要時間 | 60分 |
| 対象OS | Windows（Git Bash）/ macOS（zsh） |
| 講師 | 松倉（株式会社マインディア CTO） |
| 公開範囲 | Minedia社員＋社外公開 |

---

## 事前準備（受講者向け）

**Windowsユーザー**
- [Git for Windows](https://git-scm.com/download/win) をインストール（Git Bash が同梱されます）
- インストール後、スタートメニューから `Git Bash` を起動できるか確認

**Macユーザー**
- ターミナル.app が起動できることを確認（Spotlight で `ターミナル`）

**全員：Claude Code**
- インストール済みであること（簡単な使い方を知っていること）
- ターミナルで `claude --version` で確認できればOK

---

## カリキュラム（60分）

| 時間 | セクション | 内容 |
|------|------------|------|
| 6分  | 0. オープニング | 格差の話／Claude Code の裏側／英語通訳メタファ |
| 5分  | 1. CLIとGUIの違い＋text vs binary | 2つの比較軸（操作方法／保存形式）、ターミナルを開く（ハンズオン①） |
| 10分 | 2. シェルとコマンドの基礎＋ショートカット | コマンドフォーマット、`--help`、基本コマンド5つ、`Ctrl+C`等（ハンズオン②） |
| 13分 | 3. ファイル・ディレクトリ操作 | カレント／ホーム／チルダ／`tree`／GUI⇄CLI（ハンズオン③） |
| 5分  | 4. 探す：`find` と `grep` | AIエージェントの心臓部（ハンズオン④） |
| 3分  | 5. 環境変数 | `PATH` を覗く（ハンズオン⑤） |
| 9分  | 6. Claude Code を自分で動かす | ターミナルから起動 → 自然言語で頼む（ハンズオン⑥）★ゴール |
| 2分  | 7. 次に効くコマンド集 | `curl` `head/tail` `wc` `history` `tree` 他 |
| 4分  | 8. 応用デモ | 一括リサイズ・連番ファイル・find活用・Claude Code |
| 3分  | 9. クロージング | 次のアクション・質疑応答 |

> 詳細な講師用タイムテーブルは [`outline.md`](outline.md) を参照。

---

## 参考資料

- [慶應SFC CNSガイド (2004)](https://cns-guide.sfc.keio.ac.jp/2004/2/index.html)
- [WindowsのLinux環境でWSLではなく、Git Bashが快適だった話 — maes_data](https://note.com/h_yoshida/n/nf650bd4631a3)（Windows ユーザー向けに Git Bash を推奨する背景）

---

## このデッキの構成

```
decks/cli-basics/
├── slides.md          # 本体（Marp Markdown）
├── outline.md         # 講師用 詳細タイムテーブル
├── README.md          # このファイル
├── themes/
│   └── minedia.css    # Minedia design system を移植した Marp テーマ
└── assets/
    ├── text_logo.png  # 右下に表示する Minedia ロゴ
    └── illustrations/ # 図版（SVG）
```

---

## ビルド方法

> **⚠️ 必ずこのディレクトリ（`decks/cli-basics`）に移動してから実行してください。**

### 0. Marp CLI を入れる

```bash
npm install -g @marp-team/marp-cli
# または npx で都度実行: npx @marp-team/marp-cli@latest --version
```

### 1. プレビュー（ホットリロード付き）

```bash
cd decks/cli-basics
marp slides.md --theme themes/minedia.css --watch --preview --html
```

### 2. PDF に変換

```bash
cd decks/cli-basics
marp slides.md --theme themes/minedia.css --pdf --allow-local-files -o cli-basics-slides.pdf
```

### 3. HTML に変換（社外公開・配布用）

```bash
cd decks/cli-basics
marp slides.md --theme themes/minedia.css --html --allow-local-files -o cli-basics-slides.html
```

→ 単一ファイルで出力される。

### 4. PPTX に変換（PowerPoint で開く）

```bash
cd decks/cli-basics
marp slides.md --theme themes/minedia.css --pptx --allow-local-files -o cli-basics-slides.pptx
```

→ 編集可能なPPTXではなく画像化されたスライドになる点に注意。

### 5. PNG 連番に変換（サムネイル・SNS用）

```bash
cd decks/cli-basics
marp slides.md --theme themes/minedia.css --images png --allow-local-files
```

### ロゴ画像が表示されない時

`--allow-local-files` フラグが必須。ローカル PNG への参照を明示的に許可する。

---

## テーマの差し替え

`themes/minedia.css` は [minedia-design](https://github.com/minedia/minedia-skills/tree/main/plugins/corporate-identity/skills/minedia-design) のデザインコントラクトを Marp 用に移植したもの。下記を必ず守ること。

- 全スライドの下端に CI グラデーションバー
- 全スライドの右下に Minedia text logo
- タイトル付きスライドはタイトル左に縦グラデアクセント
- 角は基本 sharp、ページ番号なし
- フォントは Noto Sans JP（見出し・本文）/ Sometype Mono（ラベル）

カスタムクラス：

| クラス | 用途 |
|---|---|
| `cover` | 表紙 |
| `section` | セクション区切り（番号 + タイトル） |
| `dark` | 引き締めコンテンツ（#3C3C3C 背景） |
| `quote` | 引用スライド |
| `closing` | クロージング |

Markdown 内で `<!-- _class: section -->` のように指定して使う。

> テーマは各デッキに複製する方針です。`minedia.css` を更新したら、必要に応じて他デッキにも反映してください。

---

## VS Code で書く場合

[Marp for VS Code](https://marketplace.visualstudio.com/items?itemName=marp-team.marp-vscode) 拡張を入れると、エディタ右側にリアルタイムプレビューが出る。

`.vscode/settings.json`:

```json
{
  "markdown.marp.themes": ["./decks/cli-basics/themes/minedia.css"]
}
```
