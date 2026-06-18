# Claude Code ハッカソン 〜手元の業務を Claude Code で効率化する体験ワークショップ〜

> [CLI オンボーディング登壇資料シリーズ](../../README.md) の1デッキ（`claude-code-hackathon`）です。

Biz（非エンジニア）メンバー向けの、Claude Code 導入＆業務効率化ハンズオンです。
インストールからウォームアップ、ユースケースデモ、各種ハンズオン Lab、Skills、
参加者向け Q&A、ファシリテーター運営ガイドまでを **1 本のスライド（全 280 枚）** にまとめています。

完成版スライド（PDF / PPTX / HTML）は [GitHub Releases](https://github.com/minedia/cli-basics/releases/latest) からダウンロードできます。

---

## 対象・ゴール

| 項目 | 内容 |
|------|------|
| 対象 | Biz（非エンジニア）メンバー |
| 環境 | Windows PC |
| ファシリテーター | AI に詳しいエンジニア |
| ゴール | Claude Code を導入し、手元の業務を効率化する体験を提供 |

ターミナルに日本語で指示するだけ。プログラミングの知識は一切不要です。

---

## 収録セクション（全 280 枚）

| # | セクション | フッター表示 |
|---|-----------|-------------|
| — | 目次・ワークショップ概要 | `目次 ·` |
| 1 | Claude Code とは？ | `01 ·` |
| 2 | インストール & セットアップ | `02 ·` |
| 3 | ウォームアップ体験 | `03 ·` |
| 4 | ユースケースデモ（A〜G） | `04 ·` |
| 5 | ハンズオン: 自分の業務を効率化 | `05 ·` |
| 6 | Skills で更なる効率化 | `06 ·` |
| Lab | 売上ダッシュボードを作る | `Lab ·` |
| Lab | 見積書ジェネレーターを作る | `Lab ·` |
| Lab | Excel 自動レポートを作る | `Lab ·` |
| Lab | Web 情報を収集・分析する | `Lab ·` |
| 番外編 | 開発環境セットアップ | `番外編 ·` |
| 参考 | 参加者向け Q&A | `参考 ·` |
| 参考 | Claude × Office 活用 Tips | `参考 ·` |
| 運営 | ファシリテーターガイド | `ファシリテーター ·` |
| 運営 | トラブルシューティング | `ファシリテーター ·` |
| 運営 | クイックコマンド集 | `ファシリテーター ·` |

各セクションの先頭は表紙（濃紺グラデの扉）スライドになっており、`<!-- footer: '...' -->`
ディレクティブでセクションごとにフッター表示が切り替わります。

---

## このデッキの構成

```
decks/claude-code-hackathon/
├── slides.md            # 本体（Marp Markdown・全280枚を統合）
├── README.md            # このファイル
├── AUTHORING-GUIDE.md   # スライド分割・テーマクラスの執筆ルール
└── themes/
    └── hackathon.css    # 元 Astro ドキュメントサイトのデザインを移植した Marp テーマ
```

> 元データは Astro 製ドキュメントサイト（16 ページ）でした。Marp 化にあたり、
> 1 ページ＝1 セクションとして 1 本の `slides.md` に統合しています。
> スライドの分割方針やテーマクラスの使い方は [`AUTHORING-GUIDE.md`](AUTHORING-GUIDE.md) を参照してください。

---

## ビルド方法

> **⚠️ 必ずこのディレクトリ（`decks/claude-code-hackathon`）に移動してから実行してください。**
>
> このデッキのテーマは `hackathon`（`themes/hackathon.css`）です。テーマファイルを直接指定する
> `--theme` ではなく、ディレクトリごと登録する **`--theme-set themes/`** を使ってください
> （`slides.md` の frontmatter の `theme: hackathon` で実テーマが選択されます）。

### 0. Marp CLI を入れる

```bash
npm install -g @marp-team/marp-cli
# または npx で都度実行: npx @marp-team/marp-cli@latest --version
```

### 1. プレビュー（ホットリロード付き）

```bash
cd decks/claude-code-hackathon
marp slides.md --theme-set themes/ --watch --preview --html
```

### 2. PDF に変換（全 280 枚が 1 冊になる ＝ 一括PDF）

```bash
cd decks/claude-code-hackathon
marp slides.md --theme-set themes/ --pdf --allow-local-files -o claude-code-hackathon-slides.pdf
```

### 3. HTML / PPTX に変換

```bash
cd decks/claude-code-hackathon
marp slides.md --theme-set themes/ --html --allow-local-files -o claude-code-hackathon-slides.html
marp slides.md --theme-set themes/ --pptx --allow-local-files -o claude-code-hackathon-slides.pptx
```

> macOS / Linux ではシステムフォント、CI（Ubuntu）では `fonts-noto-cjk` で日本語が表示されます。
> テーマの font-family には `Noto Sans CJK JP` をフォールバックに含めてあります。

---

## CI での自動ビルド

`main` の `decks/` を更新すると、リポジトリの
[`.github/workflows/release.yml`](../../.github/workflows/release.yml) が
このデッキを自動検出し、**全 280 枚を 1 つに統合した PDF / PPTX / HTML**
（`claude-code-hackathon-slides.{pdf,pptx,html}`）をビルドして、シリーズの
リリース zip に同梱します。ワークフロー側の変更は不要です。

---

## デザイン

`themes/hackathon.css` は元サイトのデザイントークンを Marp 用に移植したものです。

| 要素 | 値 |
|------|----|
| 本文テキスト | navy `#1a1a2e` |
| 見出し・リンク・強調 | accent `#003366` |
| コードブロック背景 | `#1e293b` |

カスタムクラス（`<!-- _class: ... -->` で指定）:

| クラス | 用途 |
|---|---|
| `lead` | 表紙・セクション扉（濃紺グラデ背景・白文字） |
| `section` | 章の区切り扉（濃紺背景） |
| `compact` / `dense` | 情報量の多いスライド・大きな表向けに余白とフォントを圧縮 |
