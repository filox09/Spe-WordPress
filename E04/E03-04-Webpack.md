#WP-Pattern-Webpack
La commande `npm build:dev` est très peu utilisée car on utilise soit `npm run start` ou `npm run build`.

**Bref aperçu des dépendeances dev**
```
"autoprefixer": "^9.6.1", // ajouts des préfixes -moz, -ms
"browser-sync": "^2.26.7", // synchronisation des navigateurs
"node-sass": "^4.12.0", // moteur sass
"uglifyjs-webpack-plugin": "^2.2.0", // minifieur de js
```

# Installer webpack (première installation)
Installer n en global
```
sudo npm install -g n
```
`n` est un outil qui permet de changer la version de node.js

pour connaitre la version de node.js
```
node -v
``` 

télécharger la nouvelle version de node (en lts)
```
sudo n lts
```

checker la version

faire
```
sudo npm install -g webpack webpack-cli webpack-dev-server
```

supprimer le cache de npm pour s'assurer que les éléments téléchargés sont bons
```
sudo npm cache clear --force
```

puis 
```
npm install
```

puis
``` 
npm run start
```