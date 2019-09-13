# Le fichier de config de wordpress
- [Doc wp-config](https://wordpress.org/support/article/editing-wp-config-php)
- [Doc wp_debug](https://wordpress.org/support/article/editing-wp-config-php/#wp_debug)


## Configuration de la BDD
```php
/** Nom de la base de données de WordPress. */
define( 'DB_NAME', 'wp_two' );

/** Utilisateur de la base de données MySQL. */
define( 'DB_USER', 'wp_two' );

/** Mot de passe de la base de données MySQL. */
define( 'DB_PASSWORD', 'two' );

/** Adresse de l’hébergement MySQL. */
define( 'DB_HOST', 'localhost' );

/** Jeu de caractères à utiliser par la base de données lors de la création des tables. */
define( 'DB_CHARSET', 'utf8mb4' );

/** Type de collation de la base de données.
  * N’y touchez que si vous savez ce que vous faites.
  */
define('DB_COLLATE', '');
```

```php
/**
 * Préfixe de base de données pour les tables de WordPress.
 */
$table_prefix = 'wp_';
```


## Clés d'authentification et salage
```php
define( 'AUTH_KEY',         'MM$r<O)(Gf92b{!`THUh+;m}{4;VbmmG/}h-r2x}/y{ye=,zNRqCX,j#kB2f;[aP' );
define( 'SECURE_AUTH_KEY',  '_4<~fwchn9p>n]HPh2RbSw,a/9|y:Z|`~KIy,}rMEo8.gz8wF)nN=+D/.J-<BEq2' );
define( 'LOGGED_IN_KEY',    '@J=gSgljc#Ct=CN_EzvabmQ]3?<*y}.P^mA-h@F`_XN)4xc^{b`ll-41k4ma`D#n' );
define( 'NONCE_KEY',        'FTK&0$)EFqO^]/KxGYO4c=01[AvOZK~Y2k;RicW!>,VN&KLz{wqQxC(z-^YgF(RD' );
define( 'AUTH_SALT',        '*-8 PVB<1p+@iXK%s}QD,w!e>DnPHTp0C^MQMH+p~~n5#Nql.yO#1P>LwzKV!}_5' );
define( 'SECURE_AUTH_SALT', '#D8B3Xg2:x5IzKo`2eW UiMm^?,n/|`jTd#v7M5@`t%v<EA;yi+;2I;<kbsne#(a' );
define( 'LOGGED_IN_SALT',   'Xkr-bOS18#zg1Nl=AfBEm?BzFoZ-^Y`/cAd`uL,!k+.1+K*YUYS<gWq*xm<MJQu=' );
define( 'NONCE_SALT',       'a~d@TO+XuNbCe>c%qa#VZ^g++{6[b#cPh#pYqSfy&!rqK`fnw(M?+~T[jO59^6Xg' );
```

Les cookies sont des fichiers qui contiennet des informations de session. (l'identifiant de session, par exemple). WP a donc mis en place un système de salage pour chiffrer ce qui va être stocker côté navigateur.

:warning: Le changement de ces clés provoquent la déconnexion immédiate de tous les utilisateurs connectés sur le site.
Cela peut être utile si on veut des changement dans le fonctionnement du site pour ce qui est de la gestion des utilisateurs.


## Le mode déboguage de WordPress

### Pour PHP
- Débug de Wordpress
```php
/** En passant la valeur suivante à "true", vous activez l’affichage des notifications d’erreurs pendant vos essais.  */
define('WP_DEBUG', false);
```

- Affichage des erreurs PHP/WordPress directement dans le code HTML
```php
define('WP_DEBUG_DISPLAY', true);
```

- Enregistrement des erreurs PHP/WordPress dans un fichier de logs
```php
define('WP_DEBUG_LOG', true);
```

Le fichier d'rreur va se trouver dans le dossier wp-content, à la racine.

### Pour CSS et JS
- Activation du débug de WordPress 
```php
define('SCRIPT_DEBUG', true);
```


## Désactiver l'éditeur de thème du Back Office
Pour désactiver l'éditeur de thème (`Apparence > Éditeur de thème`) inclus par WP :
```php
define( 'DISALLOW_FILE_EDIT', true );
```

## Désactiver l'installation de plugins et de thèmes
```php
define('DISALLOW_FILE_MODS', true);
```
:warning: Pratique lorsque le site est en prod (mais pas en situation de dev)

## Paramétrer les révisions
Accéder aux révisions sur le Back Office : Articles > Article X > Document > X révisions

Par défaut, les révisions sont illimités. On peut les désactiver ou en limiter leur nombre.

```php
define('WP_POST_REVISIONS', 5);
```
**Remarques**
WordPress se charge de faire le tri entre les révisons de ne conserver que les plus pertinentes.

# Gérer l'environnement

Définir l'environnement
```php
// define( 'ENVIRONMENT', 'development' );
// define( 'ENVIRONMENT', 'staging' );
define( 'ENVIRONMENT', 'production' );
```
Conditionner le mode débug
```php
if ( defined( 'ENVIRONMENT' ) ) { // Je vérifie que la constante ENVIRONMENT existe
    if ( ENVIRONMENT === 'development' ) {
        define( 'WP_DEBUG', true );
        define( 'WP_DEBUG_DISPLAY', true ); // Affichage des erreurs PHP/WordPress directement dans le code HTML
        define( 'WP_DEBUG_LOG', false );
        define( 'DISALLOW_FILE_MODS', false ); // Activation de l'ajout des fichiers de traduction, thèmes et plugins
        define( 'FS_METHOD', 'direct' ); // Activation du téléchargement direct des fichiers de traduction, plugins et thèmes
        define( 'WP_POST_REVISIONS', false ); // Désactivation du sytème de révions des contenus
        define( 'SCRIPT_DEBUG', true ); // Activation du débogage des CSS et JS de WordPress
        define( 'EMPTY_TRASH_DAYS', 0 ); // Désactivation de la corbeille
    } elseif ( ENVIRONMENT === 'staging' ) {
        define( 'WP_DEBUG', true );
        define( 'WP_DEBUG_DISPLAY', false );
        define( 'WP_DEBUG_LOG', true ); // Ecriture des erreurs PHP/WordPress dans un fichier de log
        define( 'DISALLOW_FILE_MODS', true ); // Désactivation de l'ajout et des mises à jour des thèmes et plugins dans le backoffice
        define( 'WP_POST_REVISIONS', 10 ); // Limitation du nombre de révions des contenus
        define( 'SCRIPT_DEBUG', false );
        define( 'EMPTY_TRASH_DAYS', 60 ); // Limitation du nombre de jours de conservation des contenus dans la corbeille
    } elseif ( ENVIRONMENT === 'production' ) {
        define( 'WP_DEBUG', false );
        define( 'WP_DEBUG_DISPLAY', false );
        define( 'WP_DEBUG_LOG', true );
        define( 'DISALLOW_FILE_MODS', true );
        define( 'WP_POST_REVISIONS', 10 );
        define( 'SCRIPT_DEBUG', false );
        define( 'EMPTY_TRASH_DAYS', 60 );
    } else {
        echo 'La valeur de la constante ENVIRONMENT n\'est pas valide. Les valeurs possibles sont development, staging ou production.';
        exit;
    }
} else {
    echo 'La constante ENVIRONMENT n\'est pas définie.';
    exit;
}
```

```php
define( 'DISALLOW_FILE_EDIT', true ); // Désactivation de l'éditeur embarqué de thèmes et plugins
define( 'AUTOMATIC_UPDATER_DISABLED', true ); // Désactivation des mises à jour automatiques de WordPress
define( 'WP_AUTO_UPDATE_CORE', false ); // Désactivation des mises à jour du cœur de WordPress
```

```php
/*
Sachant que WordPress ne nous permet pas de gérer l'environnement dans lequel est exécuté notre WordPress, nous mettons la fonctionnalités en place nous-même en créant une constante qui n'est comprise que pas notre code.
*/
// define( 'ENVIRONMENT', 'development' );
// define( 'ENVIRONMENT', 'staging' );
define( 'ENVIRONMENT', 'production' );
/**
 * Additionnal configuration constants
 *
 * @link https://wordpress.org/support/article/editing-wp-config-php
 */
if ( defined( 'ENVIRONMENT' ) ) { // Je vérifie que la constante ENVIRONMENT existe
    if ( ENVIRONMENT === 'development' ) {
        define( 'WP_DEBUG', true );
        define( 'WP_DEBUG_DISPLAY', true ); // Affichage des erreurs PHP/WordPress directement dans le code HTML
        define( 'WP_DEBUG_LOG', true );
        define( 'DISALLOW_FILE_MODS', false ); // Activation de l'ajout des fichiers de traduction, thèmes et plugins
        define( 'FS_METHOD', 'direct' ); // Activation du téléchargement direct des fichiers de traduction, plugins et thèmes
        define( 'WP_POST_REVISIONS', 3 ); // Désactivation du sytème de révions des contenus
        define( 'SCRIPT_DEBUG', true ); // Activation du débogage des CSS et JS de WordPress
        define( 'EMPTY_TRASH_DAYS', 5 ); // Désactivation de la corbeille
    } elseif ( ENVIRONMENT === 'staging' ) {
        define( 'WP_DEBUG', true );
        define( 'WP_DEBUG_DISPLAY', false );
        define( 'WP_DEBUG_LOG', true ); // Ecriture des erreurs PHP/WordPress dans un fichier de log
        define( 'DISALLOW_FILE_MODS', true ); // Désactivation de l'ajout et des mises à jour des thèmes et plugins dans le backoffice
        define( 'WP_POST_REVISIONS', 10 ); // Limitation du nombre de révions des contenus
        define( 'SCRIPT_DEBUG', false );
        define( 'EMPTY_TRASH_DAYS', 60 ); // Limitation du nombre de jours de conservation des contenus dans la corbeille
    } elseif ( ENVIRONMENT === 'production' ) {
        define( 'WP_DEBUG', false );
        define( 'WP_DEBUG_DISPLAY', false );
        define( 'WP_DEBUG_LOG', true );
        define( 'DISALLOW_FILE_MODS', true );
        define( 'WP_POST_REVISIONS', 10 );
        define( 'SCRIPT_DEBUG', false );
        define( 'EMPTY_TRASH_DAYS', 60 );
    } else {
        echo 'La valeur de la constante ENVIRONMENT n\'est pas valide. Les valeurs possibles sont development, staging ou production.';
        exit;
    }
} else {
    echo 'La constante ENVIRONMENT n\'est pas définie.';
    exit;
}
define( 'DISALLOW_FILE_EDIT', true ); // Désactivation de l'éditeur embarqué de thèmes et plugins
define( 'AUTOMATIC_UPDATER_DISABLED', true ); // Désactivation des mises à jour automatiques de WordPress
define( 'WP_AUTO_UPDATE_CORE', false ); // Désactivation des mises à jour du cœur de WordPress

/* C’est tout, ne touchez pas à ce qui suit ! Bonne publication. */
```
:warning: Penser à le mettre dans le fichier wp-config.sample
Mettre le fichier config dans le gitignore