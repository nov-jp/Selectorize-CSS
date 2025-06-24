[English](README.md) | [Deutsch](README.de.md) | [Espanol](README.es.md) | [Francais](README.fr.md) | [日本語](README.ja.md) | [Русский](README.ru.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md)

> **备注:** 本 `README` 由 [ChatGPT](https://chatgpt.com/) 从日文翻译而来，敬请谅解。

---

# Selectorize CSS

一个利用自定义属性作为选择器的轻量且简单的实用工具 CSS。

它拯救了常被嫌弃的 `style` 属性，实现了直观且强大的 CSS 标记。

---

## 概述

Selectorize CSS 通过在 HTML 的 `style` 属性中设置自定义属性，并配合相应的 CSS 属性选择器，实现了以 Tailwind CSS 为代表的实用工具优先（utility-first）样式方法。这种方式无需管理类名，实现了直观且灵活的 CSS 标记。

---

## 特点

* **零构建：**
  无需任何特殊的构建流程，纯粹的 CSS（Vanilla CSS）。

* **简单的命名规则，学习成本低：**
  只需在 HTML `style` 属性中设置属性名，前后加上 `--` 即可使用。区别于需要记忆大量类名的一般实用工具 CSS，提供了一种更直观且新的样式方法。

  ```html
  <div style="--color--: crimson;"> … </div>
  ```

* **轻量且高度可扩展：**
  设计简洁，文件体积轻巧。不强制特定设计组件，能灵活地集成进项目特有的设计系统或现有 CSS。

  ```html
  <!-- Selectorize CSS + [Open Props](https://open-props.style/) -->
  <div style="--border--: solid var(--border-size-1) var(--gray-1);"> … </div>
  ```

* **优化 CSS 代码量：**
  网站特定页面或元素的 CSS 代码容易膨胀。Selectorize CSS 通过提供的自定义属性来应用样式，减少冗余类定义，最大限度地控制整体 CSS 代码增长。

  ```html
  <!-- 常规方式 -->
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

* **属性与值的高效分离：**
  避免了实用工具 CSS 中常见的类名膨胀，如 `bg-red`、`border-red`、`text-red`。通过将属性（如 `background`、`border-color`、`color`）与值（如 `red`、`green`、`blue`）分离，大幅减少 CSS 代码量，易于管理。

  ```css
  /* 常规方式 (<div class="background-pale-red border-red text-red"> … </div>) */
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

* **保持语义化 HTML 结构：**
  HTML 的文档结构和 `class` 属性集中表达语义意义，样式相关的非语义内容则用 `style` 属性和自定义属性管理，提升 HTML 的可维护性。

  ```html
  <!-- 常规方式 -->
  <div class="important text-red text-bolder align-center"> … </div>

  <!-- Selectorize CSS -->
  <div class="important" style="--color--: crimson; --font-weight--: bolder; --text-align--: center;"> … </div>
  ```

* **灵活的覆盖能力：**
  由于样式写在 `style` 属性中的自定义属性上，不会被强制应用，不用使用 `!important`，方便样式的覆盖与调整。

  ```css
  /* 常规方式 (<div class="example" style="color: goldenrod;"> … </div>) */
  .example { color: crimson !important; }

  /* Selectorize CSS (<div class="example" style="--color--: goldenrod;"> … </div>) */
  .example { color: crimson; } /* 示例：将 goldenrod 修改为 crimson */
  .example { --color--: crimson; color: var(--color--); } /* 初始值为 crimson，可用 `style` 属性中的 `--color--` 覆盖 */
  ```

* **多样的使用场景：**
  Selectorize CSS 可用于网页主设计布局的直接实现，也可结合现有 CSS 或组件，实现按钮颜色、大小等部分定制。

  ```html
  <!-- 12栏网格布局 -->
  <div style="--grid--: auto-flow / repeat(12, 1fr); --gap--: 1rem;">
    <div style="--grid-area--: auto / span 2;"> … </div>
    <div style="--grid-area--: auto / span 4;"> … </div>
    <div style="--grid-area--: auto / span 6;"> … </div>
  </div>

  <!-- 按钮部分定制 -->
  <p style="--text-align--: center;">
    <button class="button" style="--background--: royalblue; --color--: white; --min-inline-size--: calc(100% / 3);"> … </button>
  </p>
  ```

* **通过前缀扩展功能：**

  * 使用 `--gt-all_PROPERTY-NAME--:` 可将样式应用于所有子元素（`>*`）。

    ```html
    <ul style="--flex-flow--: wrap; --gt-all_flex--: auto;"> … </ul>
    ```
  * 在 `ol`, `ul`, `dl`, `div`, `table`, `tbody`, `thead`, `tfoot`, `tr` 设置 `--item_PROPERTY-NAME--:`，样式应用于相应的 `li`, `dt`, `dd`, `td`, `th`。

    ```html
    <table style="--item_border--: solid thin; --item_padding--: 0.5rem;"> … </table>
    ```
  * 在 `dl`, `div` 设置 `--dt_PROPERTY-NAME--:`，样式应用于最近的 `dt`。

    ```html
    <dl style="--flex-flow--: wrap; --dt_flex--: 100%;">
      <dt> … </dt>
      <dd> … </dd>
      <dd> … </dd>
      …
    </dl>
    ```
  * 在 `dl`, `div` 设置 `--dd_PROPERTY-NAME--:`，样式应用于最近的 `dd`。

    ```html
    <dl style="--flex-flow--: wrap; --dd_flex--: 100%;">
      <dt> … </dt>
      <dt> … </dt>
      <dd> … </dd>
      …
    </dl>
    ```
  * 设置 `--before_content--:` 可插入 `::before` 伪元素。

    ```html
    <p style="--before_content--: '👍';"> … </p>
    ```
  * 设置 `--after_content--:` 可插入 `::after` 伪元素。

    ```html
    <p style="--after_content--: '😀';"> … </p>
    ```
  * 设置 `--cq-CONTAINER-CONDITION_PROPERTY-NAME--:`，可根据指定的容器查询条件应用样式。别忘了在祖先元素设置 `--container-type--`。

    ```html
    <ul style="--container-type--: inline-size; --flex-flow--: wrap; --gt-all_flex--: 100%; --gap--: 1rem; --item_background--: ghostwhite; --item_padding--: 1rem;">
      <li style="--cq-i-gt-m_flex--: 1 0 0%;"> … </li>
      …
    </ul>
    ```

Selectorize CSS 设计极简，先看下 CSS 代码，想象它能做什么吧。

---

## 安装方法

1. 从本仓库下载 `selectorize.css` 文件，并放入项目中。
2. 在 HTML 的 `<head>` 中引入 `selectorize.css`，建议放在其他 CSS 之前。

   ```html
   <link rel="stylesheet" href="path/to/your/project/selectorize.css" />
   ```

---

## 贡献

欢迎通过 GitHub Issues 报告 Bug 或提出功能建议。
如果愿意贡献代码，请提交 Pull Request。

---

## 许可证

本项目采用 [GPL-2.0 许可证](https://www.gnu.org/licenses/gpl-2.0.html)。
详情请见 `LICENSE` 文件。
