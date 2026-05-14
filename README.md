# CLI入門講座 〜黒い画面と仲良くなる60分〜

[![Build slides](https://github.com/minedia/cli-basics/actions/workflows/release.yml/badge.svg)](https://github.com/minedia/cli-basics/actions/workflows/release.yml)

Minedia社員向け（社外公開可）の UNIX / CLI 入門ハンズオン講座の資料リポジトリです。

## 📥 スライドをダウンロード

**最新版**: [GitHub Releases](https://github.com/minedia/cli-basics/releases/latest) から取得できます。

- `cli-basics-slides.pdf` — PDF版（印刷・配布用）
- `cli-basics-slides.pptx` — PowerPoint版（編集したい場合）
- `cli-basics-slides.html` — ブラウザで開く版

`main` ブランチへの push で自動的に再ビルド・新しいリリースが作られます。

---

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
| 形式 | オンライン・ハンズオン |
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

---

## リポジトリ構成（予定）

```
.
├── README.md              # このファイル
├── outline.md             # 詳細目次・タイムテーブル
├── slides/                # 登壇スライド
├── handson/               # 受講者向けハンズオン手順書（Windows/Mac別）
└── examples/              # デモ用サンプルコード・素材
```

---

## 参考資料

- [慶應SFC CNSガイド (2004)](https://cns-guide.sfc.keio.ac.jp/2004/2/index.html)
- [WindowsのLinux環境でWSLではなく、Git Bashが快適だった話 — maes_data](https://note.com/h_yoshida/n/nf650bd4631a3)（Windows ユーザー向けに Git Bash を推奨する背景）

---

## 制作環境

知識共有のためにオープンにします。

- **作成ツール**: [Claude Code Desktop（Cowork mode）](https://www.anthropic.com/claude-code) + **Claude Opus 4.7**
- **スライド**: [Marp](https://marp.app/) — Markdown → PDF / PPTX / HTML
- **CI / 配布**: GitHub Actions（main push でビルド、`v*` タグで Release 自動生成）
- **デザイン**: Minedia Design System（[minedia-skills](https://github.com/minedia/minedia-skills) の `corporate-identity/minedia-design` を Marp 用 CSS に移植）

CTO（松倉）が Claude Code Desktop の Cowork mode で対話しながら、構成・原稿・テーマCSS・CIワークフローまで含めて一気通貫で作成しました。
**AIエージェントで講座資料を作る** こと自体が、本講座のメッセージ（「AIに業務を任せられる人になる」）の実演でもあります。

---

## ライセンス

教材は社外公開予定です。ライセンスは別途検討中。
