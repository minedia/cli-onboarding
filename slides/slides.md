---
marp: true
theme: minedia
paginate: false
size: 16:9
title: CLI入門講座
author: 松倉 友樹（Minedia CTO）
description: AI時代に効く、いちばん基礎の「英語」を60分で
---

<!-- _class: cover -->

<p class="eyebrow">MINEDIA / TECH SESSION — 2026</p>

# CLI入門講座
## 〜AI時代に効く、いちばん基礎の「英語」を60分で〜

<p class="eyebrow" style="margin-top:2em">松倉 友樹 — Minedia CTO</p>

---

<!-- _class: section -->

<p class="eyebrow">SECTION</p>
<div class="section-number">00</div>

# なぜ今、CLI なのか

---

## まず、結論から

<div class="callout">

AIエージェント時代に、**CLI を知る人と知らない人の生産性は 16 倍以上**違う。
その差は毎月毎月、複利で広がっていく。

</div>

過去：CLI は "エンジニアの道具"
**今：CLI は "AIに仕事を任せる全員の道具"**

AIエージェント（Claude Code、Cursor、各種MCP）は、GUIではなく **テキスト＝コマンドライン** を介して動く。AIに業務を委任しようとすると、必ずどこかで「ターミナル」にぶつかる。

---

## 同じツール・同じ料金・同じ給料 — でも生産性は違う

|  | CLI を使えない人 | CLI を使える人 |
|---|---|---|
| Claude Code で自動化できる業務 | 月 3 時間 | 月 50 時間 |
| 100 ファイルのリネーム | 2 時間（手作業） | **3 秒**（1 コマンド） |
| AI スクリプトをもらったとき | 「動かし方が分からない」 | 即実行・改造・定期化 |
| 生産性（同条件で） | ×1 | **×16** |

<p class="eyebrow" style="margin-top:1em">同じツール・同じ料金・同じ給料 — でも、差は毎月複利で開く</p>

---

## さらに：Claude Code の "裏側" もまったく違う

同じ「このプロジェクトから TODO を全部探して」という依頼でも：

|  | CLI 環境（あなたが使える） | GUI 環境（CLI が分からない） |
|---|---|---|
| AI 内部の動作 | `grep -r "TODO" .` を実行 | スクショ → 解析 → 座標特定 → クリック → スクショ... |
| 所要時間 | **0.5 秒** | 数分〜十数分 |
| トークン消費 | 約 1,000 | **数十万〜数百万**（数百倍） |
| 失敗時の回復 | コマンドを直して再実行 | 何が起きたか不明・最初からやり直し |

<div class="callout">

CLI が使える環境を持っていること自体が、**AI の "燃費" と "賢さ" を桁違いに上げる**。

</div>

---

<!-- _class: quote -->

> AI エージェントは「英語しか喋れない、超優秀なアシスタント」。
> CLI はその英語そのもの。
> 英語が読み書きできない人は、せっかくの優秀な助手に **1 ミリも仕事を頼めない**。

<p class="attribution">今日の 60 分は、その「英語」のいちばん基礎を体に入れる時間。</p>

---

## 今日のゴール

受講後、以下ができるようになります。

1. ターミナル（Git Bash on Windows / macOS ターミナル）を**自分で開ける**
2. カレントディレクトリ・ホームディレクトリの概念を**説明できる**
3. 基本のファイル / ディレクトリ操作コマンドが**打てる**
4. `find` / `grep` で **探せる**（= AI の心臓部と同じこと）
5. 環境変数 `PATH` を**覗いて意味がわかる**
6. ★ **自分で書いたプログラムをターミナルから実行できる**

---

## 60 分のタイムテーブル

| 時刻 | 分 | セクション |
|---|---|---|
| 0:00 | 6  | 00. オープニング（今ここ） |
| 0:06 | 4  | 01. CLI と GUI の違い |
| 0:10 | 9  | 02. シェルとコマンドの基礎 |
| 0:19 | 13 | 03. ファイル・ディレクトリ操作 |
| 0:32 | 5  | 04. 探す：`find` と `grep` |
| 0:37 | 4  | 05. 環境変数 |
| 0:41 | 10 | 06. プログラムを書いて動かす ★ゴール |
| 0:51 | 7  | 07. 応用デモ |
| 0:58 | 2  | 08. クロージング |

---

<!-- _class: section -->

<p class="eyebrow">SECTION</p>
<div class="section-number">01</div>

# CLI と GUI の違い

---

## CLI と GUI — 2つの「PCの動かし方」

**GUI**（Graphical User Interface）
= 指差し注文。メニューを見て、ボタンをクリックする。

**CLI**（Command Line Interface）
= 言葉で注文。「ホットコーヒー一つ」と打ち込む。

