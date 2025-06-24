[日本語](README.md) | [Deutsch](README.de.md) | [English](README.en.md) | [Espanol](README.es.md) | [Francais](README.fr.md) | [Русский](README.ru.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md)

> **備註：** 本 `README` 由 [ChatGPT](https://chatgpt.com/) 從日文翻譯而來，敬請見諒。

---

# Selectorize CSS

一個利用自訂屬性作為選擇器的輕量且簡潔的實用工具 CSS。

它拯救了常被嫌棄的 `style` 屬性，實現了直覺且強大的 CSS 標記。

---

## 概述

Selectorize CSS 透過在 HTML 的 `style` 屬性中設定自訂屬性，並搭配相對應的 CSS 屬性選擇器，實現以 Tailwind CSS 為代表的實用工具優先（utility-first）樣式方法。此方式無需管理類別名稱，實現直覺且靈活的 CSS 標記。

---

## 特點

* **零建置：**
  無需任何特殊建置流程，純粹的 CSS（Vanilla CSS）。

* **簡單的命名規則，學習成本低：**
  只要在 HTML `style` 屬性中設定屬性名稱，前後加上 `--` 即可使用。區別於需記憶大量類別名稱的一般實用工具 CSS，提供更直覺且全新的樣式方法。

  ```html
  <div style="--color--: crimson;"> … </div>
  ```

* **輕量且高度擴充性：**
  設計簡潔，檔案大小輕巧。不強制特定設計元件，能靈活整合至專案特有設計系統或既有 CSS。

  ```html
  <!-- Selectorize CSS + [Open Props](https://open-props.style/) -->
  <div style="--border--: solid var(--border-size-1) var(--gray-1);"> … </div>
  ```

* **優化 CSS 程式碼量：**
  網站特定頁面或元素的 CSS 程式碼容易膨脹。Selectorize CSS 透過提供的自訂屬性套用樣式，減少冗餘類別定義，最大限度控制整體 CSS 程式碼增長。

  ```html
  <!-- 一般方式 -->
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
  …
  ```

* **屬性與值的高效分離：**
  避免了實用工具 CSS 中常見的類別名稱膨脹，例如 `bg-red`、`border-red`、`text-red`。透過將屬性（如 `background`、`border-color`、`color`）與值（如 `red`、`green`、`blue`）分離，大幅減少 CSS 程式碼量，易於管理。

  ```css
  /* 一般方式 (<div class="background-pale-red border-red text-red"> … </div>) */
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

* **維持語意化 HTML 結構：**
  HTML 的文件結構與 `class` 屬性專注於語意表達，與外觀相關的非語意樣式由 `style` 屬性及自訂屬性管理，提升 HTML 維護性。

  ```html
  <!-- 一般方式 -->
  <div class="important text-red text-bolder align-center"> … </div>

  <!-- Selectorize CSS -->
  <div class="important" style="--color--: crimson; --font-weight--: bolder; --text-align--: center;"> … </div>
  ```

* **靈活的覆蓋能力：**
  由於樣式寫在 `style` 屬性的自訂屬性上，不會被強制套用，無需使用 `!important`，方便樣式覆蓋與調整。

  ```css
  /* 一般方式 (<div class="example" style="color: goldenrod;"> … </div>) */
  .example { color: crimson !important; }

  /* Selectorize CSS (<div class="example" style="--color--: goldenrod;"> … </div>) */
  .example { color: crimson; } /* 範例：將 goldenrod 修改為 crimson */
  .example { --color--: crimson; color: var(--color--); } /* 初始值為 crimson，可用 `style` 屬性的 `--color--` 覆蓋 */
  ```

* **多元的使用場景：**
  Selectorize CSS 可用於網頁主要設計版面直接實作，也可搭配既有 CSS 或元件，輕鬆製作按鈕顏色、尺寸等局部定制。

  ```html
  <!-- 12欄網格版面 -->
  <div style="--grid--: auto-flow / repeat(12, 1fr); --gap--: 1rem;">
    <div style="--grid-area--: auto / span 2;"> … </div>
    <div style="--grid-area--: auto / span 4;"> … </div>
    <div style="--grid-area--: auto / span 6;"> … </div>
  </div>

  <!-- 按鈕局部定制 -->
  <p style="--text-align--: center;">
    <button class="button" style="--background--: royalblue; --color--: white; --min-inline-size--: calc(100% / 3);"> … </button>
  </p>
  ```

* **透過前綴擴充功能：**

  * 使用 `--gt-all_PROPERTY-NAME--:` 可將樣式套用至所有子元素（`>*`）。

    ```html
    <ul style="--flex-flow--: wrap; --gt-all_flex--: auto;"> … </ul>
    ```
  * 在 `ol`, `ul`, `dl`, `div`, `table`, `tbody`, `thead`, `tfoot`, `tr` 設定 `--item_PROPERTY-NAME--:`，樣式套用於對應的 `li`, `dt`, `dd`, `td`, `th`。

    ```html
    <table style="--item_border--: solid thin; --item_padding--: 0.5rem;"> … </table>
    ```
  * 在 `dl`, `div` 設定 `--dt_PROPERTY-NAME--:`，樣式套用於最近的 `dt`。

    ```html
    <dl style="--flex-flow--: wrap; --dt_flex--: 100%;">
      <dt> … </dt>
      <dd> … </dd>
      <dd> … </dd>
      …
    </dl>
    ```
  * 在 `dl`, `div` 設定 `--dd_PROPERTY-NAME--:`，樣式套用於最近的 `dd`。

    ```html
    <dl style="--flex-flow--: wrap; --dd_flex--: 100%;">
      <dt> … </dt>
      <dt> … </dt>
      <dd> … </dd>
      …
    </dl>
    ```
  * 設定 `--before_content--:` 可插入 `::before` 偽元素。

    ```html
    <p style="--before_content--: '👍';"> … </p>
    ```
  * 設定 `--after_content--:` 可插入 `::after` 偽元素。

    ```html
    <p style="--after_content--: '😀';"> … </p>
    ```
  * 設定 `--cq-CONTAINER-CONDITION_PROPERTY-NAME--:`，可依指定的容器查詢條件套用樣式。別忘了在祖先元素設定 `--container-type--`。

    ```html
    <ul style="--container-type--: inline-size; --flex-flow--: wrap; --gt-all_flex--: 100%; --gap--: 1rem; --item_background--: ghostwhite; --item_padding--: 1rem;">
      <li style="--cq-i-gt-m_flex--: 1 0 0%;"> … </li>
      …
    </ul>
    ```

Selectorize CSS 設計極簡，建議先查看 CSS 程式碼，想像它的可能用途。

---

## 安裝方法

1. 從本倉庫下載 `selectorize.css` 檔案，放入專案中。
2. 在 HTML 的 `<head>` 中引入 `selectorize.css`，建議置於其他 CSS 之前。

   ```html
   <link rel="stylesheet" href="path/to/your/project/selectorize.css" />
   ```

---

## 貢獻

歡迎透過 GitHub Issues 回報錯誤或提出功能建議。
若有意貢獻程式碼，請提交 Pull Request。

---

## 授權條款

本專案採用 [GPL-2.0 授權條款](https://www.gnu.org/licenses/gpl-2.0.html)。
詳情請見 `LICENSE` 檔案。
