# 設計: 登壇資料リポジトリのシリーズ化（cli-onboarding）

- 日付: 2026-06-17
- 対象リポジトリ: `minedia/cli-basics` → `minedia/cli-onboarding` にリネーム
- ステータス: 承認済み

## 背景と目的

現状、このリポジトリには登壇資料が1本だけ存在する（「AI時代のコマンドライン入門」）。
今後、CLI / ターミナル系のオンボーディング教材を **独立トピックの集まり** として5本程度シリーズ化していく。

現行構成は単一デッキ前提で、`slides/` 直下に1デッキ分の `slides.md` / テーマ / アセットが置かれ、
CI も `slides/` 固定でビルドしている。このままでは2本目以降を追加できない。

本設計のゴールは、**デッキを1つ追加するときに「ディレクトリを1つ足すだけ」で済む** 構成へ再編すること。

## 決定事項（ブレストで確定）

1. **シリーズの性質: 独立トピック集**
   各デッキは順序関係を持たない独立テーマ。連番ではなく slug 名ディレクトリで管理する。
2. **共有資源: 各デッキに複製**
   テーマ（`minedia.css`）とロゴは各デッキ配下に複製し、デッキを完全自己完結にする。
   `minedia.css` 更新時は全デッキへ反映が必要になるトレードオフを許容する。
3. **CI/リリース: 全デッキを matrix ビルド → 単一リリース**
   main push ごとに全デッキをビルドし、1つの GitHub Release に全デッキの成果物を同梱する。
   無関係な更新でも全デッキ再ビルドになるトレードオフを許容する。
4. **リポジトリ名: `cli-onboarding` にリネーム**
   GitHub 上のリネームも実行し、README バッジ/URL と release.yml の参照を更新する。
5. **既存デッキの slug: `cli-basics`**
   リポジトリ名が `cli-onboarding` になるため `decks/cli-basics/` で名前重複は起きない。
   成果物名 `cli-basics-slides.{pdf,pptx,html}` は据え置き（slug 基準のため配布リンクの継続性が保たれる）。

## 目標構成

```
.
├── README.md                        # シリーズ index（デッキ一覧 + 共通ビルド/CI 説明）
├── decks/
│   └── cli-basics/                  # 既存デッキを集約した自己完結ユニット
│       ├── slides.md
│       ├── outline.md               # 講師用タイムテーブル（root から移動）
│       ├── README.md                # このデッキ固有の概要・カリキュラム
│       ├── themes/
│       │   └── minedia.css          # テーマ（各デッキに複製）
│       └── assets/
│           ├── text_logo.png
│           └── illustrations/*.svg
├── .github/
│   └── workflows/
│       └── release.yml              # discover → matrix build → 単一リリース
├── docs/
│   └── superpowers/specs/           # 設計ドキュメント
└── .gitignore                       # decks/**/*.{pdf,pptx,html,png} を無視
```

**デッキ追加の手順 = `decks/<新slug>/` に `slides.md` + `themes/` + `assets/` を置くだけ。**
CI が自動検出するため、ワークフローや設定の変更は不要。これがスケールの肝。

## コンポーネント

### 1. `decks/<slug>/` 自己完結ユニット

- 1デッキ = 1ディレクトリ。`slides.md`・テーマ・アセット・README・outline を全て同梱する。
- 他デッキへの依存ゼロ。単独でコピー・切り出しが可能。
- 各デッキの README には、そのデッキ固有の情報（対象者/ゴール/カリキュラム/事前準備/参考資料）を置く。
- ビルドは従来どおり `cd decks/<slug>` してから `marp slides.md --theme themes/minedia.css ...` を実行する。

### 2. CI ワークフロー（`.github/workflows/release.yml`）3ジョブ構成

- **discover**: `decks/*/slides.md` を走査し、slug の配列を JSON で出力（matrix の入力にする）。
- **build**: `strategy.matrix.deck` で slug を回し、各デッキを PDF / PPTX / HTML へ変換。
  出力名は `<slug>-slides.{pdf,pptx,html}`。デッキごとに artifact をアップロードする。
- **release**: 全 artifact をダウンロードし、既存のパッチ自動採番ロジック（直近タグの patch を +1）で
  単一の GitHub Release を作成。全デッキの成果物を同梱する。
  → 1リリース = その時点の全デッキ完全セット。
- トリガー: `push` の paths を `slides/**` → `decks/**` に変更。`workflow_dispatch` の手動バージョン指定は維持。

### 3. README 2層化

- **root `README.md`**: シリーズ概要 + デッキ一覧テーブル（タイトル / 所要時間 / 状態 / 各 deck README へのリンク）
  + 共通のローカルビルド方法 + CI / 自動リリースの説明 + 制作環境 / ライセンス。
- **`decks/cli-basics/README.md`**: 現 root README の講座固有部分
  （なぜこの講座をやるのか / 対象者 / ゴール / 開催概要 / 事前準備 / カリキュラム / 参考資料）。

### 4. リポジトリリネーム

- `gh repo rename cli-onboarding` を実行。
- ローカルの git remote URL を `minedia/cli-onboarding` に更新。
- README のバッジ URL・各種リンク、release.yml のリリースタイトル中の参照を更新。
- 旧 URL は GitHub が自動リダイレクトするため、外部リンクは当面壊れない。
- ローカルの ghq ディレクトリパス（`.../minedia/cli-basics`）の移動は、作業中シェルへの影響があるため
  本作業後に手動で行う（任意）。

## 移行方針

- `git mv` で履歴を保持しながら移動する。
  - `slides/` → `decks/cli-basics/`
  - root `outline.md` → `decks/cli-basics/outline.md`
- `.gitignore` の Marp ビルド出力パスを `slides/*.{html,pdf,pptx,png}` → `decks/**/*.{html,pdf,pptx,png}` に更新。
- root README を分割し、講座固有部分を `decks/cli-basics/README.md` へ移す。
- `slides/README.md` の内容（テーマ仕様・ビルド詳細）は `decks/cli-basics/README.md` に統合、
  または共通部分を root README に寄せる。

## 検証

- CI: 再編後に main へ反映し、Actions が discover → matrix build（cli-basics 1デッキ）→ 単一リリースまで
  成功すること。成果物名が `cli-basics-slides.{pdf,pptx,html}` であること。
- ローカルビルド: `cd decks/cli-basics && marp slides.md --theme themes/minedia.css --pdf --allow-local-files`
  でロゴ・イラスト・テーマが正しく出力されること（相対パス崩れがないこと）。
- ダミー2デッキ目（`decks/_smoke/` など）を一時追加して matrix が複数ジョブに分岐することを確認し、
  検証後に削除する（任意）。

## スコープ外

- 2本目以降の実コンテンツ作成。
- `handson/` `examples/`（現 README に「予定」とあるが、デッキ自己完結方針では各 deck 配下に置けるため、
  必要になった時点で `decks/<slug>/handson/` 等として追加する）。
- ライセンスの確定。
