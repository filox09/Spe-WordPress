# Rappel BEM
## Les blocks
- porte leurs noms
- Les components sont des blocks

## Les éléments
- reprennent le nom du block parent

**remarques**
- WordPress place automatiquement les paragraphe dans des balises `<p>`
- une balise `<p>` par paragraphe

## Exemple de structure
```html
  <section class="posts">
    <article class="post">
      <h2 class="post_title">Mon Article</h2>
      <div class="post_content">
        <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. <a href="#">Atque architecto qui corporis rerum animi</a> repudiandae a eius accusamus minus harum dignissimos eum corrupti minima recusandae cupiditate officia commodi, fuga ut officiis perspiciatis, nesciunt soluta unde? Quasi possimus fugit ad perferendis at? Natus repellat odio asperiores quia, laborum illum tempore quasi perspiciatis exercitationem molestiae illo id quisquam rerum reprehenderit consequatur ipsam quibusdam tempora neque labore, dolor minima. Animi ipsum et rerum repellendus explicabo perspiciatis nulla deleniti?</p>
      </div>
      <div class="post__buttons">
        <a href="#" class="button button--more">Lire la suite</a>
        <a href="#" class="button button--fav">Mettre en favoris</a>
        <a href="#" class="button button--pint">Pinterest</a>
      </div>
    </article>

    
  </section>
```

# Structure de notre pattern
- abstracts
- base
- components
- layout

`node.sass` par défaut lit l'intégralité du dossier et fichiers, sauf les fichiers qui commence par un underscore. D'où l'obligation de mettre un underscore lors du nommage des fichiers imoportés.

Dans le fichier de config de webpack on vient spécifier qu'il ne doit lire que le `app.js` et `main.scss`
```js
let config = {
  entry: [
    './app/js/app.js',
    './app/scss/main.scss',
  ],
  // autre propriétés
}
```
**remarques**
- :warning: Toujours laisser l'appel vers le fichier app.js
  ```
    <script src="js/app.js"></script>
  ```

- :warning: Les imports doivent être réalisés en premier !

# Rappel CSS
## Box-sizing
-  `border-box` permet de spécifier au navigateur que la largeur total d'un élément est égale à la taille de l'élément dans sa globalité et non pas la taille de son contenu.
- Le nom du fichier layout correspondra au nom de la class

## Les pseudo-éléments
Un pseudo élément est un éléent qui n'existe pas concrêtement dans la page web
avec ::before et ::after on peut cibler ce qui se trouve avant et après l'élément qu'on vient de cibler
> ::before crée un pseudo-élément qui sera le premier enfant de l'élément ciblé. Généralement utilisé pour ajouter du contenu esthétique à un élément via la propriété CSS content. Par défaut, l'élément créé est de type en-ligne (inline).