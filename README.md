# Selectorize CSS
カスタムプロパティをセレクタとしてスタイルを適用する軽量なユーティリティCSS。

## 概要
Tailwind CSSに代表される**ユーティリティファーストなスタイリング手法**を、**HTMLの`style`属性で設定するカスタムプロパティと、それに対応するCSSの属性セレクタで実現**します。これにより、クラス名の管理を必要とせず、直感的かつ柔軟なCSSマークアップを可能にします。

## 特徴
- **ゼロビルド:**
  特別なビルドプロセスは一切不要です。純粋なCSS (Vanilla CSS) として機能します。
- **低い学習コスト:**
  HTMLの`style`属性にCSSプロパティを直接記述する感覚で利用できます。これは、多くのクラス名を覚える必要がある一般的なユーティリティファーストCSSとは異なる、より直感的で新しいスタイリングアプローチを提供します。
- **CSSコード量の最適化:**
  ウェブサイトの特定のページや要素のためにCSSを追加し続けるとコード量は肥大化しがちです。Selectorize CSSは、用意されたカスタムプロパティを通じてスタイルを適用するため、冗長なクラス定義を削減でき、CSSコード全体の増加を最小限に抑えます。
- **プロパティと値の効率的な分離:**
  一般的なユーティリティCSSによくある「`background-red`」「`border-red`」「`text-red`」のような、値ごとに重複するクラス定義の膨張を防ぎます。プロパティ (`background`, `border`, `color` など) と値 (`red`, `green`, `blue` など) をカスタムプロパティで分離することで、CSSの記述量を大幅に削減し、管理を容易にします。
- **セマンティックなHTML構造の維持:**
  HTMLの文書構造や`class`属性はセマンティックな意味付けに集中し、見た目に関する非セマンティックなスタイルは`style`属性とカスタムプロパティで管理できます。これにより、HTMLのメンテナンス性を向上させます。
- **スタイル上書きの柔軟性:**
  `style`属性に直接プロパティを設定する代わりにカスタムプロパティを使用するため、スタイルが強制的に適用されず、`!important`を使用せずにスタイルの上書きもできます。これにより、より柔軟なデザイン調整も可能です。
- **軽量性と高い拡張性:**
  必要最小限のプロパティと機能に厳選しているため、ファイルサイズは軽量です。特定のデザインコンポーネントを強制しないため、プロジェクト固有のデザインシステムや既存のCSSに柔軟に組み込むことができます。
- **多様な利用シナリオ:**
  Selectorize CSSは、ウェブページの主要なデザイン・レイアウトを直接制御する手段として利用できますが、既存のCSSやコンポーネントと組み合わせて、ボタンのバリエーション (サイズ、色など) を手軽に作成するといった、部分的なカスタマイズにも効果を発揮します。
- **シンプルな命名規則:**
  style属性に設定するプロパティ名の前後に`--`を付けるだけです。
  ```html
  <div style="--color--: var(--red, red);">…</div>
  ```
- **プレフィクスによる拡張:**
  プレフィクスを用いることで、高度なスタイリングも可能です。
  - `--gt-all_PROPERTY-NAME--:` を設定すると、その全ての子要素 (`>*`) をスタイリングします。
  - `--item_PROPERTY-NAME--:` を `ol`, `ul`, `dl`, `div`, `table`, `tbody`, `thead`, `tfoot`, `tr` に設定すると、その直近の `li`, `dt`, `dd`, `td`, `th` をスタイリングします。
  - `--dt_PROPERTY-NAME--:` を `dl`, `div` に設定すると、その直近の `dt` をスタイリングします。
  - `--dd_PROPERTY-NAME--:` を `dl`, `div` に設定すると、その直近の `dd` をスタイリングします。
  - `--before_content--:` を設定すると、その`::before`擬似要素 を追加できます。
  - `--after_content--:` を設定すると、その`::after`擬似要素 を追加できます。
  - `--mq-MEDIA-QUERY-LIST_PROPERTY-NAME--:` を設定すると、指定したメディアクエリの条件に応じてスタイリングします。
  - `--cq-CONTAINER-CONDITION_PROPERTY-NAME--:` を設定すると、指定したコンテナクエリの条件に応じてスタイリングします。

## 導入方法
1. このリポジトリから `selectorize.css` ファイルをダウンロードし、プロジェクトに配置します。
2. HTMLの`<head>`要素内で、以下のように`selectorize.css`を読み込みます。
   ```html
   <link rel="stylesheet" href="path/to/your/project/selectorize.css" />
   ```

## 使用例
次の例は、グリッドレイアウトの設定例です。240pxを基本サイズとするグリッドアイテムが並びます。
  ```html
  <ul style="--grid--: auto-flow / repeat(auto-fit, minmax(min(240px, 100%), 1fr)); --gap--: var(--space_medium, 1rem); --background--: var(--palest_gray, #e0e0e0); --item_padding--: var(--space_large, 2rem);">
    <li>…</li>
    …
  </ul>
  ```
次の例は、フレックスボックスレイアウトの設定例です。通常は縦一列、コンテナクエリ (cq) で、インラインサイズ (i) > (gt) Mサイズ (m) なら横一列に並びます。
  ```html
  <ul style="--container-type--: inline-size; --flex-flow--: wrap; --gt-all_flex--: 100%; --gap--: var(--space_medium, 1rem); --background--: var(--palest_gray, #e0e0e0); --item_padding--: var(--space_large, 2rem);">
    <li style="--cq-i-gt-m_flex--: 1 0 0%;">…</li>
    …
  </ul>
  ```
次の例は、buttonクラスのスタイルに背景色と文字色を追加しています。
  ```html
  <p style="--text-align--: center;">
    <button type="button" class="button" style="--background--: var(--red, red); --color--: var(--white, white);">
      …
    </button>
  </p>
  ```
`var(--red, red)`のようにフォールバック値を設定することで、`--red`が定義されていなくても、デフォルトで赤色が適用されます。

## 貢献
バグ報告や機能提案は、GitHubのIssuesを通じて歓迎します。
コードの貢献にご興味があれば、プルリクエストをお送りください。

## ライセンス
このプロジェクトは [GPL-2.0 License](https://www.gnu.org/licenses/gpl-2.0.html) の下で公開されています。
詳細については、`LICENSE` ファイルを参照してください。
