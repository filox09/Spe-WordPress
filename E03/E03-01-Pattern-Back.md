# Utilisation du pattern
- Pour créer un pattern back (cf. E02-03)

### 1. Mise en place du projet
#### Repo non existant
1. Cloner le repo du pattern
2. Renommer le dossier avec le nom du projet
    - `mv <ancien nom> <nouveaunom>`
3. Se rendre dans le nouveau dossier `cd <nouveau nom>`
4. Supprimer le fichier `.git` (pour délier le nouveau dossier du repo d'origine)
    - `sudo rem -R .git`
5. Initialiser git dans le dossier du projet `git init`

#### Repo existant
1. Cloner le repo du pattern
2. Copier/Coller les élements du pattern dans le repo du nouveau projet (sauf le `.git` et le `README.md`)

### 2. Relier la BDD au projet
Pour cela on va modifier le fichier `wp-config.php` et `wp-config-sample.php` :
1. renseigner les informations de connexion à la BDD
2. e-générer les clés de salage [lien](https://api.wordpress.org/secret-key/1.1/salt/)
3. spécifier la valeur de la constante `WP_CONTENT_URL` avec notre url locale

### 3. Changer les droits des dossiers/fichiers du projet
```
sudo chown -R <user>:www-data .
sudo find . -type f -exec chmod 664 {} +
sudo find . -type d -exec chmod 775 {} +
sudo chmod 644 .htaccess
```

### 4. Se rendre sur l'url local du projet
1. Paramétrer les urls (paramètres > général)
2. Paramétrer les permaliens (paramètres > permaliens)

**Remarques**
- Wordpress s'est rendu compte que dans le wp-config on lui avait spécifié comment télécharger les fichiers. Grâce à cela et car il a les droits de téléchargement des fichiers, il propose le choix de la langue dès l'instatllation.
- La barre d'amin n'apparait plus sur le site
    - le cookie n'est plus bon car on a changé l'url 
    - il suffit de se déco,nnecter puis de se reconnecter