|  | GUI | CLI |
|---|---|---|
| 入力 | マウス（指） | キーボード（言葉） |
| 大量処理 | 苦手（1個ずつクリック） | 得意（1コマンドで何百個も） |
| 自動化 | 難しい | カンタン |
| AI との相性 | 悪い | 抜群 |

---

## 🖐 ハンズオン ①：ターミナルを開く

**Windows**（Git Bash）
1. スタートメニューを開く
2. `Git Bash` と入力（Git for Windows をインストール済みなら入っている）
3. Enter で起動

**Mac**
1. `Cmd + Space` で Spotlight を開く
2. `ターミナル` と入力
3. Enter で起動

開いたら、全員でこれを打ってください：

```bash
echo Hello
```

→ `Hello` が表示されたら成功！

<!--
講師ノート:
- Windowsは PowerShell ではなく Git Bash で統一する。理由：Git Bash なら Mac と同じ Unix コマンドがそのまま動くので、講座中に方言差を説明しなくて済む。
-->


---

<!-- _class: section -->

<p class="eyebrow">SECTION</p>
<div class="section-number">02</div>

# シェルとコマンドの基礎

---

## シェルとは

**シェル = 「あなた」と「PC」の間に立つ通訳**

あなたが日本語/コマンドで指示
　　↓
シェルが翻訳
　　↓
PC が動く

代表的なシェル：
- **bash**（Git Bash on Windows、WSL、Linux）
- **zsh**（macOS 標準）

今日は **どちらを使っても OK**。Git Bash も zsh も、入門範囲の打ち方はほぼ同じ。

> Windows ユーザーは **PowerShell ではなく Git Bash** を使ってください。
> 同じコマンドが Mac とそのまま動くので、講座中に方言を気にする必要がありません。

---

## コマンドのフォーマット — これが全ての基本

<div class="callout">

CLI で打つもの = **スペースで区切った単語の列**。
それ以上でも以下でもない。

</div>

ルールは **たった 2 つ**：

1. **一番左の単語 = コマンド名**（何をするか）
2. **それより右の単語 = 全部そのコマンドへの "追加指示"**

```
ls   -la   /Users
└┬┘  └─┬─┘  └─┬──┘
 │     │     └── 「どこの」を指定する追加指示
 │     └──────── 「どう表示するか」の追加指示（- や -- で始まる）
 └────────────── コマンド名（一覧表示せよ）
```

スペースで区切る。右側は何個並べても OK。

---

## `--help` の慣習

<div class="callout">

「このコマンド、何ができるんだっけ？」と思ったら、まず `--help` を付ける。

</div>

```bash
ls --help
git --help
python --help
```

ほぼ全てのコマンドが、慣習的に `--help` で**使い方を表示**してくれる。

→ **辞書を引くように**コマンドを学べる。
　 これを知っているだけで、未知のコマンドが怖くなくなる。

補足：
- Mac / Git Bash では `man ls` でさらに詳しいマニュアルが見られる
- 終了するときは `q` キー

---

## 🖐 ハンズオン ②：基本コマンド 5 つ + `--help`

| コマンド | 意味 | 試す |
|---|---|---|
| `pwd` | 今いる場所を表示 | `pwd` |
| `ls`  | 中身を一覧 | `ls`、`ls -la` |
| `cd`  | 場所を移動 | `cd ~` |
| `echo` | 文字を表示 | `echo Hello, World` |
| `cat` | ファイルの中身を表示 | （後で使う） |

最後に必ず：

```bash
ls --help
```

→ 大量のオプションが出てくる。**全部覚えなくていい**。
　 「ここを見ればいい」と知ることが大事。

💡 **Tab キーで補完できる**、**↑キーで履歴が出る** ことも今日中に覚える。

---

<!-- _class: section -->

<p class="eyebrow">SECTION</p>
<div class="section-number">03</div>

# ファイル・ディレクトリ操作

---

## カレントディレクトリ＝「今いる場所」

すべてのコマンドは、**カレントディレクトリ**を基準に動く。

- **カレントディレクトリ**：今あなたが立っている場所（`pwd` で確認）
- **ホームディレクトリ**：あなたの「家」
  - Windows: `C:\Users\<あなた>`
  - Mac: `/Users/<あなた>`

## ホームディレクトリの省略記号 — `~`（チルダ）

ホームのパスは長い → これを表す**特別な記号**がある：

<div class="callout">

**`~`** = ホームディレクトリ。読み方は **「チルダ」**（英語: tilde）

</div>

- `cd ~` と書けば、どこにいても**一発でホームに戻れる**
- `cd ~/Documents` のように、ホーム起点の道順も書ける
- ターミナルのプロンプトに `~` と出ていたら = 「今ホームにいる」のサイン

**絶対パスと相対パス**

- 絶対パス：`/Users/yuki/Desktop/memo.txt`（住所をフルで）
- 相対パス：`Desktop/memo.txt`（現在地からの道順）
- `.` = カレント（今ここ）／ `..` = 一つ上

