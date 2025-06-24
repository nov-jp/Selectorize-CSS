[English](README.md) | [Deutsch](README.de.md) | [Espanol](README.es.md) | [Francais](README.fr.md) | [日本語](README.ja.md) | [Русский](README.ru.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md)

> **Remarque** : Ce `README` a été traduit depuis le japonais à l’aide de [ChatGPT](https://chatgpt.com/). Merci d’en tenir compte lors de la lecture.

---

# Selectorize CSS

Un framework CSS utilitaire, minimaliste et léger, qui utilise des propriétés personnalisées comme sélecteurs.

Il réhabilite l’attribut `style`, souvent évité, pour offrir une syntaxe CSS intuitive et puissante.

---

## Aperçu

Selectorize CSS adopte une approche *utility-first*, similaire à Tailwind CSS, mais s’appuie sur des **propriétés personnalisées dans l’attribut `style` HTML**, combinées à des **sélecteurs d’attribut CSS**. Cela permet d’éviter la gestion fastidieuse des noms de classes et d’apporter une plus grande flexibilité et clarté au balisage CSS.

---

## Caractéristiques

* **Aucune étape de compilation requise :**
  Aucune dépendance, aucun build. C’est du CSS pur (Vanilla CSS).

* **Courbe d’apprentissage faible grâce à une convention de nommage simple :**
  Il suffit d’encadrer le nom de la propriété avec `--` dans l’attribut `style`. Pas besoin de mémoriser des centaines de classes utilitaires.

  ```html
  <div style="--color--: crimson;"> … </div>
  ```

* **Léger et très extensible :**
  Conçu de façon minimaliste, Selectorize CSS est léger et facilement intégrable dans des systèmes de design ou des styles CSS existants.

  ```html
  <!-- Selectorize CSS + [Open Props](https://open-props.style/) -->
  <div style="--border--: solid var(--border-size-1) var(--gray-1);"> … </div>
  ```

* **Réduction du poids global du CSS :**
  En remplaçant des classes répétitives par des propriétés personnalisées, Selectorize permet de garder un code CSS plus concis et lisible.

  ```html
  <!-- Méthode classique -->
  <style>
    .very-unique-grid-1 { display: grid; grid: …; … }
    .very-unique-grid-2 { display: grid; grid: …; … }
    …
  </style>
  …
  <div class="very-unique-grid-1"> … </div>
  <div class="very-unique-grid-2"> … </div>
  …

  <!-- Avec Selectorize CSS -->
  <div style="--grid--: …;"> … </div>
  <div style="--grid--: …;"> … </div>
  …
  ```

* **Séparation claire entre propriété et valeur :**
  Au lieu de générer des classes telles que `bg-red`, `border-red`, `text-red`, vous séparez les propriétés (`background`, `border-color`, `color`) de leurs valeurs (`crimson`, `blue`, etc.). Résultat : moins de code et meilleure organisation.

  ```css
  /* Méthode classique (<div class="background-pale-red border-red text-red"> … </div>) */
  .background-red { background: crimson; }
  .background-pale-red { background: mistyrose; }
  …
  .border-red { border-color: crimson; }
  .border-pale-red { border-color: mistyrose; }
  …
  .text-red { color: crimson; }
  .text-pale-red { color: mistyrose; }
  …

  /* Avec Selectorize CSS (<div style="--background--: mistyrose; --border-color--: crimson; --color--: crimson;"> … </div>) */
  [style~="--background--:"] { background: var(--background--); }
  [style~="--border-color--:"] { border-color: var(--border-color--); }
  [style~="--color--:"] { color: var(--color--); }
  ```

* **Maintien de la sémantique HTML :**
  L’attribut `class` peut rester sémantique, tandis que les styles purement visuels sont gérés via `style` et des variables CSS, améliorant la lisibilité du HTML.

  ```html
  <!-- Méthode classique -->
  <div class="important text-red text-bolder align-center"> … </div>

  <!-- Avec Selectorize CSS -->
  <div class="important" style="--color--: crimson; --font-weight--: bolder; --text-align--: center;"> … </div>
  ```

* **Surcharge de style flexible sans `!important` :**
  Les propriétés personnalisées permettent une surcharge naturelle des styles sans recourir à `!important`, ce qui simplifie les ajustements.

  ```css
  /* Méthode classique (<div class="example" style="color: goldenrod;"> … </div>) */
  .example { color: crimson !important; }

  /* Avec Selectorize CSS (<div class="example" style="--color--: goldenrod;"> … </div>) */
  .example { color: crimson; } /* Exemple : changer goldenrod en crimson */
  .example { --color--: crimson; color: var(--color--); } /* Exemple : définir la valeur initiale à crimson pour pouvoir la surcharger via `--color--` dans l’attribut `style` */
  ```

* **Utilisation polyvalente :**
  Que ce soit pour des systèmes de layout entiers ou des ajustements ponctuels sur des composants, Selectorize CSS est souple et puissant.

  ```html
  <!-- Grille de 12 colonnes -->
  <div style="--grid--: auto-flow / repeat(12, 1fr); --gap--: 1rem;">
    <div style="--grid-area--: auto / span 2;"> … </div>
    <div style="--grid-area--: auto / span 4;"> … </div>
    <div style="--grid-area--: auto / span 6;"> … </div>
  </div>

  <!-- Personnalisation d’un bouton -->
  <p style="--text-align--: center;">
    <button class="button" style="--background--: royalblue; --color--: white; --min-inline-size--: calc(100% / 3);"> … </button>
  </p>
  ```

* **Extensions via préfixes :**

  * `--gt-all_PROPERTY-NAME--:` applique le style à tous les enfants directs (`>*`).

    ```html
    <ul style="--flex-flow--: wrap; --gt-all_flex--: auto;"> … </ul>
    ```

  * `--item_PROPERTY-NAME--:` appliqué à `ol`, `ul`, `dl`, `div`, `table`, `tbody`, `thead`, `tfoot`, `tr`, cible les éléments `li`, `dt`, `dd`, `td` ou `th`.

    ```html
    <table style="--item_border--: solid thin; --item_padding--: 0.5rem;"> … </table>
    ```

  * `--dt_PROPERTY-NAME--:` applique un style au `dt` le plus proche.

    ```html
    <dl style="--flex-flow--: wrap; --dt_flex--: 100%;">
      <dt> … </dt>
      <dd> … </dd>
      <dd> … </dd>
      …
    </dl>
    ```

  * `--dd_PROPERTY-NAME--:` cible les éléments `dd`.

    ```html
    <dl style="--flex-flow--: wrap; --dd_flex--: 100%;">
      <dt> … </dt>
      <dt> … </dt>
      <dd> … </dd>
      …
    </dl>
    ```

  * `--before_content--:` insère un contenu via `::before`.

    ```html
    <p style="--before_content--: '👍';"> … </p>
    ```

  * `--after_content--:` insère un contenu via `::after`.

    ```html
    <p style="--after_content--: '😀';"> … </p>
    ```

  * `--cq-CONTAINER-CONDITION_PROPERTY-NAME--:` applique des styles conditionnels via *container queries*. N’oubliez pas de définir `--container-type--` sur l’élément parent.

    ```html
    <ul style="--container-type--: inline-size; --flex-flow--: wrap; --gt-all_flex--: 100%; --gap--: 1rem; --item_background--: ghostwhite; --item_padding--: 1rem;">
      <li style="--cq-i-gt-m_flex--: 1 0 0%;"> … </li>
      …
    </ul>
    ```

Selectorize CSS est conçu pour rester extrêmement minimal. Il suffit de consulter son fichier CSS pour en imaginer les possibilités.

---

## Installation

1. Téléchargez le fichier `selectorize.css` depuis ce dépôt et placez-le dans votre projet.
2. Liez-le dans la balise `<head>` de votre document HTML, **de préférence avant** les autres fichiers CSS :

   ```html
   <link rel="stylesheet" href="chemin/vers/votre/projet/selectorize.css" />
   ```

---

## Contributions

Les suggestions, rapports de bugs et idées d’amélioration sont les bienvenus via les Issues GitHub.
Les contributions via pull request sont également appréciées.

---

## Licence

Ce projet est publié sous licence [www.gnu.org/licenses/gpl-2.0.html](http://www.gnu.org/licenses/gpl-2.0.html)).
Veuillez consulter le fichier `LICENSE` pour plus de détails.








