# oBlog
[Repo](https://github.com/O-clock-Universe/WP-Atelier-oBlog-christopheOclock)

# Les étapes
## Étape 1 : Cloner le repo
```
git clone <repo>
```
## Étape 2 : Récupérer le pattern et le coller dans le repo
- Copier puis coller les éléments du pattern Webpack à lexception du `README.md` et du `package-lock.json`.

## Étape 3 : Installer les dépendances nécessaires
### Les dépendances
- `reset-css`
- `font-awesome`

### Installer les dépendances

### Étape 1 : Installation en ligne de commande
Dans le terminal, saisir les commandes suivantes:
```
npm i font-awesome
npm i reset-css
```

### Étape 2 :  Import des dépendances
Dans le fichier `main.scss` faire l'import des dépendances
```scss
@import
    '~reset-css/sass/reset',
    '~font-awesome/scss/font-awesome'
```

**Remarques**
- :warning: Normalement avec le pattern 7-1, le dossier `vendors` est le 2ème dossier à importer. Mais comme nous utilisons NPM afin de gérer nos dépendances, les `vendors` (c'est-à-dire nos dépendances) se trouvent dans le dossier `node_modules`.
On va donc demander à `node-sass` d'importer nos vendors depuis le dossier `node_modules`.
- `~` est un alias (raccourci) vers le répertoire `node_modules/`


#### :warning: __Sauf que pour font-awesome c'est un peu plus compliqué que ça !__

### Le cas font-awesome

1. Installer `file-loader`
On va donc installer `file-loader` en dépendance de dev. Il se chargera de gérer `font-awesome` pour nous.
```
npm i -D file-loader
```

2. Configurer webpack
Cette configuration sera utile en en prod comme en dev. 
Il faut copier les instructions suivantes dans les 2 fichiers de config.
```json
// Gestion des fonts
      {
        test: /\.(woff(2)?|ttf|eot|svg)(\?v=[0-9]\.[0-9]\.[0-9])?$/,
        use: {
          loader: 'file-loader',
          options: {
            name: '[name].[ext]',
            outputPath: 'fonts/', // Je veux copier les fichiers de fonts dans le répertoire public/fonts
            publicPath: '../fonts' // J'informe à mon code CSS (dans css/style.css) que les polices de caractères seront dans le répertoire ../fonts
          }
        },
      },
```

3. Définir `$font-path` dans `abstratcs/variables`
En sass c'est la première déclaration de varaible qui gagne. On peut donc redéfinir `$font-path` dans `abstratcs/variables`.
Si on oublie cette étape, l'import ne pourra pas avoir lieu car le chemin n'est pas bon.

**Remarques**
- Pour être sur d'avoir le bon nom d'icon, se référérer à la [Libraire Font-Awesome v4.7.0](https://fontawesome.com/v4.7.0/icons/)

- Toutes les icones de font-awesome sont des caractères spéciaux. On peut donc utiliser les mêmes propriétés que pour une police.


# Supprimer une dépendance
(du packet package.json, package-lock.json et node-modules)
```
npm uninstall <nom de la dépendance>
```

# L'intégration
## Les étapes
1. Découper le design en layout et components 
2. Faire la structure html
3. Faire le css
    - de haut en bas
    - de gauche à droite
    - du général (html>body) au particulier (layout>component)
4. Admirer son magnifique travail

## Recommandations et bonnes pratiques
- En langage BEM un component est un block à part entière
- Une nav n'est rien d'autre qu'une liste de liens
- Placer le contenu important en premier.
  - ici, on va placer la balise article avant l'aside 
  - on pourra gérer l'ordre avec un order préférablement (ou un row reverse, moin recommandé)
- Définir les couleurs, les polices, les tailles de polices, vitesses de transition, largeurs pour les media queries, ou tout autres éléments pertinent dans des variables (`abstracts/_variables.scss`)

## Remarques
- Il n'est pas possible de déterminer la largeur de l'underline (text-decoration: underline)

### Exemple
### 1. Variables 
```scss
/* Website colors */
$yellow:rgb(255, 236, 0);
$dark-grey: rgb(28, 29, 31);
$light-grey: rgb(245, 246, 248);

/* Color attribution */
$main-color: $yellow;
$text-color: $dark-grey;
$background-color: $light-grey;

/* Typo */
$font-familly: ('Montserrat', sans-serif);
$fallback-font-familly: (Arial, Helvetica, sans-serif);

/* Typo sizes */
$default-font-size: 16px;
$medium_font-size: 18px;
```

#### 2. Champ de recherche
Le label est une indication pour un élément de formulaire. Il permet de "focus" sur le champ lorsqu'on clique sur le label.
```html
<div class="search">
    <form action="" class="search__form">
    <label for="search" class="search__form__label">
        <i class="fa fa-search" aria-hidden="true"></i>
    </label>
    <input type="text" name="search" id="search" class="search__form__input">
    </form>
<div>
```

## Symboles
- point noir : `&bull`;
- copyright : `&copy`;