---

## 🖐 ハンズオン ③：作業フォルダで CRUD

**(1) ターミナルで作業フォルダを作る**

```bash
cd ~                  # ホームに移動
mkdir cli-handson     # フォルダを作る
cd cli-handson        # 移動
pwd                   # 今ここを確認
```

**(2) テキストエディタで `memo.txt` を作る**
- メモ帳（Windows） / TextEdit（Mac） / 好きなエディタを開く
- 中身：`Hello CLI`
- 保存先：`~/cli-handson/memo.txt`

**(3) ターミナルに戻って、ファイルを操作する**

```bash
ls                    # memo.txt が見えるはず
cat memo.txt          # 中身を表示
cp memo.txt note.txt  # コピー
mv note.txt log.txt   # 名前変更（または移動）
rm log.txt            # 削除
ls
```

`mkdir` `cp` `mv` `rm` — この 4 つで**作る・複製・移動・消す**が全部できる。

---

<!-- _class: dark -->

## ⚠️ `rm` は **ゴミ箱を経由しない**

`rm` で消したファイルは、**即・完全に消える**。

- ゴミ箱に入らない
- 「ごめんやっぱ戻して」が効かない

特に危険：

```bash
rm -rf /     # ← 絶対やってはいけない。PC が死ぬ
```

<div class="callout">

**`rm` する前に必ず `ls` で確認する癖**をつける。
これは今日いちばん大事なルール。

</div>

---

<!-- _class: section -->

<p class="eyebrow">SECTION</p>
<div class="section-number">04</div>

# 探す：`find` と `grep`
## AI エージェントの心臓部

---

## `find` — 名前で探す

```bash
find . -name "memo.txt"       # カレント以下から memo.txt を探す
find ~ -name "report.txt"     # ホーム以下から report.txt を探す
```

- `.` = カレントから / `~` = ホームから
- `-name` の後ろに **探したいファイル名**
- 結果：**見つかった場所のパスが一覧で出る**

**`ls` との違い**：`ls` は「今ここだけ」、`find` は「**サブフォルダも全部**」見てくれる。

## `grep` — 中身で探す

```bash
grep "Hello" memo.txt         # memo.txt の中で "Hello" を含む行
grep -r "TODO" .              # カレント以下のファイル全てを再帰検索
grep -i "error" log.txt       # 大文字小文字を無視
grep -n "import" hello.py     # 行番号付きで表示
```

`-r` `-i` `-n` は **組み合わせ OK**：`grep -rin "todo" .`

---

## 🖐 ハンズオン ④：探す

**(1) エディタで 2 つファイルを追加**（ハンズオン③の `memo.txt` に加えて）

- `~/cli-handson/task.txt`　中身：`TODO: 後で書く`
- `~/cli-handson/greeting.txt`　中身：`Hello again`

**(2) ターミナルで探してみる**

```bash
cd ~/cli-handson

# 名前で探す（find は名前パターンを書く）
find . -name "memo.txt"
find . -name "task.txt"

# 中身で探す
grep "Hello" memo.txt
grep "Hello" greeting.txt
grep -r "TODO" .
```

---

<!-- _class: quote -->

> 今やったこれ、Claude Code が裏で動くたびに**何百回もやっています**。
> あなたは今、AI の心臓部と**まったく同じこと**をしました。

<p class="attribution">— つまり、AI が何をしているか、もうあなたは見えている</p>

---

<!-- _class: section -->

<p class="eyebrow">SECTION</p>
<div class="section-number">05</div>

# 環境変数

---

## 環境変数 = PC 全体の「設定メモ」

代表例：**`PATH`**
= "コマンドを探しに行く場所のリスト"

つまり、`ls` と打ったとき、シェルはこのリストに書かれたフォルダを順に見て、`ls` という名前の実行ファイルを探す。

**なぜ API キーは環境変数に入れるのか？**

- コードに直接書く → Git に push した瞬間に**世界に漏れる**
- 環境変数に入れる → コードはキーを知らずに使える

→ **セキュリティの基本** であり、すべてのAIサービスのキーはここに入る。

---

## 🖐 ハンズオン ⑤：`PATH` を覗く

**Windows（Git Bash）/ Mac**

```bash
echo $PATH
```

→ コロン `:` で区切られた、フォルダのリストが出てくる。

<div class="callout">

ここに含まれているフォルダの中の実行ファイルだけが、**「名前だけ」で起動できる**。

</div>

例：`python` と打って動くのは、`PATH` のどこかに `python` が置いてあるから。

<!--
講師ノート:
- PowerShell では `$env:PATH` だが、今回は Git Bash 統一なので `$PATH` でOK。
- 余裕があれば「PowerShell では `$env:PATH` という書き方になる」だけ1秒触れる。
-->


