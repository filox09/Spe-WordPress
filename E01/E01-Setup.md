# WORDPRESS : INSTALLATION CLASSIQUE

## Étape 1 : Télécharger WordPress
1. Télchercher le dossier zip sur le site officiel
    - lien de téléchargement : [Wordpress en français](https://fr.wordpress.org/download/)

2. Extraire le dossier
    - via le terminal : `unzip mon-fichier.zip -d destination`
    - via l'interface graphique : clique-droit > extraire

**Remarques**
- Sur la VM, Apache joue le rôle du serveur web.
- Le `document root` c'est la racine du dossier
- La langue de téléchargement de WordPress détermine la langue du Back Office


## Étape 2 : Créer la BDD
1. Aller sur phpMyAdmin
2. Dans `Comptes d'utilisateurs > Ajouter un compte d'utilisateur`, remplir les champs suivants :
- Nom d'utilisateur
- Nom d'hôte
- Mot de passe
- [x] Créer une base portant son nom et donner à cet utilisateur tous le sprivilèges sur cette base

**Remarques**
- Pour le `Nom de l'hôte`, 
    - `tout client` permet l'accès depuis n'importe quel ordinateur
    - `local` permet l'accès seulement depuis le notre
    - on peut y spécifier une ou plusieurs adresses ip


## Étape 3 : Donner les droits d'écriture à Apache
Lorsque la BDD est créée, il faut se rendre via le localhost dans le dossier du projet.

Dès que le fichier ciblé est en PHP, Apache exécute le fichier puis renvoie le résultat.
Or, il ne dispose pas des droits d'écriture nécessaires  à la création du fichier de config. Il faut donc donner ces droits à Apache :
```
sudo chown -R <user>:www-data .
sudo find . -type f -exec chmod 664 {} +
sudo find . -type d -exec chmod 775 {} +
sudo chmod 644 .htaccess
```

**Explication des commandes**
```
sudo chown -R mint:www-data  .
```
- `<user>` : nom d'utilisateur, ici `mint`
- `sudo` : Substitute User DO
- `chown` : CHange OWNer
- `-R` : de manière recursive

```
sudo find . -type f -exec chmod 664 {} +
```
- sélectionne tous les fichiers et applique un `chmod 664`
- [explication chmod 664](https://chmodcommand.com/chmod-664/)

```
sudo find . -type d -exec chmod 775 {} +
```
- sélectionne tous les dossiers 775 et apllique un `chmod 775`
- [explication chmod 775](https://chmodcommand.com/chmod-775/)

**Les droits**
- `r` : read
- `w` : write
- `x` : execute

**Les droits (valeurs numériques)**
- 0 = --- (No Permission)
- 1 = --x (Execute)
- 2 = -w- (Write)
- 3 = -wx
- 4 = r- (Read)
- 5 = r-x
- 6 = rw-
- 7 = rwx

**Lecture des résultats de la commande  `ls -la`**
- Colonne 1 : type de fichiers
    - `d` : directory
    - `l` : link
    - `-` : file
- Colonne 2 : Utilisateur
- Colonne 3 : groupe d'utilisateurs


# Étape 4 :Configuration du site

## Création du site
Renseigner les champs suivants :
- Titre du site
- Identifiant
- Mot depasse
- Adresse mail (en développement mettre une adresse fictive pour ne pas saturer sa boîte mail )
- [x] Demander aux moteurs de recherche de ne pas indexer ce site

## Définir le mode de mise à jour
Dans le fichier wp-config (après la ligne 85), saisir l'instruction suivante :
```php
define('FS_METHOD', 'direct');
```
> Cette fonction indique à WordPress qu'il doit directement télécharger & mettre à jour les fichiers (pas besoin de passer par du SSH ou du FTP)


## Configurer le .htaccess
Par défaut le fichier `.htaccess` contient des régles d'écriture basées sur une url statique. 
On va donc modifier le `.htaccess` pour le rendre universel:
```
RewriteEngine on
RewriteRule ^index\.php$ - [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . index.php [L]
```

:warning: Il faut attribuer les droits d'écriture à Apache sur les fichiers crées à la suite de l'installation.
```
sudo chown -R <user>:www-data .
sudo find . -type f -exec chmod 664 {} +
sudo find . -type d -exec chmod 775 {} +
sudo chmod 644 .htaccess
```

# Informations supplémentaires
## Page vs articles

Les articles sont des contenus non-hiérachiques. On ne peut pas les relier directement entre eux. Si on veut les relier, il faut utiliser les taxonomies.

Les pages sont des contenus hiérarchiques. 

## Astuces
### 1. Modifier les identifants de l'administrateur
- Aller sur PMA
- Modifier la mdp
- Sélectionner `MD5` dans la colonne `fonction`
- Exécuter

WordPress rechiffrera le mot de passe avec un algo de cryptage plus sécurisé !

### 2. Modifier `siteurl` et `home`
Dans la BDD associée au porjet WP, la table wp-option nous permet de redéfinir `siteurl` et `home`. C'est ce qui sert à la génération des `permaliens`.

### 3. Gestions des permaliens
Pour modifier le format d'affichage des permaliens, il faut se rendre sur le Back Office de WP, aller dans `Réglages > Permaliens`.

:warning: Dès qu'on modifie les permaliens, WP re-génère un fichier `.htaccess`.

Le fichier `.htaccess` est un fichier de configuration d'Apache. On l'utilise notamment pour la récriture d'url (url rewriting), la redirection, et bloquer l'accès au fichier `app` (dans nos projets précédents).



# Quiz

1. Que signifie CMS
    - content management system
2. Quel est le fichier qui permet de configurer WordPress ?
    - wp-config.php
3. le codex c'est...
    - la bible de wordpress by automattic (la documention officiel de wordpress)
4. wordpress.com c'est le site sur lequel on trouve...
    - de quoi avoir un wordpress hébergé par automattic

**Remarques**
- Le fichier `index.php` est un point d'entrée et fait un peu office de front controller
- Le fichier `.htaccess` permet de donner des instructions, paramétrer, configurer à Apache