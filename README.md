# CLI オンボーディング登壇資料

[![Build slides](https://github.com/minedia/cli-onboarding/actions/workflows/release.yml/badge.svg)](https://github.com/minedia/cli-onboarding/actions/workflows/release.yml)
![Windows](https://img.shields.io/badge/Windows-Git_Bash-0078D4?logo=windows&logoColor=white)
![macOS](https://img.shields.io/badge/macOS-Terminal-000000?logo=apple&logoColor=white)

Minedia社員向け（社外公開可）の、CLI / ターミナルまわりのオンボーディング登壇資料シリーズです。
1テーマ = 1デッキで独立しており、今後トピックを追加していきます。

各デッキの内容は、下表「詳細」列の各デッキ README を参照してください。
完成版スライドは [GitHub Releases](https://github.com/minedia/cli-onboarding/releases/latest) からダウンロードできます。

## デッキ一覧

| デッキ | テーマ | 所要 | 状態 | 詳細 |
|--------|--------|------|------|------|
| `cli-basics` | AI時代のコマンドライン入門 | 60分 | ✅ 公開中 | [概要](decks/cli-basics/README.md) |
| _（追加予定）_ | — | — | 🚧 | — |

> シリーズとして5本程度を予定しています。新しいデッキを追加したら、この表に1行追記してください。

---

## リポジトリ構成

```
.
├── README.md                  # このファイル（シリーズ index）
├── decks/                     # デッキ置き場。1ディレクトリ = 1デッキ（自己完結）
│   └── cli-basics/
│       ├── slides.md          # 本体（Marp Markdown）
│       ├── outline.md         # 講師用タイムテーブル
│       ├── README.md          # このデッキ固有の概要・カリキュラム・ビルド
│       ├── themes/minedia.css # Minedia design system を移植した Marp テーマ
│       └── assets/            # ロゴ・イラスト
├── .github/workflows/release.yml  # 全デッキを自動ビルド → 単一リリース
└── docs/                      # 設計ドキュメント等
```

各デッキは **テーマ・アセットを同梱した自己完結ユニット**です。他デッキへの依存はありません。

---

## 新しいデッキを追加する

ディレクトリを1つ足すだけです。CI が自動検出します（ワークフローの変更は不要）。

```bash
# 既存デッキを雛形にコピーするのが速い
cp -r decks/cli-basics decks/<新しいslug>

# 中身を差し替える
#   - decks/<新しいslug>/slides.md   … 本文を書き換え
#   - decks/<新しいslug>/README.md   … 概要を書き換え
#   - decks/<新しいslug>/outline.md  … 任意
#   - themes/ assets/                … 必要に応じて差し替え（テーマは各デッキに複製）
```

最後に、上の「デッキ一覧」表に1行追記してください。

`main` に push すると、新デッキも含めた全デッキがビルドされ、`<新しいslug>-slides.{pdf,pptx,html}` がリリースに同梱されます。

---

## ローカルでビルドする

### 前提

- [Node.js](https://nodejs.org/) 18 以上
- Marp CLI: `npm install -g @marp-team/marp-cli`

### ビルドコマンド

**⚠️ 必ず対象デッキのディレクトリに移動してから実行してください。**
`cd` を忘れると `slides.md` も `themes/minedia.css` も見つからずエラーになります。

```bash
cd decks/cli-basics   # ← ビルドしたいデッキへ

# PDF（印刷・配布用）
marp slides.md --theme themes/minedia.css --pdf  --allow-local-files -o cli-basics-slides.pdf

# PPTX（PowerPoint 版）
marp slides.md --theme themes/minedia.css --pptx --allow-local-files -o cli-basics-slides.pptx

# HTML（ブラウザ版）
marp slides.md --theme themes/minedia.css --html --allow-local-files -o cli-basics-slides.html

# プレビュー（ライブリロード付き）
marp slides.md --theme themes/minedia.css --server
```

> macOS / Linux ではシステムフォントで日本語が表示されます。
> CI 環境（Ubuntu）では `fonts-noto-cjk` を自動インストールしています。
> ロゴ画像が表示されない時は `--allow-local-files` を付け忘れていないか確認してください。

---

## CI / 自動リリース

`main` の `decks/` が更新されると、**全デッキを自動ビルドし、バージョンを自動採番してリリース**します。

ワークフローは3ジョブ構成です。

1. **discover** — `decks/*/slides.md` を走査し、ビルド対象のデッキ一覧を自動検出
2. **build** — デッキごとに並列で PDF / PPTX / HTML を生成
3. **release** — 全成果物をまとめ、直近タグのパッチを +1 した新バージョンで GitHub Release を作成

| トリガー | 動作 |
|---|---|
| `main` への push（`decks/` 変更時） | 全デッキをビルド → 直近タグのパッチを +1 した新バージョン（例: `v0.0.5` → `v0.0.6`）でタグ＋ Release を自動作成 |
| 手動実行（Actions → Run workflow） | `version` を指定すればその版でリリース（minor / major 上げ用）。空なら自動採番 |

> パッチ以外（minor / major）を上げたいときだけ、Actions タブから手動実行して `version`（例: `v0.1.0`）を指定してください。

---

## 制作環境

- **作成ツール**: [Claude Code](https://www.anthropic.com/claude-code)
- **スライド**: [Marp](https://marp.app/) — Markdown → PDF / PPTX / HTML
- **CI / 配布**: GitHub Actions
- **デザイン**: Minedia Design System

---

## ライセンス

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

本リポジトリの教材（スライド・図版・ドキュメント）は [クリエイティブ・コモンズ 表示 4.0 国際 (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/deed.ja) の下で公開しています。
クレジット（© 株式会社マインディア）を明示すれば、商用・非商用を問わず、複製・改変・再配布が可能です。

全文は [`LICENSE`](LICENSE) を参照してください。
