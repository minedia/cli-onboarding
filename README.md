# CLI入門講座 〜黒い画面と仲良くなる60分〜

[![Build slides](https://github.com/minedia/cli-basics/actions/workflows/release.yml/badge.svg)](https://github.com/minedia/cli-basics/actions/workflows/release.yml)
[![Latest release](https://img.shields.io/github/v/release/minedia/cli-basics?label=latest%20slides)](https://github.com/minedia/cli-basics/releases/latest)

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

- ターミナルを開いたことがない、または開いても何をしていいかわからない方
- Claude Code・Python・各種CLIツールを"使いたいけど動かし方がわからない"方
- 「カレントディレクトリ」「環境変数」「パス」と聞いてピンと来ない方
- 業務の繰り返し作業を自動化したいが、最初の一歩が踏み出せない方

OS問わず参加可能（受講者の約9割がWindows想定／Macも対応）。
**Windowsユーザーは Git Bash を使います**（事前にGit for Windowsをインストール）。Mac は標準ターミナル（zsh）。
こうすることで、講座中に登場するコマンドが Windows / Mac 両方でほぼ同じになり、方言の差を気にする必要がなくなります。

---

## ゴール

受講後、以下ができるようになります。

1. ターミナル（Git Bash on Windows / macOSターミナル）を自分で開ける
2. カレントディレクトリ・ホームディレクトリの概念を説明できる（`~` の意味も）
3. 基本的なファイル/ディレクトリ操作コマンドが打てる（`cd` / `ls` / `mkdir` / `cp` / `mv` / `rm`）
4. `find` / `grep` でファイルや中身を**探せる**（= AIエージェントの心臓部と同じこと）
5. 環境変数 `PATH` を覗いて意味がわかる
6. **自分で書いたプログラム（例: `hello.py`）をターミナルから実行できる**

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
- Python のインストール（事前案内の手順書を参照）

**Macユーザー**
- ターミナル.app が起動できることを確認（Spotlight で `ターミナル`）
- Python は標準搭載 or `python3` コマンドで確認

---

## カリキュラム（60分）

| 時間 | セクション | 内容 |
|------|------------|------|
| 6分  | 0. オープニング | 格差の話／Claude Code の裏側／英語通訳メタファ |
| 4分  | 1. CLIとGUIの違い | ターミナルを開く（ハンズオン①） |
| 9分  | 2. シェルとコマンドの基礎 | コマンドフォーマット、`--help`、基本コマンド5つ（ハンズオン②） |
| 13分 | 3. ファイル・ディレクトリ操作 | カレント／ホーム／チルダ／パス（ハンズオン③） |
| 5分  | 4. 探す：`find` と `grep` | AIエージェントの心臓部（ハンズオン④） |
| 4分  | 5. 環境変数 | `PATH` を覗く（ハンズオン⑤） |
| 10分 | 6. プログラムを書いて動かす | `hello.py` 作成 → 実行（ハンズオン⑥）★ゴール |
| 7分  | 7. 応用デモ | 一括リサイズ・連番ファイル・自動化・Claude Code |
| 2分  | 8. クロージング | 次のアクション・質疑応答 |

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

## ライセンス

教材は社外公開予定です。ライセンスは別途検討中。
