# Les watcher (cf. E02)
(à compléter)

# Les builder

## Créer un builder de  css
1. Créer un script qui va se charger de compiler notre fichier .scss ou .sass
```
"build-css": "node-sass --output-style compressed scss/style.scss css/style.css"
```
- `scss/style.scss` : fichier source
- `css/style.css` : destination

2. Exectuer le script
```
npm run build-css
```

# Les watcher-builder
Les watcher-builder sont des scripts qui se charge d'excuter d'autres scripts.
Dans notre cas, ce sont des watcher-builder d'assets car ils génèrent des fichiers css.


