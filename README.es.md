[日本語](README.md) | [Deutsch](README.de.md) | [English](README.en.md) | [Espanol](README.es.md) | [Francais](README.fr.md) | [Русский](README.ru.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md)

> **Nota**: Este `README` ha sido traducido del japonés utilizando [ChatGPT](https://chatgpt.com/). Por favor, tenlo en cuenta al leerlo.

---

# Selectorize CSS

Un framework CSS utilitario, minimalista y liviano que utiliza propiedades personalizadas como selectores.

Reinventa el uso del atributo `style`, a menudo evitado, para ofrecer un marcado CSS potente e intuitivo.

---

## Descripción general

Selectorize CSS aplica el enfoque *utility-first*, similar a Tailwind CSS, pero utilizando propiedades personalizadas dentro del atributo `style` de HTML y selectores de atributos en CSS. Esto permite evitar la gestión de nombres de clase, ofreciendo una forma más flexible e intuitiva de escribir estilos.

---

## Características

* **Sin proceso de compilación:**
  No requiere herramientas ni procesos especiales. Es CSS puro (Vanilla CSS).

* **Curva de aprendizaje baja con una convención de nombres simple:**
  Solo necesitas encapsular el nombre de la propiedad entre `--` dentro del atributo `style`. A diferencia de los frameworks tradicionales con cientos de clases, esta metodología es más natural y directa.

  ```html
  <div style="--color--: crimson;"> … </div>
  ```

* **Ligero y altamente extensible:**
  Gracias a su diseño minimalista, el archivo CSS es muy liviano. No impone componentes visuales predefinidos, por lo que puede integrarse fácilmente con sistemas de diseño personalizados o CSS existentes.

  ```html
  <!-- Selectorize CSS + [Open Props](https://open-props.style/) -->
  <div style="--border--: solid var(--border-size-1) var(--gray-1);"> … </div>
  ```

* **Optimización del volumen de código CSS:**
  En proyectos grandes, el CSS tiende a crecer innecesariamente. Selectorize CSS ayuda a reducir las definiciones de clase redundantes usando propiedades reutilizables.

  ```html
  <!-- Enfoque tradicional -->
  <style>
    .very-unique-grid-1 { display: grid; grid: …; … }
    .very-unique-grid-2 { display: grid; grid: …; … }
    …
  </style>
  …
  <div class="very-unique-grid-1"> … </div>
  <div class="very-unique-grid-2"> … </div>
  …

  <!-- Con Selectorize CSS -->
  <div style="--grid--: …;"> … </div>
  <div style="--grid--: …;"> … </div>
  …
  ```

* **Separación eficiente entre propiedades y valores:**
  Evita la proliferación de clases como `bg-red`, `border-red`, `text-red`. En su lugar, separa la propiedad (`background`, `border-color`, `color`) del valor (`red`, `blue`, `green`, etc.), lo cual reduce la cantidad de código y facilita su mantenimiento.

  ```css
  /* Enfoque clásico (<div class="background-pale-red border-red text-red"> … </div>) */
  .background-red { background: crimson; }
  .background-pale-red { background: mistyrose; }
  …
  .border-red { border-color: crimson; }
  .border-pale-red { border-color: mistyrose; }
  …
  .text-red { color: crimson; }
  .text-pale-red { color: mistyrose; }
  …
  
  /* Con Selectorize CSS (<div style="--background--: mistyrose; --border-color--: crimson; --color--: crimson;"> … </div>) */
  [style~="--background--:"] { background: var(--background--); }
  [style~="--border-color--:"] { border-color: var(--border-color--); }
  [style~="--color--:"] { color: var(--color--); }
  ```

* **Preserva la estructura semántica del HTML:**
  El atributo `class` puede utilizarse para describir significado semántico, mientras que el `style` se encarga exclusivamente de la apariencia visual, lo que mejora la claridad y mantenibilidad del código.

  ```html
  <!-- Enfoque tradicional -->
  <div class="important text-red text-bolder align-center"> … </div>

  <!-- Con Selectorize CSS -->
  <div class="important" style="--color--: crimson; --font-weight--: bolder; --text-align--: center;"> … </div>
  ```

* **Flexible y sobrescribible sin `!important`:**
  Al usar propiedades personalizadas dentro del atributo `style`, los estilos se pueden sobrescribir fácilmente sin necesidad de `!important`, lo que permite una personalización más limpia.

  ```css
  /* Enfoque tradicional (<div class="example" style="color: goldenrod;"> … </div>) */
  .example { color: crimson !important; }

  /* Con Selectorize CSS (<div class="example" style="--color--: goldenrod;"> … </div>) */
  .example { color: crimson; } /* Ejemplo: cambiar goldenrod a crimson */
  .example { --color--: crimson; color: var(--color--); } /* Ejemplo: establecer el valor inicial en crimson para que se pueda sobrescribir con `--color--` en el atributo `style` */
  ```

* **Versatilidad de uso:**
  Selectorize CSS puede usarse para crear estructuras de diseño completas o para modificaciones puntuales como variaciones de color o tamaño en componentes reutilizables.

  ```html
  <!-- Sistema de grid de 12 columnas -->
  <div style="--grid--: auto-flow / repeat(12, 1fr); --gap--: 1rem;">
    <div style="--grid-area--: auto / span 2;"> … </div>
    <div style="--grid-area--: auto / span 4;"> … </div>
    <div style="--grid-area--: auto / span 6;"> … </div>
  </div>

  <!-- Personalización de botones -->
  <p style="--text-align--: center;">
    <button class="button" style="--background--: royalblue; --color--: white; --min-inline-size--: calc(100% / 3);"> … </button>
  </p>
  ```

* **Extensiones mediante prefijos:**

  * Usa `--gt-all_PROPERTY-NAME--:` para aplicar estilos a todos los hijos directos (`>*`).

    ```html
    <ul style="--flex-flow--: wrap; --gt-all_flex--: auto;"> … </ul>
    ```

  * Usa `--item_PROPERTY-NAME--:` en `ol`, `ul`, `dl`, `div`, `table`, `tbody`, `thead`, `tfoot`, `tr` para aplicar estilos al `li`, `dt`, `dd`, `td` o `th` más cercano.

    ```html
    <table style="--item_border--: solid thin; --item_padding--: 0.5rem;"> … </table>
    ```

  * Usa `--dt_PROPERTY-NAME--:` para aplicar estilos al `dt` más cercano.

    ```html
    <dl style="--flex-flow--: wrap; --dt_flex--: 100%;">
      <dt> … </dt>
      <dd> … </dd>
      <dd> … </dd>
      …
    </dl>
    ```

  * Usa `--dd_PROPERTY-NAME--:` para aplicar estilos al `dd` más cercano.

    ```html
    <dl style="--flex-flow--: wrap; --dd_flex--: 100%;">
      <dt> … </dt>
      <dt> … </dt>
      <dd> … </dd>
      …
    </dl>
    ```

  * Usa `--before_content--:` para insertar contenido mediante `::before`.

    ```html
    <p style="--before_content--: '👍';"> … </p>
    ```

  * Usa `--after_content--:` para insertar contenido mediante `::after`.

    ```html
    <p style="--after_content--: '😀';"> … </p>
    ```

  * Usa `--cq-CONTAINER-CONDITION_PROPERTY-NAME--:` para aplicar estilos condicionados por *container queries*. No olvides establecer `--container-type--` en el contenedor padre.

    ```html
    <ul style="--container-type--: inline-size; --flex-flow--: wrap; --gt-all_flex--: 100%; --gap--: 1rem; --item_background--: ghostwhite; --item_padding--: 1rem;">
      <li style="--cq-i-gt-m_flex--: 1 0 0%;"> … </li>
      …
    </ul>
    ```

Selectorize CSS está diseñado para ser extremadamente minimalista. Puedes comenzar simplemente leyendo el archivo CSS y explorando lo que es posible.

---

## Instalación

1. Descarga el archivo `selectorize.css` desde este repositorio y colócalo en tu proyecto.
2. Inclúyelo en el `<head>` de tu documento HTML, preferiblemente **antes** de otros archivos CSS:

   ```html
   <link rel="stylesheet" href="ruta/a/tu/proyecto/selectorize.css" />
   ```

---

## Contribuciones

Se agradecen los reportes de errores y sugerencias a través de GitHub Issues.
Si deseas contribuir con código, siéntete libre de enviar un *pull request*.

---

## Licencia

Este proyecto está licenciado bajo la [Licencia GPL-2.0](https://www.gnu.org/licenses/gpl-2.0.html).
Consulta el archivo `LICENSE` para más detalles.
