Ubersetzungen: [Japanisch](README.md), [Deutsch](README.de.md), [Englisch](README.en.md), [Spanisch](README.es.md), [Franzosisch](README.fr.md), [Russisch](README.ru.md), [Vereinfachtes Chinesisch](README.zh-CN.md), [Traditionelles Chinesisch](README.zh-TW.md)

Dieses README wurde aus dem Japanischen von [Google Gemini](https://gemini.google.com) ubersetzt. Bitte beachten Sie dies.

-----

# Selectorize CSS

Ein leichtgewichtiges Utility-CSS, das Stile mithilfe von CSS-Custom-Properties als Selektoren anwendet.

-----

## Ubersicht

Selectorize CSS ermoglicht einen Utility-First-Styling-Ansatz, ahnlich wie Tailwind CSS, indem es **CSS-Custom-Properties, die im `style`-Attribut von HTML gesetzt werden**, und die entsprechenden CSS-Attribut-Selektoren nutzt. Dies ermoglicht eine intuitive und flexible CSS-Markup-Erstellung, ohne dass eine umfangreiche Verwaltung von Klassennamen erforderlich ist.

-----

## Funktionen

  * **Zero Build:**
    Es ist kein spezieller Build-Prozess erforderlich. Es funktioniert als reines CSS (Vanilla CSS).
  * **Geringe Lernkurve:**
    Sie konnen es verwenden, indem Sie Eigenschaften direkt im `style`-Attribut von HTML festlegen, ahnlich wie beim Setzen von Inline-Styles. Dies bietet einen intuitiveren und neueren Styling-Ansatz, der sich von typischem Utility-First-CSS unterscheidet, bei dem man viele Klassennamen auswendig lernen muss.
  * **Optimierung der CSS-Code-Menge:**
    Die CSS-Code-Menge neigt dazu, sich aufzublahen, wenn man standig CSS fur bestimmte Webseiten oder Elemente hinzufugt. Selectorize CSS wendet Stile uber bereitgestellte Custom-Properties an, wodurch redundante Klassendefinitionen reduziert und die Zunahme des gesamten CSS-Codes minimiert werden kann.
  * **Effiziente Trennung von Eigenschaften und Werten:**
    Es verhindert die ubliche Ausbreitung redundanter Klassendefinitionen wie ?`background-red`“, ?`border-red`“ und ?`text-red`“, die in vielen Utility-CSS-Frameworks vorkommen. Durch die Trennung von Eigenschaften (`background`, `border`, `color` usw.) und Werten (`red`, `green`, `blue` usw.) mithilfe von Custom-Properties wird die CSS-Schreibweise erheblich reduziert und die Verwaltung vereinfacht.
  * **Beibehaltung der semantischen HTML-Struktur:**
    Die HTML-Dokumentstruktur und die `class`-Attribute konnen sich auf die semantische Bedeutung konzentrieren, wahrend nicht-semantische visuelle Stile mit dem `style`-Attribut und Custom-Properties verwaltet werden konnen. Dies verbessert die Wartbarkeit des HTML.
  * **Flexibilitat beim Uberschreiben von Stilen:**
    Da Custom-Properties anstelle des direkten Setzens von Eigenschaften im `style`-Attribut verwendet werden, werden Stile nicht erzwungen, und Stile konnen ohne die Verwendung von `!important` uberschrieben werden. Dies ermoglicht flexiblere Designanpassungen.
  * **Leichtgewichtigkeit und hohe Erweiterbarkeit:**
    Die Dateigrose ist gering, da nur die notwendigsten Eigenschaften und Funktionen ausgewahlt wurden. Da keine spezifischen Designkomponenten erzwungen werden, kann es flexibel in projektspezifische Designsysteme oder bestehendes CSS integriert werden.
  * **Vielfaltige Nutzungsszenarien:**
    Selectorize CSS kann als Mittel zur direkten Steuerung des Hauptdesigns und des Layouts von Webseiten verwendet werden, zeigt aber auch seine Wirksamkeit bei teilweisen Anpassungen, wie dem einfachen Erstellen von Schaltflachenvarianten (Grose, Farbe usw.) durch die Kombination mit bestehendem CSS oder Komponenten.
  * **Einfache Benennungskonvention:**
    Fugen Sie dem Eigenschaftsnamen, der im `style`-Attribut festgelegt wird, einfach `--` vor und nach hinzu.
    ```html
    <div style="--color--: var(--red, red);">…</div>
    ```
  * **Erweiterung durch Prafixe:**
    Durch die Verwendung von Prafixen ist auch fortgeschrittenes Styling moglich:
      * Das Setzen von `--gt-all_PROPERTY-NAME--:` styled alle direkten Kindelemente (`>*`) des Elements.
      * Das Setzen von `--item_PROPERTY-NAME--:` bei `ol`, `ul`, `dl`, `div`, `table`, `tbody`, `thead`, `tfoot`, `tr` styled deren direkte `li`, `dt`, `dd`, `td`, `th` Kindelemente.
      * Das Setzen von `--dt_PROPERTY-NAME--:` bei `dl`, `div` styled deren direkte `dt` Kindelemente.
      * Das Setzen von `--dd_PROPERTY-NAME--:` bei `dl`, `div` styled deren direkte `dd` Kindelemente.
      * Das Setzen von `--before_content--:` fugt ein `::before`-Pseudo-Element hinzu.
      * Das Setzen von `--after_content--:` fugt ein `::after`-Pseudo-Element hinzu.
      * Das Setzen von `--cq-CONTAINER-CONDITION_PROPERTY-NAME--:` styled Elemente basierend auf der angegebenen Container-Query-Bedingung. Denken Sie daran, `--container-type--` auf einem ubergeordneten Element zu setzen.

-----

## Installation

1.  Laden Sie die Datei `selectorize.css` aus diesem Repository herunter und legen Sie sie in Ihrem Projekt ab.
2.  Binden Sie `selectorize.css` im `<head>`-Element Ihres HTML ein, vorzugsweise vor anderen CSS-Dateien:
    ```html
    <link rel="stylesheet" href="path/to/your/project/selectorize.css" />
    ```

-----

## Anwendungsbeispiele

Das folgende Beispiel zeigt die Einrichtung eines Grid-Layouts. Grid-Elemente mit einer Basisgrose von 240px werden angeordnet.

```html
<ul style="--grid--: auto-flow / repeat(auto-fit, minmax(min(240px, 100%), 1fr)); --gap--: var(--space_medium, 1rem); --background--: var(--palest-gray, #e0e0e0); --item_padding--: var(--space_large, 2rem);">
  <li>…</li>
  …
</ul>
```

Das nachste Beispiel zeigt ein Flexbox-Layout. Normalerweise in einer einzigen vertikalen Spalte angeordnet, wechselt es zu einer horizontalen Zeile, wenn die Container-Query (cq) fur die Inline-Grose (i) groser (gt) als die M-Grose (m) ist.

```html
<ul style="--container-type--: inline-size; --flex-flow--: wrap; --gt-all_flex--: 100%; --gap--: var(--space_medium, 1rem); --background--: var(--palest-gray, #e0e0e0); --item_padding--: var(--space_large, 2rem);">
  <li style="--cq-i-gt-m_flex--: 1 0 0%;">…</li>
  …
</ul>
```

Das nachste Beispiel fugt einer `button`-Klasse Hintergrund- und Textfarbe hinzu.

```html
<p style="--text-align--: center;">
  <button type="button" class="button" style="--background--: var(--red, red); --color--: var(--white, white);">
    …
  </button>
</p>
```

Durch das Setzen eines Fallback-Wertes wie `var(--red, red)` wird die Farbe Rot standardmasig angewendet, auch wenn `--red` nicht definiert ist.
Das nachste Beispiel zeigt, wie es zur Erweiterung einer `button`-Klasse verwendet wird.

```css
.button {
  /* Wenn gesetzt wie <button class="button" style="--background--: var(--red, red);">…</button>, wird das folgende --background-- uberschrieben. */
  --background--: transparent; /* Standard-Hintergrundfarbe ist transparent */
  background: var(--background--);
  …
}
```

Alternativ,

```css
.button {
  background: transparent; /* Standard-Hintergrundfarbe ist transparent */
  …
}
.button[style~="--background--:"] {
  background: var(--background--);
}
```

-----

## Beitrag

Fehlerberichte und Funktionsvorschlage sind uber GitHub Issues willkommen.
Wenn Sie Interesse haben, Code beizutragen, senden Sie bitte einen Pull Request.

-----

## Lizenz

Dieses Projekt ist unter der [GPL-2.0 Lizenz](https://www.gnu.org/licenses/gpl-2.0.html) veroffentlicht.
Weitere Details finden Sie in der Datei `LICENSE`.
