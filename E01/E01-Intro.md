[Programme de la spé](https://github.com/O-clock-Alumni/fiches-recap/blob/master/wordpress/programme.md)

## Fiche récap
[Ressources](https://github.com/O-clock-Alumni/fiches-recap/blob/master/wordpress/wp/ressources.md)

# Découverte de WordPress

WordPress est un CMS, sun sytème de gestion de contenus.

- wordpress.org : toute la partie open source de WordPress (documentation, code source, forum, etc)
- wordpress.com : partie commerciale (création de site wordpress)

## Avantages des CMS
Les CMS permettent de :
- Gérer des contenus dynamiquement
    - Dans WorPress, tout ce que qu'on enregistre est considéré comme du contenu (article, page, media, commentaire , utilisateur)
- Structurer et hiérachiser des contenus et documents
    - les taxonomies
- séparer les opérations de gestion de forme et de contenu
    - forme : thème (affichage du contenu)
    - contenu : article, page, etc (via le BO)
- gérer des versions de contenu 
    - similaire à GitHub
- D'accéder à  un workflow de gestion (création, édition, relecture, publication)
- Permet d'attribuer des rôles et des persmissions aux utilisateurs
    - administrateur, editeur, auteur, contributeur, abonné
    - possibilité des créer des rôles (si ceux par défaut ne sont pas suffisant)
    - les différents rôles utilisateur ([lien](https://yesyouweb.com/wordpress-differents-roles-utilisateurs/))


## Plugins
Les plugins permettent de rajouter une fonctionnalité à WordPress sansmofifier le code source de wp

## Gutenberg 
Gutenberg exploite la REST API de Wordpress

### API vs REST API
- API
    - Interface de programmation applicative
    - Url sur lesquelles ont va pouvoir accéder à du contenu 

- REST API
    - Une REST API se doit d’être sans état ou stateless en anglais : la communication entre le client et le serveur ne doit pas dépendre d’un quelconque contexte provenant du serveur.
    - Une REST API respecte la norme HTTP


## Inconvénients
- Pleins de plugins
- Customisation (parfois trop)
- Hyper monétisation
- Faire le tri n'est pas toujours simple

À partir du moment où il y a trop de liens différents entres les contenus, on préféra une autre solution à WordPress. Il faut penser en terme d'entité.

Le MCD peut aider à faire l'arbitrage. 