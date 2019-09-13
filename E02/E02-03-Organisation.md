# Réorganiser le dossier

1. Dans le dossier du projet (`two`), créer un dossier `wp` qui contient l'entièreté des fichiers WordPress

2. Récupérer/crée les fichiers suivants et les mettre à la racine :
    - `index.php`
    - `wp-config.php`
    - `wp-config-sample.php`
    - `.htaccess`

3. Mettre le fichier `.gitignore` à la racine et y inscrire :
    - `wp/`
    - `vendor/`
    - `wp-config.php`
    - `content/*`
    - `!content/themes` ()
    - `content/themes/*`
    - `!content/themes/monsupertheme`

4.  Modifier le `require()` présent dans `index.php` 
```php
// original
require( dirname( __FILE__ ) . '/wp-blog-header.php' );

// après modification
require( dirname( __FILE__ ) . '/wp/wp-blog-header.php' );
```

5. Modifier la BDD
    - se rendre dans la table `wp-options` et modifier la colonne `siteurl` : http://localhost/oclock/spe/two/wp


6. Dans `wp-config.php` (et `wp-config-sample.php`), spécifier à WordPress sur quelle url se trouve le dossier `content`
```php
define('WP_CONTENT_URL', '{chemin}/content');
define( 'WP_CONTENT_DIR', dirname( ABSPATH ) . '/content' );
```

7. Faire `composer init` puis `composer require johnpbloch/wordpress`

8. Modifier le fichier composer.json
```json
{
    "repositories": [
        {
            "type": "composer",
            "url": "https://wpackagist.org"
        }
    ],
    "require": {
        "johnpbloch/wordpress": "^5.2",
        "wpackagist-theme/twentynineteen": "*",
        "wpackagist-plugin/hello-dolly": "*"
    },
    "extra": {
        "wordpress-install-dir": "wp",
        "installer-paths": {
            "content/plugins/{$name}/": ["type:wordpress-plugin"],
            "content/themes/{$name}/": ["type:wordpress-theme"]
        }
    }
}

```

9. Supprimer les dossiers ``wp`, `content`, `vendor` et `wordpress`

10. Faire `composer install`, puis `composer require`

11. Donner les droits de fichiers à Apache (pour pouvoir changer la langue sur le BO)
```
sudo chown -R <user>:www-data .
sudo find . -type f -exec chmod 664 {} +
sudo find . -type d -exec chmod 775 {} +
sudo chmod 644 .htaccess
```

## Arborescence finale
- Projet
    - /content
    - /wp
    - index.php
    - wp-config.php
    - wp-config-sample.php
    - .htaccess
    - .gitignore
    - composer.json
    - composer.lock


## Modification à apporter dans la BDD
siteurl : option qui précise à wp sa localisation 
http://localhost/oclock/spe/two/wp

home : option qui précise à wp l'url de la page d'acceuil
http://localhost/oclock/spe/two

## Remarques
- Cette architecture permet de faire de WordPress une librairie
- Si je fais la modification du mon fichier composer.json après le composer install il faut que je signale les modification à composer avec la commande `composer update`
    - sinon il faudra faire `composer require` pour récupérer les thèmes et les plugins

2. GIT
    - Git ne versionne QUE les fichiers
    - Si un dossier est vide, git ne le versionne pas.
        - `.keep` permet de versionner un dossier vide

3. Thèmes pardéfaut
Il est indispensable d'avoir le dernier thème par deféaut de WP (`twentynineteen`)

# Ressources
https://packagist.org/packages/johnpbloch/wordpress
https://wpackagist.org/
https://github.com/O-clock-Alumni/fiches-recap/blob/master/wordpress/wp/installation-custom.md