---

<!-- _class: section -->

<p class="eyebrow">SECTION</p>
<div class="section-number">06</div>

# プログラムを書いて動かす
## ★ 今日のゴール

---

## "自分で書く → 自分で動かす" のループ

今日のゴール：**このループを 1 回でも自分の手で回す**

これさえできれば、明日からは：
- AI が書いてくれたスクリプトを **動かせる**
- 動かしたスクリプトを **改造できる**
- 改造したスクリプトを **定期実行できる**

→ つまり、**AI に業務を本当に任せられる**ようになる。

事前確認：
```bash
python --version    # または py --version (Windows)
```
バージョンが表示されれば OK。

---

## 🖐 ハンズオン ⑥：`hello.py` を作って動かす

**1. テキストエディタで以下を書いて保存**（メモ帳でOK）
保存先：`~/cli-handson/hello.py`

```python
# hello.py
name = "Minedia"
print(f"Hello, {name}!")
```

**2. ターミナルで実行**

```bash
cd ~/cli-handson
python hello.py
```

**3. 表示されるはず**

```
Hello, Minedia!
```

Windows で `python` がないときは `python3` を試す（Git Bash でも同じく `python3 hello.py`）。

---

<!-- _class: dark -->

# 🎉 ゴール達成

あなたは今、

✅ ターミナルを自分で開いた
✅ コマンドの文法を覚えた
✅ ファイルを操作した
✅ ファイルと中身を探した（AI の心臓部）
✅ 環境変数を覗いた
✅ **自分で書いたプログラムを動かした**

これで、Claude Code もPython スクリプトも、もう怖くない。

---

<!-- _class: section -->

<p class="eyebrow">SECTION</p>
<div class="section-number">07</div>

# 応用デモ
## 「この先こんなことができる」

---

## デモ ① — 100 枚の画像を一括リサイズ

**Mac**
```bash
sips -Z 800 *.jpg
```

**Windows（Git Bash + ImageMagick）**
```bash
magick mogrify -resize 800x *.jpg
```

<div class="callout">

これ、GUI でやったら **2 時間**。CLI で **3 秒**。

</div>

<!--
講師ノート:
- ここで初めて `*` が出てくる。1秒だけ「これはワイルドカードという便利な記号で、"全部"の意味です。次回詳しくやります」と触れる。深入りしない。
- 受講者は打たない（見せるだけ）。
-->

---

## デモ ② — 連番ファイルを 1 コマンドで作る

```bash
for i in {1..100}; do touch "report_$(printf "%03d" $i).txt"; done
```

→ `report_001.txt` 〜 `report_100.txt` が **一瞬で**生まれる。

報告書テンプレ、テストデータ、研修用ダミーファイル...
**「100個作って」は CLI が一番得意な仕事**。

---

## デモ ③ — シェルスクリプトで自動化

```bash
#!/bin/bash
# daily_backup.sh
DATE=$(date +%Y%m%d)
cp -r ~/Documents ~/Backups/docs_$DATE
echo "Backup done: docs_$DATE"
```

これを **タスクスケジューラ（Windows）** や **cron（Mac）** に登録すれば、毎朝自動でバックアップ。

→ 「毎日朝イチでこれやる」みたいな**繰り返し作業はすべて消える**。

---

## デモ ④ — Claude Code に実務を任せる

実際に Claude Code を起動して、自然言語で指示：

> 「このフォルダの CSV を集計して、月次レポートを作って」

**裏で起きていること**（あなたが今日学んだコマンド達）：
- `ls` でフォルダ一覧
- `find` で CSV を全部探す
- `cat` / Python で中身を読む
- `grep` で必要な行を抽出
- スクリプトを書いて実行

<div class="callout">

今日学んだ CLI の土台 = そのまま AI の土台。
**あなたが分かれば、AI も分かる**。

</div>

---

<!-- _class: section -->

<p class="eyebrow">SECTION</p>
<div class="section-number">08</div>

# クロージング

---

## 明日からの 3 ステップ

**1. 業務で「5 回に 1 回」、CLI で解決できないか考える**
　 → 100ファイルのリネーム、定型レポート、ファイル整理。これ全部 CLI 案件。

**2. Claude Code を業務で使ってみる**
　 → 今日のCLI知識があれば、Claude Code の操作・出力が読める。

**3. 困ったら社内 Slack `#ai` で聞く**
　 → 「とりあえず打ってみたけど動かない」が一番上達する。

<div class="callout">

CLI は "覚える" ものではなく "慣れる" もの。
**今日のあと、明日も 1 行だけでも打つこと**。

</div>

---

<!-- _class: closing -->

# ありがとうございました

質問・要望は社内 Slack **`#ai`** まで。
資料リポジトリ：**github.com/minedia/cli-basics**
