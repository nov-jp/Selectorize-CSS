[English](README.md) | [Deutsch](README.de.md) | [Espanol](README.es.md) | [Francais](README.fr.md) | [日本語](README.ja.md) | [Русский](README.ru.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md)

-----

# Selectorize CSS

カスタムプロパティをセレクタとして利用した、軽量でシンプルなユーティリティCSS。

嫌われがちな`style`属性を救済し、直感的でパワフルなCSSマークアップを実現します。

-----

## 概要

Tailwind CSSに代表されるユーティリティファーストなスタイリング手法を、HTMLの`style`属性に設定するカスタムプロパティと、それに対応するCSSの属性セレクタで実現します。これにより、クラス名の管理を必要とせず、直感的かつ柔軟なCSSマークアップを可能にします。

-----

## 特徴

* **ゼロビルド:**
  特別なビルドプロセスは一切不要です。純粋なCSS (Vanilla CSS) です。
* **シンプルな命名規則による低い学習コスト:**
  HTMLの`style`属性に設定するプロパティ名の前後に`--`を付けるだけで利用できます。多くのクラス名を覚える必要がある一般的なユーティリティファーストCSSとは異なる、より直感的で新しいスタイリングアプローチを提供します。
  ```html
  <div style="--color--: crimson;"> … </div>
  ```
* **軽量性と高い拡張性:**
  ミニマルな設計により、ファイルサイズは軽量です。特定のデザインコンポーネントを強制しないため、プロジェクト固有のデザインシステムや既存のCSSに柔軟に組み込むことができます。
  ```html
  <!-- Selectorize CSS + [Open Props](https://open-props.style/) -->
  <div style="--border--: solid var(--border-size-1) var(--gray-1);"> … </div>
  ```
* **CSSコード量の最適化:**
  ウェブサイトの特定のページや要素のためにCSSを追加し続けるとコード量は肥大化しがちです。Selectorize CSSは、用意されたカスタムプロパティを通じてスタイルを適用するため、冗長なクラス定義を削減でき、CSSコード全体の増加を最小限に抑えます。
  ```html
  <!-- 一般的な方法 -->
  <style>
  .very-unique-grid-1 { display: grid; grid: … ; … }
  .very-unique-grid-2 { display: grid; grid: … ; … }
  …
  </style>
  …
  <div class="very-unique-grid-1"> … </div>
  <div class="very-unique-grid-2"> … </div>
  …
  
  <!-- Selectorize CSS -->
  <div style="--grid--: … ;"> … </div>
  <div style="--grid--: … ;"> … </div>
  ```
* **プロパティと値の効率的な分離:**
  一般的なユーティリティCSSによくある「`bg-red`」「`border-red`」「`text-red`」のようなクラス定義の膨張を防ぎます。プロパティ (`background`, `border-color`, `color` など) と値 (`red`, `green`, `blue` など) を分離することで、CSSの記述量を大幅に削減し、管理を容易にします。
  ```css
  /* 一般的な方法 (<div class="background-pale-red border-red text-red"> … </div>) */
  .background-red { background: crimson; }
  .background-pale-red { background: mistyrose; }
  …
  .border-red { border-color: crimson; }
  .border-pale-red { border-color: mistyrose; }
  …
  .text-red { color: crimson; }
  .text-pale-red { color: mistyrose; }
  …
  
  /* Selectorize CSS (<div style="--background--: mistyrose; --border-color--: crimson; --color--: crimson;"> … </div>) */
  [style~="--background--:"] { background: var(--background--); }
  [style~="--border-color--:"] { border-color: var(--border-color--); }
  [style~="--color--:"] { color: var(--color--); }
  ```
* **セマンティックなHTML構造の維持:**
  HTMLの文書構造や`class`属性はセマンティックな意味付けに集中し、見た目に関する非セマンティックなスタイルは`style`属性とカスタムプロパティで管理できます。これにより、HTMLのメンテナンス性を向上させます。
  ```html
  <!-- 一般的な方法 -->
  <div class="important text-red text-bolder align-center"> … </div>
  
  <!-- Selectorize CSS -->
  <div class="important" style="--color--: crimson; --font-weight--: bolder; --text-align--: center;"> … </div>
  ```
