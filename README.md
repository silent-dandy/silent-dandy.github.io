# silent-dandy.github.io

Silent Comfort の GitHub Pages https://silent-dandy.github.io/

| パス | 内容 |
|---|---|
| `index.html` | ポータル（World Nadenade とジェネレーターの入口） |
| `assets/style.css` | 全ページ共通のスタイル |
| `generator/` | なでなで・ASMR音ジェネレーター（説明・利用規約・本体・設定例）。Jekyll の変換対象外で、そのまま配信 |
| `world-nadenade/*.md` | World Nadenade のワールド制作者向けマニュアル（Markdown。Jekyll が `_layouts/manual.html` で HTML にする） |
| `_data/nadenade_nav.yml` | マニュアルの目次。ページを足したらここにも追加する |

## マニュアルのページを足す

1. `world-nadenade/<名前>.md` を作り、先頭に front matter を書く（レイアウトは `_config.yml` で自動指定）

   ```
   ---
   title: ページの見出し
   description: 検索結果などに出る説明（任意）
   ---
   ```

2. `_data/nadenade_nav.yml` に `title` と `url`（`/world-nadenade/<名前>.html`）を追加する

下書きの注意書きは、引用の直後に `{: .note-draft}` を付けると黄色の枠になる。

## 権利について

このリポジトリのコード・文章・設定ファイルの権利は Silent Comfort にあります（オープンソースではありません）。
ジェネレーターで書き出した音の扱いは [利用規約](https://silent-dandy.github.io/generator/terms.html) をご覧ください。
