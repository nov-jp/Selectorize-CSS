Traducciones: [Japones](README.md), [Aleman](README.de.md), [Ingles](README.en.md), [Espanol](README.es.md), [Frances](README.fr.md), [Ruso](README.ru.md), [Chino simplificado](README.zh-CN.md), [Chino tradicional](README.zh-TW.md)

Este README fue traducido del japones por [Google Gemini](https://gemini.google.com). Por favor, tengalo en cuenta.

-----

# Selectorize CSS

Un CSS utilitario ligero que aplica estilos usando propiedades personalizadas de CSS como selectores.

-----

## Resumen

Selectorize CSS implementa una metodologia de estilizacion "utility-first", similar a Tailwind CSS, utilizando propiedades personalizadas configuradas en el atributo `style` de HTML y sus correspondientes selectores de atributo CSS. Esto permite un marcado CSS intuitivo y flexible sin la necesidad de gestionar nombres de clases.

-----

## Caracteristicas

  * **Cero compilacion:**
    No se requiere ningun proceso de compilacion especial. Funciona como CSS puro (Vanilla CSS).
  * **Bajo coste de aprendizaje:**
    Se puede utilizar escribiendo directamente propiedades en el atributo `style` de HTML, de forma similar a como se configuran los estilos en linea. Esto ofrece un enfoque de estilizacion mas intuitivo y novedoso, a diferencia del CSS "utility-first" comun que requiere memorizar muchos nombres de clases.
  * **Optimizacion del tamano del codigo CSS:**
    La cantidad de codigo CSS tiende a aumentar cuando se anaden estilos para paginas o elementos especificos de un sitio web. Selectorize CSS aplica estilos a traves de propiedades personalizadas ya preparadas, lo que reduce las definiciones de clase redundantes y minimiza el aumento general del codigo CSS.
  * **Separacion eficiente de propiedades y valores:**
    Evita la proliferacion comun de definiciones de clase redundantes como "`background-red`", "`border-red`" y "`text-red`", que se encuentran a menudo en el CSS utilitario. Al separar propiedades (`background`, `border`, `color`, etc.) y valores (`red`, `green`, `blue`, etc.) mediante propiedades personalizadas, se reduce significativamente la cantidad de codigo CSS y se facilita su gestion.
  * **Mantenimiento de la estructura semantica de HTML:**
    La estructura del documento HTML y los atributos `class` pueden centrarse en el significado semantico, mientras que los estilos visuales no semanticos pueden gestionarse con el atributo `style` y las propiedades personalizadas. Esto mejora la mantenibilidad del HTML.
  * **Flexibilidad en la sobrescritura de estilos:**
    Dado que se utilizan propiedades personalizadas en lugar de establecer propiedades directamente en el atributo `style`, los estilos no se aplican forzosamente y se pueden sobrescribir sin usar `!important`. Esto permite ajustes de diseno mas flexibles.
  * **Ligereza y alta extensibilidad:**
    El tamano del archivo es ligero, ya que se han seleccionado solo las propiedades y funciones minimas necesarias. No impone componentes de diseno especificos, lo que permite una integracion flexible en sistemas de diseno especificos del proyecto o en CSS existente.
  * **Diversos escenarios de uso:**
    Selectorize CSS se puede utilizar como un medio para controlar directamente el diseno y la maquetacion principal de paginas web, pero tambien es eficaz para personalizaciones parciales, como crear facilmente variaciones de botones (tamano, color, etc.) combinandolo con CSS o componentes existentes.
  * **Convencion de nombres simple:**
    Simplemente anada `--` antes y despues del nombre de la propiedad establecida en el atributo `style`.
    ```html
    <div style="--color--: var(--red, red);">…</div>
    ```
  * **Extensiones basadas en prefijos:**
    Tambien es posible un estilo avanzado utilizando prefijos:
      * Configurar `--gt-all_PROPERTY-NAME--:` aplica estilo a todos los hijos directos (`>*`) del elemento.
      * Configurar `--item_PROPERTY-NAME--:` en `ol`, `ul`, `dl`, `div`, `table`, `tbody`, `thead`, `tfoot`, `tr` aplica estilo a sus hijos inmediatos `li`, `dt`, `dd`, `td`, `th`.
      * Configurar `--dt_PROPERTY-NAME--:` en `dl`, `div` aplica estilo a sus hijos `dt` inmediatos.
      * Configurar `--dd_PROPERTY-NAME--:` en `dl`, `div` aplica estilo a sus hijos `dd` inmediatos.
      * Configurar `--before_content--:` anade un pseudo-elemento `::before`.
      * Configurar `--after_content--:` anade un pseudo-elemento `::after`.
      * Configurar `--cq-CONTAINER-CONDITION_PROPERTY-NAME--:` aplica estilo a los elementos segun la condicion de consulta de contenedor especificada. No olvide configurar `--container-type--` en un elemento ancestral.

-----

## Instalacion

1.  Descargue el archivo `selectorize.css` de este repositorio y coloquelo en su proyecto.
2.  En el elemento `<head>` de su HTML, incluya `selectorize.css` como se muestra a continuacion. Se recomienda cargarlo antes que otros archivos CSS.
    ```html
    <link rel="stylesheet" href="path/to/your/project/selectorize.css" />
    ```

-----

## Ejemplos de uso

El siguiente ejemplo muestra la configuracion de un diseno de cuadricula. Los elementos de la cuadricula con un tamano base de 240px se organizaran.

```html
<ul style="--grid--: auto-flow / repeat(auto-fit, minmax(min(240px, 100%), 1fr)); --gap--: var(--space_medium, 1rem); --background--: var(--palest-gray, #e0e0e0); --item_padding--: var(--space_large, 2rem);">
  <li>…</li>
  …
</ul>
```

El siguiente ejemplo muestra la configuracion de un diseno de flexbox. Normalmente dispuesto en una sola columna vertical, cambia a una fila horizontal si la consulta de contenedor (cq) para el tamano en linea (i) es mayor que (gt) el tamano M (m).

```html
<ul style="--container-type--: inline-size; --flex-flow--: wrap; --gt-all_flex--: 100%; --gap--: var(--space_medium, 1rem); --background--: var(--palest-gray, #e0e0e0); --item_padding--: var(--space_large, 2rem);">
  <li style="--cq-i-gt-m_flex--: 1 0 0%;">…</li>
  …
</ul>
```

El siguiente ejemplo anade un color de fondo y un color de texto a la clase `button`.

```html
<p style="--text-align--: center;">
  <button type="button" class="button" style="--background--: var(--red, red); --color--: var(--white, white);">
    …
  </button>
</p>
```

Al establecer un valor de reserva como `var(--red, red)`, se aplicara el color rojo por defecto aunque `--red` no este definido.
El siguiente ejemplo muestra como usarlo para extender una clase `button`.

```css
.button {
  /* Si se configura como <button class="button" style="--background--: var(--red, red);">…</button>, el siguiente --background-- sera sobrescrito. */
  --background--: transparent; /* El color de fondo predeterminado es transparente */
  background: var(--background--);
  …
}
```

Alternativamente,

```css
.button {
  background: transparent; /* El color de fondo predeterminado es transparente */
  …
}
.button[style~="--background--:"] {
  background: var(--background--);
}
```

-----

## Contribucion

Los informes de errores y las sugerencias de funciones son bienvenidos a traves de los Issues de GitHub.
Si esta interesado en contribuir con codigo, envie una solicitud de extraccion (pull request).

-----

## Licencia

Este proyecto esta bajo la [Licencia GPL-2.0](https://www.gnu.org/licenses/gpl-2.0.html).
Consulte el archivo `LICENSE` para mas detalles.
