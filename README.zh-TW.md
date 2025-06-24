翻譯：[日語](README.md), [德語](README.de.md), [英語](README.en.md), [西班牙語](README.es.md), [法語](README.fr.md), [俄語](README.ru.md), [簡體中文](README.zh-CN.md), [繁體中文](README.zh-TW.md)

此 README 由 [Google Gemini](https://gemini.google.com) 從日語翻譯而來。請知悉。

-----

# Selectorize CSS

一個輕量級的工具型 CSS，它使用 CSS 自訂屬性作為選擇器來應用樣式。

-----

## 概述

Selectorize CSS 實現了以「實用工具優先」（utility-first）的樣式方法，類似於 Tailwind CSS，透過利用 **HTML `style` 屬性中設定的 CSS 自訂屬性**及其對應的 CSS 屬性選擇器來實現。這使得 CSS 標記直觀靈活，無需管理類別名稱。

-----

## 特點

  * **零建構：**
    無需任何特殊的建構過程。它作為純粹的 CSS (Vanilla CSS) 運行。
  * **低學習成本：**
    您可以像直接在 HTML `style` 屬性中編寫屬性一樣使用它。這提供了一種更直觀、更新穎的樣式方法，與需要記住大量類別名稱的常見實用工具優先 CSS 不同。
  * **優化 CSS 程式碼量：**
    為網站特定頁面或元素持續添加 CSS 會導致程式碼量膨脹。Selectorize CSS 透過預設的自訂屬性應用樣式，可以減少冗餘的類別定義，最大限度地減少整體 CSS 程式碼的增加。
  * **高效分離屬性和值：**
    它避免了常見實用工具 CSS 中常見的「`background-red`」、「`border-red`」、「`text-red`」等按值重複類別定義的大量增加。透過使用自訂屬性分離屬性（`background`、`border`、`color` 等）和值（`red`、`green`、`blue` 等），可以顯著減少 CSS 程式碼量並簡化管理。
  * **維護語義化的 HTML 結構：**
    HTML 的文件結構和 `class` 屬性可以專注於語義化，而與外觀相關的非語義化樣式可以透過 `style` 屬性與自訂屬性進行管理。這提高了 HTML 的可維護性。
  * **彈性的樣式覆蓋：**
    由於使用自訂屬性而不是直接在 `style` 屬性中設定屬性，因此樣式不會被強制應用，並且可以在不使用 `!important` 的情況下覆蓋樣式。這允許更彈性的設計調整。
  * **輕量級和高擴展性：**
    它只精選了最少的屬性和功能，因此檔案大小輕巧。它不強制使用特定的設計元件，因此可以彈性地整合到專案特定的設計系統或現有 CSS 中。
  * **多樣的使用情境：**
    Selectorize CSS 可以作為直接控制網頁主要設計和佈局的手段，但它也可以與現有 CSS 或元件結合使用，例如輕鬆創建按鈕變體（大小、顏色等），從而有效地實現局部定制。
  * **簡單的命名規範：**
    只需在 `style` 屬性中設定的屬性名稱前後添加 `--`。
    ```html
    <div style="--color--: var(--red, red);">…</div>
    ```
  * **基於前綴的擴展：**
    使用前綴還可以實現進階樣式：
      * 設定 `--gt-all_PROPERTY-NAME--:` 將樣式應用於元素的所有直接子元素 (`>*`)。
      * 在 `ol`、`ul`、`dl`、`div`、`table`、`tbody`、`thead`、`tfoot`、`tr` 上設定 `--item_PROPERTY-NAME--:` 將樣式應用於它們的直接子元素 `li`、`dt`、`dd`、`td`、`th`。
      * 在 `dl`、`div` 上設定 `--dt_PROPERTY-NAME--:` 將樣式應用於它們的直接子元素 `dt`。
      * 在 `dl`、`div` 上設定 `--dd_PROPERTY-NAME--:` 將樣式應用於它們的直接子元素 `dd`。
      * 設定 `--before_content--:` 可以添加 `::before` 偽元素。
      * 設定 `--after_content--:` 可以添加 `::after` 偽元素。
      * 設定 `--cq-CONTAINER-CONDITION_PROPERTY-NAME--:` 將根據指定的容器查詢條件設定樣式。別忘了在祖先元素上設定 `--container-type--`。

-----

## 安裝方法

1.  從該儲存庫下載 `selectorize.css` 檔案並將其放置在您的專案中。
2.  在 HTML 的 `<head>` 元素中，按如下方式載入 `selectorize.css`。建議將其放置在其他 CSS 檔案之前。
    ```html
    <link rel="stylesheet" href="path/to/your/project/selectorize.css" />
    ```

-----

## 使用範例

以下範例演示了網格佈局的設定。網格項以 240px 為基本尺寸排列。

```html
<ul style="--grid--: auto-flow / repeat(auto-fit, minmax(min(240px, 100%), 1fr)); --gap--: var(--space_medium, 1rem); --background--: var(--palest-gray, #e0e0e0); --item_padding--: var(--space_large, 2rem);">
  <li>…</li>
  …
</ul>
```

以下範例演示了彈性盒子佈局的設定。通常是垂直單列排列，如果容器查詢 (cq) 中內聯尺寸 (i) 大於 (gt) M 尺寸 (m)，則切換為水平單行排列。

```html
<ul style="--container-type--: inline-size; --flex-flow--: wrap; --gt-all_flex--: 100%; --gap--: var(--space_medium, 1rem); --background--: var(--palest-gray, #e0e0e0); --item_padding--: var(--space_large, 2rem);">
  <li style="--cq-i-gt-m_flex--: 1 0 0%;">…</li>
  …
</ul>
```

以下範例為 `button` 類別添加了背景色和文字顏色。

```html
<p style="--text-align--: center;">
  <button type="button" class="button" style="--background--: var(--red, red); --color--: var(--white, white);">
    …
  </button>
</p>
```

透過設定 `var(--red, red)` 這樣的備用值，即使未定義 `--red`，預設也會應用紅色。
以下範例展示了如何使用它來擴展 `button` 類別。

```css
.button {
  /* 當設定為 <button class="button" style="--background--: var(--red, red);">…</button> 時，以下 --background-- 將會被覆蓋。 */
  --background--: transparent; /* 預設背景色為透明 */
  background: var(--background--);
  …
}
```

或者，

```css
.button {
  background: transparent; /* 預設背景色為透明 */
  …
}
.button[style~="--background--:"] {
  background: var(--background--);
}
```

-----

## 貢獻

歡迎透過 GitHub Issues 回報錯誤或提出功能建議。
如果您有興趣貢獻程式碼，請傳送 Pull Request。

-----

## 授權

此專案在 [GPL-2.0 License](https://www.gnu.org/licenses/gpl-2.0.html) 下發布。
有關詳細資訊，請參閱 `LICENSE` 檔案。
