[English](README.md) | [Deutsch](README.de.md) | [Espanol](README.es.md) | [Francais](README.fr.md) | [日本語](README.ja.md) | [Русский](README.ru.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md)

> **Note**: This `README` was translated from Japanese using [ChatGPT](https://chatgpt.com/). Please keep this in mind when reading.

---

# Selectorize CSS

A lightweight and minimalist utility CSS framework that leverages custom properties as selectors.

It reimagines the often-disliked `style` attribute, enabling intuitive and powerful CSS markup.

---

## Overview

Selectorize CSS implements a utility-first styling approach—similar to Tailwind CSS—using custom properties set in the HTML `style` attribute and CSS attribute selectors to apply styles. This eliminates the need for class name management and enables more intuitive and flexible CSS markup.

---

## Features

* **Zero Build Process:**
  No special build tools required. It's pure, vanilla CSS.

* **Low Learning Curve with Simple Naming Convention:**
  Just wrap your property names with `--` inside the `style` attribute. This approach provides a more intuitive and fresh styling method, without the need to memorize a large number of utility classes.

  ```html
  <div style="--color--: crimson;"> … </div>
  ```

* **Lightweight and Highly Extensible:**
  Its minimal design ensures a small file size. Since it doesn't enforce specific design components, it can be easily integrated into project-specific design systems or existing CSS.

  ```html
  <!-- Selectorize CSS + [Open Props](https://open-props.style/) -->
  <div style="--border--: solid var(--border-size-1) var(--gray-1);"> … </div>
  ```

* **Optimized CSS Codebase:**
  CSS can easily bloat when new styles are added for every unique page or component. By using predefined custom properties, Selectorize CSS reduces redundant class definitions and helps keep your stylesheet lean.

  ```html
  <!-- Traditional approach -->
  <style>
    .very-unique-grid-1 { display: grid; grid: …; … }
    .very-unique-grid-2 { display: grid; grid: …; … }
    …
  </style>
  …
  <div class="very-unique-grid-1"> … </div>
  <div class="very-unique-grid-2"> … </div>
  …

  <!-- With Selectorize CSS -->
  <div style="--grid--: …;"> … </div>
  <div style="--grid--: …;"> … </div>
  …
  ```

* **Efficient Separation of Properties and Values:**
  Prevents class name explosion common in utility CSS (e.g., `bg-red`, `border-red`, `text-red`) by separating properties like `background`, `border-color`, `color`, etc., from values like `red`, `green`, `blue`. This drastically reduces CSS repetition and improves maintainability.

  ```css
  /* Traditional approach (<div class="background-pale-red border-red text-red"> … </div>) */
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

* **Preserves Semantic HTML Structure:**
  Keep `class` attributes focused on semantic meaning, while styling is handled through the `style` attribute and custom properties. This enhances maintainability and semantic clarity.

  ```html
  <!-- Traditional approach -->
  <div class="important text-red text-bolder align-center"> … </div>

  <!-- Selectorize CSS -->
  <div class="important" style="--color--: crimson; --font-weight--: bolder; --text-align--: center;"> … </div>
  ```

* **Override-Friendly Without `!important`:**
  Because styles are applied via custom properties in the `style` attribute, you can override them without using `!important`. This allows flexible and non-intrusive design adjustments.

  ```css
  /* Traditional approach (<div class="example" style="color: goldenrod;"> … </div>) */
  .example { color: crimson !important; }

  /* Selectorize CSS (<div class="example" style="--color--: goldenrod;"> … </div>) */
  .example { color: crimson; } /* Example: overriding crimson with goldenrod */
  .example { --color--: crimson; color: var(--color--); } /* crimson as default, overridable via `style` attribute */
  ```

* **Versatile Usage Scenarios:**
  Selectorize CSS is suitable for implementing full layouts or components, or for localized style variations like button colors and sizes.

  ```html
  <!-- 12-column grid layout -->
  <div style="--grid--: auto-flow / repeat(12, 1fr); --gap--: 1rem;">
    <div style="--grid-area--: auto / span 2;"> … </div>
    <div style="--grid-area--: auto / span 4;"> … </div>
    <div style="--grid-area--: auto / span 6;"> … </div>
  </div>

  <!-- Customizing button styles -->
  <p style="--text-align--: center;">
    <button class="button" style="--background--: royalblue; --color--: white; --min-inline-size--: calc(100% / 3);"> … </button>
  </p>
  ```

* **Advanced Styling with Prefixes:**
  Selectorize CSS supports prefix-based extensions for more advanced use cases.

  * Use `--gt-all_PROPERTY-NAME--:` to apply styles to all direct children (`>*`).

    ```html
    <ul style="--flex-flow--: wrap; --gt-all_flex--: auto;"> … </ul>
    ```

  * Use `--item_PROPERTY-NAME--:` on elements like `ol`, `ul`, `dl`, `div`, `table`, `tbody`, `thead`, `tfoot`, `tr` to target the nearest `li`, `dt`, `dd`, `td`, or `th`.

    ```html
    <table style="--item_border--: solid thin; --item_padding--: 0.5rem;"> … </table>
    ```

  * Use `--dt_PROPERTY-NAME--:` on `dl` or `div` to apply styles to the nearest `dt`.

    ```html
    <dl style="--flex-flow--: wrap; --dt_flex--: 100%;">
      <dt> … </dt>
      <dd> … </dd>
      <dd> … </dd>
      …
    </dl>
    ```

  * Use `--dd_PROPERTY-NAME--:` on `dl` or `div` to apply styles to the nearest `dd`.

    ```html
    <dl style="--flex-flow--: wrap; --dd_flex--: 100%;">
      <dt> … </dt>
      <dt> … </dt>
      <dd> … </dd>
      …
    </dl>
    ```

  * Use `--before_content--:` to insert content via `::before`.

    ```html
    <p style="--before_content--: '👍';"> … </p>
    ```

  * Use `--after_content--:` to insert content via `::after`.

    ```html
    <p style="--after_content--: '😀';"> … </p>
    ```

  * Use `--cq-CONTAINER-CONDITION_PROPERTY-NAME--:` to apply styles based on container query conditions. Be sure to set `--container-type--` on the parent element.

    ```html
    <ul style="--container-type--: inline-size; --flex-flow--: wrap; --gt-all_flex--: 100%; --gap--: 1rem; --item_background--: ghostwhite; --item_padding--: 1rem;">
      <li style="--cq-i-gt-m_flex--: 1 0 0%;"> … </li>
      …
    </ul>
    ```

Selectorize CSS is designed to be extremely minimal. Start by reviewing the CSS source itself—it might inspire new styling ideas.

---

## Installation

1. Download the `selectorize.css` file from this repository and place it in your project.
2. Include the file in the `<head>` of your HTML. It's recommended to load it **before** other stylesheets.

   ```html
   <link rel="stylesheet" href="path/to/your/project/selectorize.css" />
   ```

---

## Contributing

Bug reports and feature suggestions are welcome via GitHub Issues.
If you're interested in contributing code, feel free to submit a pull request.

---

## License

This project is licensed under the [GPL-2.0 License](https://www.gnu.org/licenses/gpl-2.0.html).
See the `LICENSE` file for details.
