[English](README.md) | [Deutsch](README.de.md) | [Espanol](README.es.md) | [Francais](README.fr.md) | [日本語](README.ja.md) | [Русский](README.ru.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md)

> **Примечание:** Этот `README` был переведён с японского языка с помощью [ChatGPT](https://chatgpt.com/). Пожалуйста, учитывайте это при чтении.

---

# Selectorize CSS

Лёгкий, минималистичный CSS-фреймворк с утилитарным подходом, использующий пользовательские свойства в качестве селекторов.

Переосмысливает использование часто игнорируемого атрибута `style`, делая CSS-разметку интуитивно понятной и мощной.

---

## Общее описание

Selectorize CSS реализует *utility-first* подход, как в Tailwind CSS, но с использованием **пользовательских свойств (custom properties) внутри атрибута `style` HTML** и **селекторов по атрибуту** в CSS. Это позволяет отказаться от громоздкой системы классов и писать CSS более гибко и понятно.

---

## Особенности

* **Без сборки:**
  Не требует компиляции или дополнительных инструментов. Это чистый CSS (Vanilla CSS).

* **Простая система именования и лёгкий порог входа:**
  Чтобы использовать стиль, просто добавьте имя свойства с префиксом и постфиксом `--` внутри `style`.

  ```html
  <div style="--color--: crimson;"> … </div>
  ```

* **Минимализм и расширяемость:**
  Небольшой размер файла и отсутствие жёстких компонентов позволяют легко внедрять Selectorize в любые проекты и дизайн-системы.

  ```html
  <!-- Selectorize CSS + [Open Props](https://open-props.style/) -->
  <div style="--border--: solid var(--border-size-1) var(--gray-1);"> … </div>
  ```

* **Оптимизация CSS-кода:**
  Вместо постоянного добавления новых классов для каждой страницы можно переиспользовать свойства, снижая общий объём кода.

  ```html
  <!-- Обычный подход -->
  <style>
    .grid-layout-1 { display: grid; grid: …; }
    .grid-layout-2 { display: grid; grid: …; }
    …
  </style>
  …
  <div class="grid-layout-1"> … </div>
  <div class="grid-layout-2"> … </div>
  …

  <!-- Selectorize CSS -->
  <div style="--grid--: …;"> … </div>
  <div style="--grid--: …;"> … </div>
  …
  ```

* **Разделение свойств и значений:**
  Избегайте создания избыточных классов вроде `bg-red`, `border-red`, `text-red`. Вместо этого используйте одно свойство и назначайте нужное значение:

  ```css
  /* Классический подход (<div class="bg-light-red border-red text-red"> … </div>) */
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

* **Сохранение семантики HTML:**
  `class` можно использовать для логической структуры, а внешний вид переносится в `style`, улучшая читаемость и поддержку кода.

  ```html
  <!-- Классический подход -->
  <div class="important text-red text-bold align-center"> … </div>

  <!-- Selectorize CSS -->
  <div class="important" style="--color--: crimson; --font-weight--: bolder; --text-align--: center;"> … </div>
  ```

* **Гибкое переопределение без `!important`:**
  Стиль можно переопределить прямо из `style`, без необходимости использовать `!important`.

  ```css
  /* Классический способ */
  .example { color: crimson !important; }

  /* Selectorize CSS */
  .example { color: crimson; } /* Пример: изменение goldenrod на crimson */
  .example { --color--: crimson; color: var(--color--); } /* Пример: установка начального значения crimson, чтобы можно было переопределить через `--color--` в атрибуте `style` */
  ```

* **Гибкость применения:**
  Подходит как для построения сложных интерфейсов (например, грид-сеток), так и для частичной кастомизации компонентов (например, изменение цвета кнопки).

  ```html
  <!-- Грид-система из 12 колонок -->
  <div style="--grid--: auto-flow / repeat(12, 1fr); --gap--: 1rem;">
    <div style="--grid-area--: auto / span 2;"> … </div>
    <div style="--grid-area--: auto / span 4;"> … </div>
    <div style="--grid-area--: auto / span 6;"> … </div>
  </div>

  <!-- Кастомизация кнопки -->
  <p style="--text-align--: center;">
    <button class="button" style="--background--: royalblue; --color--: white; --min-inline-size--: calc(100% / 3);"> … </button>
  </p>
  ```

* **Расширения через префиксы:**

  * `--gt-all_PROPERTY--:` — применяет стиль ко всем прямым потомкам (`>*`).

    ```html
    <ul style="--flex-flow--: wrap; --gt-all_flex--: auto;"> … </ul>
    ```

  * `--item_PROPERTY--:` применяется к `li`, `dt`, `dd`, `td`, `th` в зависимости от ближайшего родителя (`ul`, `dl`, `table` и т.п.).

    ```html
    <table style="--item_border--: solid thin; --item_padding--: 0.5rem;"> … </table>
    ```

  * `--dt_PROPERTY--:` применяет стиль к ближайшему `dt`.

    ```html
    <dl style="--flex-flow--: wrap; --dt_flex--: 100%;">
      <dt> … </dt>
      <dd> … </dd>
      <dd> … </dd>
      …
    </dl>
    ```

  * `--dd_PROPERTY--:` применяет стиль к `dd`.

    ```html
    <dl style="--flex-flow--: wrap; --dd_flex--: 100%;">
      <dt> … </dt>
      <dt> … </dt>
      <dd> … </dd>
      …
    </dl>
    ```

  * `--before_content--:` вставляет `::before` с указанным контентом.

    ```html
    <p style="--before_content--: '👍';"> … </p>
    ```

  * `--after_content--:` вставляет `::after`.

    ```html
    <p style="--after_content--: '😀';"> … </p>
    ```

  * `--cq-CONDITION_PROPERTY--:` применяет стили при выполнении container query. Не забудьте задать `--container-type--` родителю.

    ```html
    <ul style="--container-type--: inline-size; --flex-flow--: wrap; --gt-all_flex--: 100%; --gap--: 1rem; --item_background--: ghostwhite; --item_padding--: 1rem;">
      <li style="--cq-i-gt-m_flex--: 1 0 0%;"> … </li>
      …
    </ul>
    ```

Selectorize CSS — это минималистичный инструмент. Просто откройте CSS-файл и посмотрите, на что он способен.

---

## Установка

1. Скачайте файл `selectorize.css` из репозитория и добавьте его в ваш проект.
2. Подключите его в `<head>` HTML-документа **до** подключения других CSS-файлов:

   ```html
   <link rel="stylesheet" href="путь/к/вашему/проекту/selectorize.css" />
   ```

---

## Вклад

Мы приветствуем отчёты об ошибках и предложения новых функций через GitHub Issues.
Pull requests с улучшениями кода также приветствуются.

---

## Лицензия

Этот проект распространяется по лицензии [GPL-2.0](https://www.gnu.org/licenses/gpl-2.0.html).
Подробности — в файле `LICENSE`.
