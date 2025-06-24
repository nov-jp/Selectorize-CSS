[English](README.md) | [Deutsch](README.de.md) | [Espanol](README.es.md) | [Francais](README.fr.md) | [日本語](README.ja.md) | [Русский](README.ru.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md)

> **Hinweis**: Dieses `README` wurde mithilfe von [ChatGPT](https://chatgpt.com/) aus dem Japanischen übersetzt. Bitte berücksichtigen Sie dies beim Lesen.

---

# Selectorize CSS

Ein leichtgewichtiges, minimalistisches Utility-CSS-Framework, das benutzerdefinierte Properties als Selektoren verwendet.

Es nutzt das oft ungeliebte `style`-Attribut neu und ermöglicht eine intuitive und leistungsstarke CSS-Auszeichnung.

---

## Übersicht

Selectorize CSS verfolgt einen Utility-First-Ansatz – ähnlich wie Tailwind CSS –, verwendet dabei jedoch benutzerdefinierte Properties im HTML-`style`-Attribut sowie CSS-Attributselektoren zur Stilzuweisung. Dadurch entfällt das Verwalten von Klassennamen, und es entsteht eine intuitivere und flexiblere CSS-Struktur.

---

## Merkmale

* **Kein Build-Prozess erforderlich:**
  Es wird keine Build-Toolchain benötigt. Es handelt sich um reines Vanilla-CSS.

* **Geringe Lernkurve durch einfache Namenskonvention:**
  Zur Verwendung genügt es, den Namen der CSS-Property im `style`-Attribut mit `--` zu umschließen. Dieses Konzept ermöglicht eine intuitive, alternative Methode zum bekannten Utility-CSS-Stil.

  ```html
  <div style="--color--: crimson;"> … </div>
  ```

* **Leichtgewichtig und hochgradig erweiterbar:**
  Dank eines minimalistischen Designs bleibt die Dateigröße klein. Es werden keine vordefinierten Design-Komponenten erzwungen, wodurch sich Selectorize CSS leicht in bestehende Designsysteme und CSS-Strukturen integrieren lässt.

  ```html
  <!-- Selectorize CSS + [Open Props](https://open-props.style/) -->
  <div style="--border--: solid var(--border-size-1) var(--gray-1);"> … </div>
  ```

* **Optimierter CSS-Codeumfang:**
  Ohne Utility-Systeme neigt CSS zur Überfrachtung durch sich wiederholende Klassen. Mit Selectorize CSS erfolgt die Stilzuweisung über Properties, wodurch redundante Klassendefinitionen entfallen.

  ```html
  <!-- Klassischer Ansatz -->
  <style>
    .very-unique-grid-1 { display: grid; grid: …; … }
    .very-unique-grid-2 { display: grid; grid: …; … }
    …
  </style>
  …
  <div class="very-unique-grid-1"> … </div>
  <div class="very-unique-grid-2"> … </div>
  …

  <!-- Mit Selectorize CSS -->
  <div style="--grid--: …;"> … </div>
  <div style="--grid--: …;"> … </div>
  ```

* **Effiziente Trennung von Properties und Werten:**
  Klassische Utility-CSS-Frameworks führen oft zu Klassen-Explosionen wie `bg-red`, `border-red`, `text-red`. Selectorize CSS trennt Eigenschaften (`background`, `border-color`, `color`) von Werten (`red`, `green`, `blue`) – was die Wartung erleichtert und die CSS-Menge reduziert.

  ```css
  /* Klassischer Ansatz (<div class="background-pale-red border-red text-red"> … </div>) */
  .background-red { background: crimson; }
  .background-pale-red { background: mistyrose; }
  …
  .border-red { border-color: crimson; }
  .border-pale-red { border-color: mistyrose; }
  …
  .text-red { color: crimson; }
  .text-pale-red { color: mistyrose; }
  …

  /* Mit Selectorize CSS (<div style="--background--: mistyrose; --border-color--: crimson; --color--: crimson;"> … </div>) */
  [style~="--background--:"] { background: var(--background--); }
  [style~="--border-color--:"] { border-color: var(--border-color--); }
  [style~="--color--:"] { color: var(--color--); }
  ```

* **Beibehaltung semantischer HTML-Struktur:**
  Die `class`-Attribute können semantisch bleiben, während die visuelle Gestaltung über das `style`-Attribut und benutzerdefinierte Properties erfolgt. Dies verbessert die Lesbarkeit und Wartbarkeit des HTML-Codes.

  ```html
  <!-- Klassischer Ansatz -->
  <div class="important text-red text-bolder align-center"> … </div>

  <!-- Mit Selectorize CSS -->
  <div class="important" style="--color--: crimson; --font-weight--: bolder; --text-align--: center;"> … </div>
  ```

* **Flexible Überschreibung ohne `!important`:**
  Da die Styles über benutzerdefinierte Properties gesetzt werden, lassen sie sich ohne `!important` überschreiben – was flexiblere Designanpassungen ermöglicht.

  ```css
  /* Klassischer Ansatz (<div class="example" style="color: goldenrod;"> … </div>) */
  .example { color: crimson !important; }

  /* Mit Selectorize CSS (<div class="example" style="--color--: goldenrod;"> … </div>) */
  .example { color: crimson; } /* Beispiel: goldenrod wird zu crimson geändert */
  .example { --color--: crimson; color: var(--color--); } /* Beispiel: Anfangswert auf crimson gesetzt, damit `--color--` im `style`-Attribut überschrieben werden kann */
  ```

* **Vielfältige Einsatzmöglichkeiten:**
  Selectorize CSS kann für das grundlegende Layout oder gezielte UI-Komponenten eingesetzt werden – z. B. für Varianten wie unterschiedliche Button-Farben und -Größen.

  ```html
  <!-- 12-Spalten-Grid -->
  <div style="--grid--: auto-flow / repeat(12, 1fr); --gap--: 1rem;">
    <div style="--grid-area--: auto / span 2;"> … </div>
    <div style="--grid-area--: auto / span 4;"> … </div>
    <div style="--grid-area--: auto / span 6;"> … </div>
  </div>

  <!-- Individuelle Button-Anpassung -->
  <p style="--text-align--: center;">
    <button class="button" style="--background--: royalblue; --color--: white; --min-inline-size--: calc(100% / 3);"> … </button>
  </p>
  ```

* **Erweiterbarkeit über Präfixe:**

  * `--gt-all_PROPERTY-NAME--:` wendet Styles auf alle direkten Kindelemente (`>*`) an.

    ```html
    <ul style="--flex-flow--: wrap; --gt-all_flex--: auto;"> … </ul>
    ```

  * `--item_PROPERTY-NAME--:` auf `ol`, `ul`, `dl`, `div`, `table`, `tbody`, `thead`, `tfoot`, `tr` wirkt auf das jeweils nächste `li`, `dt`, `dd`, `td` oder `th`.

    ```html
    <table style="--item_border--: solid thin; --item_padding--: 0.5rem;"> … </table>
    ```

  * `--dt_PROPERTY-NAME--:` auf `dl` oder `div` wendet Styles auf das nächste `dt`-Element an.

    ```html
    <dl style="--flex-flow--: wrap; --dt_flex--: 100%;">
      <dt> … </dt>
      <dd> … </dd>
      <dd> … </dd>
      …
    </dl>
    ```

  * `--dd_PROPERTY-NAME--:` wirkt entsprechend auf `dd`.

    ```html
    <dl style="--flex-flow--: wrap; --dd_flex--: 100%;">
      <dt> … </dt>
      <dt> … </dt>
      <dd> … </dd>
      …
    </dl>
    ```

  * `--before_content--:` fügt Inhalte über das `::before`-Pseudoelement ein.

    ```html
    <p style="--before_content--: '👍';"> … </p>
    ```

  * `--after_content--:` für `::after`-Inhalte.

    ```html
    <p style="--after_content--: '😀';"> … </p>
    ```

  * `--cq-CONTAINER-CONDITION_PROPERTY-NAME--:` ermöglicht Container-Query-abhängige Styles. Vergessen Sie nicht, `--container-type--` im Elternelement zu setzen.

    ```html
    <ul style="--container-type--: inline-size; --flex-flow--: wrap; --gt-all_flex--: 100%; --gap--: 1rem; --item_background--: ghostwhite; --item_padding--: 1rem;">
      <li style="--cq-i-gt-m_flex--: 1 0 0%;"> … </li>
      …
    </ul>
    ```

Selectorize CSS ist äußerst minimalistisch gehalten – werfen Sie einfach einen Blick in die CSS-Datei und lassen Sie sich von den Möglichkeiten inspirieren.

---

## Installation

1. Laden Sie die Datei `selectorize.css` aus diesem Repository herunter und binden Sie sie in Ihr Projekt ein.
2. Verlinken Sie sie im `<head>`-Bereich Ihrer HTML-Datei, idealerweise \*\*vor


\*\* anderen Stylesheets:

```html
<link rel="stylesheet" href="path/to/your/project/selectorize.css" />
```

---

## Beiträge

Fehlermeldungen und Feature-Vorschläge sind über GitHub Issues willkommen.
Pull Requests sind gerne gesehen, wenn Sie zum Code beitragen möchten.

---

## Lizenz

Dieses Projekt steht unter der [GPL-2.0-Lizenz](https://www.gnu.org/licenses/gpl-2.0.html).
Details finden Sie in der Datei `LICENSE`.
