Traductions : [Japonais](README.md), [Allemand](README.de.md), [Anglais](README.en.md), [Espagnol](README.es.md), [Francais](README.fr.md), [Russe](README.ru.md), [Chinois simplifie](README.zh-CN.md), [Chinois traditionnel](README.zh-TW.md)

Ce README a ete traduit du japonais par [Google Gemini](https://gemini.google.com). Veuillez en tenir compte.

-----

# Selectorize CSS

Un utilitaire CSS leger qui applique des styles en utilisant les proprietes personnalisees CSS comme selecteurs.

-----

## Apercu

Selectorize CSS met en ?uvre une approche de stylisation "utility-first", similaire a Tailwind CSS, en exploitant les **proprietes personnalisees CSS definies dans l'attribut `style` de HTML** et leurs selecteurs d'attributs CSS correspondants. Cela permet un balisage CSS intuitif et flexible sans avoir besoin de gerer les noms de classes.

-----

## Fonctionnalites

  * **Zero compilation :**
    Aucun processus de compilation special n'est requis. Il fonctionne comme du CSS pur (Vanilla CSS).
  * **Faible cout d'apprentissage :**
    Vous pouvez l'utiliser en ecrivant directement les proprietes dans l'attribut `style` de HTML, comme si vous definissiez des styles en ligne. Cela offre une approche de stylisation plus intuitive et novatrice, contrairement au CSS "utility-first" typique qui necessite de memoriser de nombreux noms de classes.
  * **Optimisation de la taille du code CSS :**
    La quantite de code CSS a tendance a augmenter a mesure que vous ajoutez des styles pour des pages ou des elements specifiques d'un site web. Selectorize CSS applique les styles via des proprietes personnalisees predefinies, reduisant ainsi les definitions de classe redondantes et minimisant l'augmentation globale du code CSS.
  * **Separation efficace des proprietes et des valeurs :**
    Il empeche la proliferation courante des definitions de classes redondantes comme "`background-red`", "`border-red`" et "`text-red`" que l'on trouve dans de nombreux frameworks CSS utilitaires. En separant les proprietes (`background`, `border`, `color`, etc.) et les valeurs (`red`, `green`, `blue`, etc.) a l'aide de proprietes personnalisees, il reduit considerablement le nombre de lignes de CSS et simplifie la gestion.
  * **Maintien de la structure HTML semantique :**
    La structure du document HTML et les attributs `class` peuvent se concentrer sur la signification semantique, tandis que les styles visuels non semantiques peuvent etre geres avec l'attribut `style` et les proprietes personnalisees. Cela ameliore la maintenabilite du HTML.
  * **Flexibilite de la surcharge de style :**
    Puisque les proprietes personnalisees sont utilisees a la place de la definition directe des proprietes dans l'attribut `style`, les styles ne sont pas forces, et les surcharges de style peuvent etre effectuees sans utiliser `!important`. Cela permet egalement des ajustements de conception plus flexibles.
  * **Legerete et haute extensibilite :**
    La taille du fichier est legere, car seules les proprietes et fonctions essentielles ont ete selectionnees. Il n'impose pas de composants de conception specifiques, permettant une integration flexible dans les systemes de conception specifiques au projet ou dans le CSS existant.
  * **Scenarios d'utilisation varies :**
    Selectorize CSS peut etre utilise comme un moyen de controler directement la conception et la mise en page principales des pages web, mais il est egalement efficace pour des personnalisations partielles, comme la creation facile de variations de boutons (taille, couleur, etc.) en le combinant avec du CSS ou des composants existants.
  * **Convention de nommage simple :**
    Ajoutez simplement `--` avant et apres le nom de la propriete definie dans l'attribut `style`.
    ```html
    <div style="--color--: var(--red, red);">…</div>
    ```
  * **Extensions basees sur des prefixes :**
    Un style avance est egalement possible en utilisant des prefixes :
      * Definir `--gt-all_PROPERTY-NAME--:` stylise tous les enfants directs (`>*`) de l'element.
      * Definir `--item_PROPERTY-NAME--:` sur `ol`, `ul`, `dl`, `div`, `table`, `tbody`, `thead`, `tfoot`, `tr` stylise leurs enfants immediats `li`, `dt`, `dd`, `td`, `th`.
      * Definir `--dt_PROPERTY-NAME--:` sur `dl`, `div` stylise leurs enfants `dt` immediats.
      * Definir `--dd_PROPERTY-NAME--:` sur `dl`, `div` stylise leurs enfants `dd` immediats.
      * Definir `--before_content--:` ajoute un pseudo-element `::before`.
      * Definir `--after_content--:` ajoute un pseudo-element `::after`.
      * Definir `--cq-CONTAINER-CONDITION_PROPERTY-NAME--:` stylise les elements en fonction de la condition de requete de conteneur specifiee. N'oubliez pas de definir `--container-type--` sur un element ancetre.

-----

## Installation

1.  Telechargez le fichier `selectorize.css` depuis ce depot et placez-le dans votre projet.
2.  Liez `selectorize.css` dans la section `<head>` de votre HTML, de preference avant les autres fichiers CSS :
    ```html
    <link rel="stylesheet" href="path/to/your/project/selectorize.css" />
    ```

-----

## Exemples d'utilisation

L'exemple suivant montre la configuration d'une mise en page en grille. Les elements de la grille avec une taille de base de 240px seront arranges.

```html
<ul style="--grid--: auto-flow / repeat(auto-fit, minmax(min(240px, 100%), 1fr)); --gap--: var(--space_medium, 1rem); --background--: var(--palest-gray, #e0e0e0); --item_padding--: var(--space_large, 2rem);">
  <li>…</li>
  …
</ul>
```

L'exemple suivant montre la configuration d'une mise en page en flexbox. Normalement disposee en une seule colonne verticale, elle passe a une rangee horizontale si la requete de conteneur (cq) pour la taille en ligne (i) est superieure a (gt) la taille M (m).

```html
<ul style="--container-type--: inline-size; --flex-flow--: wrap; --gt-all_flex--: 100%; --gap--: var(--space_medium, 1rem); --background--: var(--palest-gray, #e0e0e0); --item_padding--: var(--space_large, 2rem);">
  <li style="--cq-i-gt-m_flex--: 1 0 0%;">…</li>
  …
</ul>
```

L'exemple suivant ajoute une couleur d'arriere-plan et une couleur de texte a la classe `button`.

```html
<p style="--text-align--: center;">
  <button type="button" class="button" style="--background--: var(--red, red); --color--: var(--white, white);">
    …
  </button>
</p>
```

En definissant une valeur de repli comme `var(--red, red)`, la couleur rouge sera appliquee par defaut meme si `--red` n'est pas defini.
L'exemple suivant montre comment l'utiliser pour etendre une classe `button`.

```css
.button {
  /* Si defini comme <button class="button" style="--background--: var(--red, red);">…</button>, le --background-- suivant sera ecrase. */
  --background--: transparent; /* La couleur d'arriere-plan par defaut est transparente */
  background: var(--background--);
  …
}
```

Alternativement,

```css
.button {
  background: transparent; /* La couleur d'arriere-plan par defaut est transparente */
  …
}
.button[style~="--background--:"] {
  background: var(--background--);
}
```

-----

## Contribution

Les rapports de bugs et les suggestions de fonctionnalites sont les bienvenus via les Issues de GitHub.
Si vous etes interesse par la contribution de code, veuillez envoyer une Pull Request.

-----

## Licence

Ce projet est sous licence [GPL-2.0](https://www.gnu.org/licenses/gpl-2.0.html).
Consultez le fichier `LICENSE` pour plus de details.
