# slides/

Marpで書かれた CLI 入門講座スライド。

## 構成

```
slides/
├── slides.md          # 本体（Marp Markdown）
├── themes/
│   └── minedia.css    # Minedia design system を移植した Marp テーマ
├── assets/
│   └── text_logo.png  # 右下に表示する Minedia ロゴ
└── README.md          # このファイル
```

## ビルド方法

### 0. Marp CLI を入れる

```bash
# npm
npm install -g @marp-team/marp-cli

# または npx で都度実行
npx @marp-team/marp-cli@latest --version
```

### 1. プレビュー（ホットリロード付き）

```bash
cd slides
marp slides.md --theme themes/minedia.css --watch --preview --html
```

### 2. PDF に変換

```bash
cd slides
marp slides.md --theme themes/minedia.css --pdf --allow-local-files
```

→ `slides.pdf` が出力される。

### 3. HTML に変換（社外公開・配布用）

```bash
cd slides
marp slides.md --theme themes/minedia.css --html --allow-local-files
```

→ `slides.html` が単一ファイルで出力される。

### 4. PPTX に変換（PowerPoint で開く）

```bash
cd slides
marp slides.md --theme themes/minedia.css --pptx --allow-local-files
```

→ `slides.pptx` が出力される（編集可能なPPTXではなく画像化されたスライドになる点に注意）。

### 5. PNG 連番に変換（サムネイル・SNS用）

```bash
cd slides
marp slides.md --theme themes/minedia.css --images png --allow-local-files
```

## ロゴ画像が表示されない時

`--allow-local-files` フラグが必須。ローカル PNG への参照を明示的に許可する。

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

## VS Code で書く場合

[Marp for VS Code](https://marketplace.visualstudio.com/items?itemName=marp-team.marp-vscode) 拡張を入れると、エディタ右側にリアルタイムプレビューが出る。

`.vscode/settings.json`:

```json
{
  "markdown.marp.themes": ["./slides/themes/minedia.css"]
}
```
