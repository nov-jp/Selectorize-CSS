Translations: [English](README.md), [Japanese](https://www.google.com/search?q=README.ja.md)

-----

# Selectorize CSS

A lightweight utility CSS that applies styles using CSS custom properties as selectors.

-----

## Overview

Selectorize CSS enables a utility-first styling approach, similar to Tailwind CSS, by leveraging **CSS custom properties set in HTML's `style` attribute** and their corresponding CSS attribute selectors. This allows for intuitive and flexible CSS markup without the need for extensive class name management.

-----

## Features

  * **Zero Build:**
    No special build process is required. It functions as pure Vanilla CSS.
  * **Low Learning Curve:**
    You can use it by directly writing properties in the HTML `style` attribute, just like setting inline styles. This offers a more intuitive and novel styling approach, unlike typical utility-first CSS that requires memorizing many class names.
  * **Optimized CSS Code Size:**
    CSS code tends to grow as you add styles for specific web pages or elements. Selectorize CSS applies styles through predefined custom properties, reducing redundant class definitions and minimizing the overall increase in CSS code.
  * **Efficient Separation of Properties and Values:**
    It prevents the common proliferation of redundant class definitions like `background-red`, `border-red`, and `text-red` found in many utility CSS frameworks. By separating properties (`background`, `border`, `color`, etc.) and values (`red`, `green`, `blue`, etc.) using custom properties, it significantly reduces CSS lines and simplifies management.
  * **Maintenance of Semantic HTML Structure:**
    HTML's document structure and `class` attributes can focus on semantic meaning, while non-semantic visual styles can be managed with the `style` attribute and custom properties. This enhances HTML maintainability.
  * **Flexible Style Overriding:**
    Since custom properties are used instead of directly setting properties in the `style` attribute, styles are not forced, allowing for style overrides without using `!important`. This enables more flexible design adjustments.
  * **Lightweight and Highly Extensible:**
    The file size is lightweight, as it focuses only on essential properties and features. It doesn't enforce specific design components, allowing for flexible integration into project-specific design systems or existing CSS.
  * **Diverse Usage Scenarios:**
    Selectorize CSS can be used to directly control the main design and layout of web pages. It also works effectively for partial customizations, such as easily creating button variations (size, color, etc.) by combining it with existing CSS or components.
  * **Simple Naming Convention:**
    Just add `--` before and after the property name set in the `style` attribute.
    ```html
    <div style="--color--: var(--red, red);">…</div>
    ```
  * **Prefix-based Extensions:**
    Advanced styling is possible by using prefixes:
      * Setting `--gt-all_PROPERTY-NAME--:` styles all direct children (`>*`) of the element.
      * Setting `--item_PROPERTY-NAME--:` on `ol`, `ul`, `dl`, `div`, `table`, `tbody`, `thead`, `tfoot`, `tr` styles their immediate `li`, `dt`, `dd`, `td`, `th` children.
      * Setting `--dt_PROPERTY-NAME--:` on `dl`, `div` styles their immediate `dt` children.
      * Setting `--dd_PROPERTY-NAME--:` on `dl`, `div` styles their immediate `dd` children.
      * Setting `--before_content--:` adds a `::before` pseudo-element.
      * Setting `--after_content--:` adds an `::after` pseudo-element.
      * Setting `--cq-CONTAINER-CONDITION_PROPERTY-NAME--:` styles elements based on the specified container query condition. Remember to set `--container-type--` on an ancestor element.

-----

## Installation

1.  Download the `selectorize.css` file from this repository and place it in your project.
2.  Link `selectorize.css` in your HTML's `<head>` section, preferably before other CSS files:
    ```html
    <link rel="stylesheet" href="path/to/your/project/selectorize.css" />
    ```

-----

## Usage Examples

The following example demonstrates setting up a grid layout. Grid items with a base size of 240px will be arranged.

```html
<ul style="--grid--: auto-flow / repeat(auto-fit, minmax(min(240px, 100%), 1fr)); --gap--: var(--space_medium, 1rem); --background--: var(--palest_gray, #e0e0e0); --item_padding--: var(--space_large, 2rem);">
  <li>…</li>
  …
</ul>
```

The next example demonstrates a flexbox layout. Normally arranged in a single vertical column, it switches to a horizontal row when the container query (cq) for inline-size (i) is greater than (gt) medium (m) size.

```html
<ul style="--container-type--: inline-size; --flex-flow--: wrap; --gt-all_flex--: 100%; --gap--: var(--space_medium, 1rem); --background--: var(--palest_gray, #e0e0e0); --item_padding--: var(--space_large, 2rem);">
  <li style="--cq-i-gt-m_flex--: 1 0 0%;">…</li>
  …
</ul>
```

The next example adds background and text color to a `button` class.

```html
<p style="--text-align--: center;">
  <button type="button" class="button" style="--background--: var(--red, red); --color--: var(--white, white);">
    …
  </button>
</p>
```

By setting a fallback value like `var(--red, red)`, red color will be applied by default even if `--red` is not defined.
The next example shows how to use it to extend a `button` class.

```css
.button {
  /* When set like <button class="button" style="--background--: var(--red, red);">…</button>, the following --background-- will be overridden. */
  --background--: transparent; /* Default background color is transparent */
  background: var(--background--);
  …
}
```

Alternatively,

```css
.button {
  background: transparent; /* Default background color is transparent */
  …
}
.button[style~="--background--:"] {
  background: var(--background--);
}
```

-----

## Contributing

Bug reports and feature suggestions are welcome via GitHub Issues.
If you are interested in contributing code, please send a pull request.

-----

## License

This project is licensed under the [GPL-2.0 License](https://www.gnu.org/licenses/gpl-2.0.html).
See the `LICENSE` file for more details.
