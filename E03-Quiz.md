# Quiz : npm et Sass

## 1. Pour exécuter un script présent dans package.json je doit saisir
> `npm run <mon script>`
- si le script s'appelle satrt on peut faire npm start

## 2. (avec npm) Mes dépendances sont chargée où dans mon projet
> Dans le dossier `node_modules`

## 3. browser-sync via npm est une dépendance...
> Oui mais de développement

**Remarques**
- On distingue les `devDependencies` (dépendances de dev) des `dependencies` (dépendances de projet) car les `devDependencies` ne sont pas utiles en prod. 
- Le script `build:prod` génère un dossier `public` avec les dépendances de projet.
- En général, lors de la mise en ligne, on installe pas npm sur le serveur de prod. On envoie le dossier `public` tel quel (il a été compilé au préalable).

## 4. jQuery via npm est une dépendance...
> Oui mais de projet

## 5. bootstrap via npm est une dépendance...
> Oui mais de projet

## 6. Un watcher-builder d'assets en pipeline c'est...
> Un outil qui surveille nos fichiers, exploite des plugins et construit à la volée notre dossier public

## 7. Le SASS est un language de...
> Génération de feuille de style qui s'excute sur le serveur

**remarque :** la feuille de style générée par sass est exécuté côté navigateur

## 8. Le pré-processeur SASS...
> Génère des fichiers .css à partir de fichiers .sass et .scss 

## 9. Les fichiers .scss
> Ont la même syntaxe que les fichiers .css

**Remarque**
- En revanche les fichiers .sass ont une syntaxe dérivée de ruby