* **上書きできる柔軟性:**
  プロパティの代わりにカスタムプロパティを`style`属性に設定するため、スタイルが強制的に適用されず、`!important`を使用しなくてもスタイルの上書きができます。これにより、柔軟なデザイン調整も可能です。
  ```css
  /* 一般的な方法 (<div class="example" style="color: goldenrod;"> … </div>) */
  .example { color: crimson !important; }
  
  /* Selectorize CSS (<div class="example" style="--color--: goldenrod;"> … </div>) */
  .example { color: crimson; } /* goldenrod を crimson に変更する例 */
  .example { --color--: crimson; color: var(--color--); } /* 初期値を crimson にして`style`属性の`--color--`で上書き可能にする例 */
  ```
* **多様な利用シナリオ:**
  Selectorize CSSは、ウェブページの主要なデザイン・レイアウトを直接実装する手段として利用できますが、既存のCSSやコンポーネントと組み合わせて、ボタンの色やサイズなどのバリエーションを手軽に作成するといった、部分的なカスタマイズにも効果を発揮します。
  ```html
  <!-- 12分割グリッドレイアウトの実装 -->
  <div style="--grid--: auto-flow / repeat(12, 1fr); --gap--: 1rem;">
    <div style="--grid-area--: auto / span 2;"> … </div>
    <div style="--grid-area--: auto / span 4;"> … </div>
    <div style="--grid-area--: auto / span 6;"> … </div>
  </div>

  <!-- ボタンの部分的なカスタマイズ -->
  <p style="--text-align--: center;">
    <button class="button" style="--background--: royalblue; --color--: white; --min-inline-size--: calc(100% / 3);"> … </button>
  </p>
  ```
* **プレフィクスによる拡張:**
  プレフィクスを用いることで、高度なスタイリングも可能です。
  * `--gt-all_PROPERTY-NAME--:` のように設定すると、子要素 (`>*`) にスタイルを適用します。
    ```html
    <ul style="--flex-flow--: wrap; --gt-all_flex--: auto;"> … </ul>
    ```
  * `--item_PROPERTY-NAME--:` を `ol`, `ul`, `dl`, `div`, `table`, `tbody`, `thead`, `tfoot`, `tr` に設定すると、直近の `li`, `dt`, `dd`, `td`, `th` にスタイルを適用します。
    ```html
    <table style="--item_border--: solid thin; --item_padding--: 0.5rem;"> … </table>
    ```
  * `--dt_PROPERTY-NAME--:` を `dl`, `div` に設定すると、直近の `dt` にスタイルを適用します。
    ```html
    <dl style="--flex-flow--: wrap; --dt_flex--: 100%;">
      <dt> … </dt>
      <dd> … </dd>
      <dd> … </dd>
      …
    </dl>
    ```
  * `--dd_PROPERTY-NAME--:` を `dl`, `div` に設定すると、直近の `dd` にスタイルを適用します。
    ```html
    <dl style="--flex-flow--: wrap; --dd_flex--: 100%;">
      <dt> … </dt>
      <dt> … </dt>
      <dd> … </dd>
      …
    </dl>
    ```
  * `--before_content--:` を設定すると、`::before`擬似要素を追加できます。
    ```html
    <p style="--before_content--: '👍';"> … </p>
    ```
  * `--after_content--:` を設定すると、`::after`擬似要素を追加できます。
    ```html
    <p style="--after_content--: '😀';"> … </p>
    ```
  * `--cq-CONTAINER-CONDITION_PROPERTY-NAME--:` を設定すると、指定したコンテナクエリの条件に応じてスタイルを適用します。`--container-type--`を祖先要素に設定することも忘れずに。
    ```html
    <ul style="--container-type--: inline-size; --flex-flow--: wrap; --gt-all_flex--: 100%; --gap--: 1rem; --item_background--: ghostwhite; --item_padding--: 1rem;">
      <li style="--cq-i-gt-m_flex--: 1 0 0%;"> … </li>
      …
    </ul>
    ```

Selectorize CSSはとてもミニマルに設計されているので、まずはCSSコードを見ていただき、何ができるか想像してみてください。

-----

## 導入方法

1. このリポジトリから `selectorize.css` ファイルをダウンロードし、プロジェクトに配置します。
2. HTMLの`<head>`要素内で、以下のように`selectorize.css`を読み込みます。他のCSSファイルよりも先に読み込むことをお勧めします。
   ```html
   <link rel="stylesheet" href="path/to/your/project/selectorize.css" />
   ```

-----

## 貢献

バグ報告や機能提案は、GitHubのIssuesを通じて歓迎します。
コードの貢献にご興味があれば、プルリクエストをお送りください。

-----

## ライセンス

このプロジェクトは [GPL-2.0 License](https://www.gnu.org/licenses/gpl-2.0.html) の下で公開されています。
詳細については、`LICENSE` ファイルを参照してください。
