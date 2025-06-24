翻译：[日语](README.md), [德语](README.de.md), [英语](README.en.md), [西班牙语](README.es.md), [法语](README.fr.md), [俄语](README.ru.md), [简体中文](README.zh-CN.md), [繁体中文](README.zh-TW.md)

此 README 由 [Google Gemini](https://gemini.google.com) 从日语翻译而来。请知悉。

-----

# Selectorize CSS

一个轻量级的工具类CSS，它使用CSS自定义属性作为选择器来应用样式。

-----

## 概述

Selectorize CSS 实现了以“实用工具优先”（utility-first）的样式方法，类似于 Tailwind CSS，通过利用 **HTML `style` 属性中设置的 CSS 自定义属性**及其对应的 CSS 属性选择器来实现。这使得 CSS 标记直观灵活，无需管理类名。

-----

## 特点

  * **零构建：**
    无需任何特殊的构建过程。它作为纯粹的 CSS (Vanilla CSS) 运行。
  * **低学习成本：**
    您可以像直接在 HTML `style` 属性中编写属性一样使用它。这提供了一种更直观、更新颖的样式方法，与需要记住大量类名的常见实用工具优先 CSS 不同。
  * **优化 CSS 代码量：**
    为网站特定页面或元素持续添加 CSS 会导致代码量膨胀。Selectorize CSS 通过预设的自定义属性应用样式，可以减少冗余的类定义，最大限度地减少整体 CSS 代码的增加。
  * **高效分离属性和值：**
    它避免了常见实用工具 CSS 中常见的“`background-red`”、“`border-red`”、“`text-red`”等按值重复类定义的大量增加。通过使用自定义属性分离属性（`background`、`border`、`color` 等）和值（`red`、`green`、`blue` 等），可以显著减少 CSS 代码量并简化管理。
  * **维护语义化的 HTML 结构：**
    HTML 的文档结构和 `class` 属性可以专注于语义化，而与外观相关的非语义化样式可以通过 `style` 属性和自定义属性进行管理。这提高了 HTML 的可维护性。
  * **灵活的样式覆盖：**
    由于使用自定义属性而不是直接在 `style` 属性中设置属性，因此样式不会被强制应用，并且可以在不使用 `!important` 的情况下覆盖样式。这允许更灵活的设计调整。
  * **轻量级和高扩展性：**
    它只精选了最少的属性和功能，因此文件大小轻巧。它不强制使用特定的设计组件，因此可以灵活地集成到项目特定的设计系统或现有 CSS 中。
  * **多样的使用场景：**
    Selectorize CSS 可以作为直接控制网页主要设计和布局的手段，但它也可以与现有 CSS 或组件结合使用，例如轻松创建按钮变体（大小、颜色等），从而有效地实现局部定制。
  * **简单的命名规范：**
    只需在 `style` 属性中设置的属性名称前后添加 `--`。
    ```html
    <div style="--color--: var(--red, red);">…</div>
    ```
  * **基于前缀的扩展：**
    使用前缀还可以实现高级样式：
      * 设置 `--gt-all_PROPERTY-NAME--:` 将样式应用于元素的所有直接子元素 (`>*`)。
      * 在 `ol`、`ul`、`dl`、`div`、`table`、`tbody`、`thead`、`tfoot`、`tr` 上设置 `--item_PROPERTY-NAME--:` 将样式应用于它们的直接子元素 `li`、`dt`、`dd`、`td`、`th`。
      * 在 `dl`、`div` 上设置 `--dt_PROPERTY-NAME--:` 将样式应用于它们的直接子元素 `dt`。
      * 在 `dl`、`div` 上设置 `--dd_PROPERTY-NAME--:` 将样式应用于它们的直接子元素 `dd`。
      * 设置 `--before_content--:` 可以添加 `::before` 伪元素。
      * 设置 `--after_content--:` 可以添加 `::after` 伪元素。
      * 设置 `--cq-CONTAINER-CONDITION_PROPERTY-NAME--:` 将根据指定的容器查询条件设置样式。别忘了在祖先元素上设置 `--container-type--`。

-----

## 安装方法

1.  从该仓库下载 `selectorize.css` 文件并将其放置在您的项目中。
2.  在 HTML 的 `<head>` 元素中，按如下方式加载 `selectorize.css`。建议将其放置在其他 CSS 文件之前。
    ```html
    <link rel="stylesheet" href="path/to/your/project/selectorize.css" />
    ```

-----

## 使用示例

以下示例演示了网格布局的设置。网格项以 240px 为基本尺寸排列。

```html
<ul style="--grid--: auto-flow / repeat(auto-fit, minmax(min(240px, 100%), 1fr)); --gap--: var(--space_medium, 1rem); --background--: var(--palest-gray, #e0e0e0); --item_padding--: var(--space_large, 2rem);">
  <li>…</li>
  …
</ul>
```

以下示例演示了 flexbox 布局的设置。通常是垂直单列排列，如果容器查询 (cq) 中内联尺寸 (i) 大于 (gt) M 尺寸 (m)，则切换为水平单行排列。

```html
<ul style="--container-type--: inline-size; --flex-flow--: wrap; --gt-all_flex--: 100%; --gap--: var(--space_medium, 1rem); --background--: var(--palest-gray, #e0e0e0); --item_padding--: var(--space_large, 2rem);">
  <li style="--cq-i-gt-m_flex--: 1 0 0%;">…</li>
  …
</ul>
```

以下示例为 `button` 类添加了背景色和文字颜色。

```html
<p style="--text-align--: center;">
  <button type="button" class="button" style="--background--: var(--red, red); --color--: var(--white, white);">
    …
  </button>
</p>
```

通过设置 `var(--red, red)` 这样的回退值，即使未定义 `--red`，默认也会应用红色。
以下示例展示了如何使用它来扩展 `button` 类。

```css
.button {
  /* 当设置为 <button class="button" style="--background--: var(--red, red);">…</button> 时，以下 --background-- 将被覆盖。 */
  --background--: transparent; /* 默认背景色为透明 */
  background: var(--background--);
  …
}
```

或者，

```css
.button {
  background: transparent; /* 默认背景色为透明 */
  …
}
.button[style~="--background--:"] {
  background: var(--background--);
}
```

-----

## 贡献

欢迎通过 GitHub Issues 报告错误或提出功能建议。
如果您有兴趣贡献代码，请发送 Pull Request。

-----

## 许可证

本项目在 [GPL-2.0 License](https://www.gnu.org/licenses/gpl-2.0.html) 下发布。
有关详细信息，请参阅 `LICENSE` 文件。
