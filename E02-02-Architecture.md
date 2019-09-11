# Architecture de WordPress
- [Fiche récap : WP core load](https://github.com/O-clock-Alumni/fiches-recap/blob/master/wordpress/medias/wordpress_core_load.png)

## index.php
Toutes les requêtes du front sont redirigées sur `index.php`.
`index.php` déclare une constante et vient charger le ficher `wp-blog-header`.

## wp-blog-header.php
`wp-blog-header.php` vérifie que la variable `$wp_did_header` a été déclarée puis il charge `wp-load.php`.

## wp-load.php
`wp-load.php` déclare une constante `ABSPATH` (si ça n'est pas le cas).
Il charge `wp-config.php`, si il existe. Sinon, WP considère qu'il s'agit d'un nouvelle installation (on est donc redirigé vers setup-config.php, le fichier qui gère l'installation)

## wp-config.php
`wp-config.php` déclare les constantes en rapport avec la BDD. 
Il vérifie si `ABSPATH` a été déclarée et se charge de lancer `wp-settings.php`.

## wp-settings.php
`wp-settings.php` définit la constante `WPINC`.
C'est le _fichier HUB_ de WordPress, il se charge de charger tous un tas de fichiers.

## wp-admin (dossier)
Toutes les requêtes faites sur le Back Office sont redirigées sur `wp-admin`.

## wp-include (dossier)
Ce dossier contient toutes les classes de WordPress. C'est le coeur de WordPress.

## wp-content (dossier)
On y trouve les plugins (`/plugins`), les thèmes (`/themes`), les media (`/uploads`), les traductions (`/laguages`), les mises-à-jour (`/upgrade`)

**remarque**
-  WordPress télécharge le fichier de MAJ (zip), puis applique la maj, et supprime le ficheir la mise à jour réalisée.


## La base de données
Pour chaque type de contenu, WordPress stocke les informations principales dans une première table puis les méta-informations dans une seconde.
