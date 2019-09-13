# Sass
Syntactically Awesome Style Sheets

## Intro
### Principe
- Le moteur Sass va compilé des fichiers .scss ou .sass et ainsi transformé en CSS valide.
Sass est à la fois le moteur et le nom de la syntaxe.

### Carcatéristiques
- 1 moteur de base : Sass (développé en Ruby) 
    - porté  en C/C++ : LibSass
    - porté en node.js : node-sass

- 2 syntaxes : 
    - Sass
    - SCSS


## Installer le moteur node-sass
```
npm i node-sass -D
```
**Remarque**
- `npm i node-sass -D` équivaut à `npmi i node-sass --save-dev`

# Syntaxe
## Variables
**Quelques exemples**
```scss
$variable: 'initial value';

$direction: 'left';
$font-type: sans-serif;

$length: 0; // pas besoin de préciser les unités pour les longeurs uniquement /!\

$value: 42;
$length: $value * 1px;
```

## Couleurs
```scss
$color : rgb(42, 42, 42);

mix(white, $color, $percentage);
mix(black, $color, $percentage);
```

## Listes et maps
```scss
// liste (similaire aux tableaux indexés)
$font-stack: ('Helvetica', 'Arial', sans-serif);

// map (similaire aux tableaux associatifs)
$breakpoints: (
  'small': 767px,
  'medium': 992px,
  'large': 1200px,
);
```

## Imbrication des sélecteurs
```scss
.form {
    &-register {// Ici, & = ".form"

        &__email {// Ici, & = ".form-register"

            &:hover { // Ici, & = ".form-register__email"
                background-color: darken($color-green, 15%);
            }
        }
    }
}
```

**Rappels**
- `&` reprend le nom du parent
- BEM
    - ciblage des éléments en fonction de leurs classes
    - enfants(`__`), modifiers (`--`)


# Architecture 
[Doc Sass archticture](https://sass-guidelin.es/fr/#architecture)

Dorénavant, on va travailler dans un dossier `app`.
Le dossier `assets` contiendra tout ce qui ne sera pas modifié, compilé.

**Structure du dossier `app`**
```
-app
    - /assets
        - index.html
    - /js
        - app.js
    -scss
        - main.scss
```


**Remarques**
- Normalement pour exécuter le script `start` il faut taper `npm run start`, mais il existe un raccourci : `npm start`


## @import

L'utilisation de `@import` pour l'import de feuilles de style n'est pas recommandé car le temps de chargement des pages est rallongé.

Sass est exécuté côté serveur, on peut donc tout a fait utiliser `@import` en Sass car à la fin toute sles feuilles de style seront compilées sur le même fichier `.css`. Et seul ce fichier sera chargé pa le navigateur.

:warning: Sass est exécuté côté serveur !

À terme, toutes les feuilles de style seront importées sur `main.scss`

**Norme d enommage**
- un fichier rimporté à toujours un undescore `_` devant (ex: `_test.scss`)

##  Le pattern 7-1
Ce pattern est un outil, il n'est en rien contraignant. On peut l'adpater à nos besoins !

Dans notre cas par exemple, le dossier `vendors` est inutile. On se retoruve alors avec un patterne 6-1.

### Structure de base
```
sass/
|
|– abstracts/
|   |– _variables.scss    # Sass Variables
|   |– _functions.scss    # Sass Functions
|   |– _mixins.scss       # Sass Mixins
|   |– _placeholders.scss # Sass Placeholders
|
|– base/
|   |– _reset.scss        # Reset/normalize
|   |– _typography.scss   # Typography rules
|   …                     # Etc.
|
|– components/
|   |– _buttons.scss      # Buttons
|   |– _carousel.scss     # Carousel
|   |– _cover.scss        # Cover
|   |– _dropdown.scss     # Dropdown
|   …                     # Etc.
|
|– layout/
|   |– _navigation.scss   # Navigation
|   |– _grid.scss         # Grid system
|   |– _header.scss       # Header
|   |– _footer.scss       # Footer
|   |– _sidebar.scss      # Sidebar
|   |– _forms.scss        # Forms
|   …                     # Etc.
|
|– pages/
|   |– _home.scss         # Home specific styles
|   |– _contact.scss      # Contact specific styles
|   …                     # Etc.
|
|– themes/
|   |– _theme.scss        # Default theme
|   |– _admin.scss        # Admin theme
|   …                     # Etc.
|
|– vendors/
|   |– _bootstrap.scss    # Bootstrap
|   |– _jquery-ui.scss    # jQuery UI
|   …                     # Etc.
|
`– main.scss              # Main Sass file
```
**remarques**
- Un composant est un tout petit élément dans la page.
- Le fichier principal est généralement nommé `main.scss`

- L'ordre d'import doit être respecté
    1. abstracts/
    2. vendors/
    3. base/
    4. layout/
    5. components/
    6. pages/
    7. themes/

### Bonnes pratiques
#### Option 1
- un fichier par @import
- un @import par ligne
- pas de saut de ligne entre 2 imports provenant du même dossier
- un saut de ligne après le dernier import d’un dossier
- les extensions fichiers et les underscores initiaux doivent être omis
```
@import 'abstracts/variables';
@import 'abstracts/functions';
@import 'abstracts/mixins';
@import 'abstracts/placeholders';

@import 'vendors/bootstrap';
@import 'vendors/jquery-ui';
```

#### Option 2
- un @import par dossier
- retour à la ligne après @import
- chaque fichier sur sa propre ligne
- un saut de ligne après le dernier import d’un dossier
- les extensions fichiers et les underscores initiaux doivent être omis
```
@import
  'abstracts/variables',
  'abstracts/functions',
  'abstracts/mixins',
  'abstracts/placeholders';

@import
  'vendors/bootstrap',
  'vendors/jquery-ui';
```

**Remarques**
- :warning: Le globbing n'est pas conseillé car on perd la maitrise sur ce qui est importé et sur l'ordre d'importation !
- Le fichier de la honte `_shame.scss`doit être mis à la racine 

# Extend
(à compléter)

# Mixins
(à compléter)
similaire aux fontion

# Conditions
(à compléter)

# Boucles
(à compléter)
utile pour parcourir les tableaux