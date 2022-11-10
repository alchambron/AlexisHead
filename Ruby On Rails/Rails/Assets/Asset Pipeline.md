Related to : [[Rails]]

#CSS 

[Cours THP](https://www.thehackingproject.org/fr/dashboard/courses/1/weeks/4/days/4)

---

### Qu'est-ce que l'Asset Pipeline ?

L'asset Pipeline est une logique de mise en place de fichier visant à optimiser l'accès au différent assets que l'ont va ajouter à Rails (Javascript ou CSS). 

#### Comprendre comment rails interprete la pipeline

Si tu vas dans ton fichier `app/views/layouts/application.html.erb` tu devrais voir les lignes suivantes :

```ruby
    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
```

Ces lignes indiquent à Rails que toutes tes views (`application.html.erb` est le fichier de base de toutes tes views) vont appeler deux fichiers importants :

-   `app/assets/stylesheets/application.css`
-   `app/assets/javascripts/application.js`

Ces deux fichiers `application.css` et `application.js` sont donc appelé par rails et ce sont eux qui vont ensuire require les différents assets. 

```ruby
    /*
     * This is a manifest file that'll be compiled into application.css, which will include all the files
     * listed below.
     *
     * Any CSS and SCSS file within this directory, lib/assets/stylesheets, or any plugin's
     * vendor/assets/stylesheets directory can be referenced here using a relative path.
     *
     * You're free to add application-wide styles to this file and they'll appear at the bottom of the
     * compiled file so the styles you add here take precedence over styles defined in any other CSS/SCSS
     * files in this directory. Styles in this file should be added after the last require_* statement.
     * It is generally better to create a new file per style scope.
     *
     *= require_tree .
     *= require_self
     */
```
> Exemple de ce qui est présent dans le `application.css`

En gros, Rails te demande d’ajouter les fichiers que tu veux intégrer dans ton gestionnaire de CSS. Ainsi, si tu veux ajouter le fichier css de ton thème, tu ajouterais la ligne suivante :

```ruby
     *= require ton_thème
```

L'interet de prévoir ça de cette manière est qu'une fois en production, le pipeline va interpreter uniquement ces deux gros fichiers, et donc en les compressant va pouvoir faire en sorte que le site est moins de surcharge à télécharger. 

--- 

#### L'organisation des fichiers

Dans un **projet web classique d’entreprise**, on a **3 sources de CSS** différentes:

-   Les CSS du projet (“Comment on affiche le petit chat sur la page principale”)
-   Les CSS de son entreprise (“Quelle est la couleur officielle du logo de la boîte”)
-   Les CSS des librairies externes (“Comment Bootstrap affiche un bouton”)

Ces différents fichiers n’ont pas les mêmes façons d’évoluer et vont donc être placés dans des répertoires différents:

-   Les fichiers du projet vont dans `app/assets/stylesheets/`
-   Les fichiers de l’entreprise vont dans `lib/assets/stylesheets/`
-   Les fichiers des librairies externes vont dans `vendor/assets/stylesheets` (ou en CDN)


#### Les librairies en front
#librairies
#assets

Les librairies en front sont des elements de code déja fait pour toi. 

Il existe plein de **librairies** que l'ont peut utiliser :

-   [chart.js](https://www.chartjs.org/) est une super librairie qui permet d’afficher des graphes : idéal si tu as besoin d’afficher tes données dans un dashboard admin

-   [Animate.css](https://daneden.github.io/animate.css/) fait des animations

-   [Reveal.js](https://revealjs.com/#/) est une super librairie pour faire des présentations de type PowerPoint : très pratique pour faire des présentations à la volée

-   [Font Awesome](https://fontawesome.com/) propose plein d’icônes pour aider ton app à être plus lisible

-   [Code Mirror](https://codemirror.net/) est un outil te permettant d’intégrer un éditeur de code dans ton application : idéal pour lancer le futur CodeCademy !

##### En cas d'achat de template Bootstrap

Lors de ce genre d'achat il est possible que le template vienne avec beaucoup de librairies, que l'ont devra ranger dans le dossier `vendor/`.

---

### Configuration de l'asset pipeline

#### Créer les dossiers / Fichiers


Petit rappel des différents emplacements des fichiers 
> les fichiers du projet vont dans `app/assets/stylesheets`, les fichiers de l’entreprise vont dans `lib/assets/stylesheets`, les fichiers des librairies externes vont dans `vendor/assets/stylesheets` (ou en CDN).

Les sous-dossiers ne sont pas créés, je t’invite donc à créer les dossiers suivants :

-   `lib/assets/`
-   `lib/assets/stylesheets/`
-   `lib/assets/javascripts/` 
>(nous verrons plus en détails comment s’occuper de JS quand on fera du JS, mais ça ne mange pas de pain de créer ce simple dossier)


-   `vendor/assets/`
-   `vendor/assets/stylesheets/`
-   `vendor/assets/javascripts/` 
>(nous verrons plus en détails comment s’occuper de JS quand on fera du JS, mais ça ne mange pas de pain de créer ce simple dossier)

Structure du dossier `vendor`
![[CleanShot 2022-11-10 at 17.11.29@2x.png | 300]]

#### Configurer le assets.rb

Le fichier `assets.rb` est présent dans `config/initializer/assets.rb`.

C'est dedans que l'ont pourra renseigner les différents chemin que doit comprendre rails pour lié les différentes librairies / assets. 

```ruby
 Rails.application.config.assets.paths << Rails.root.join("lib", "assets", "stylesheets")
    Rails.application.config.assets.paths << Rails.root.join("lib", "assets", "javascripts")
    Rails.application.config.assets.paths << Rails.root.join("vendor", "assets", "stylesheets")
    Rails.application.config.assets.paths << Rails.root.join("vendor", "assets", "javascripts")
```
> Voici l'exemple d'une configuration qui permettrait à Rails de trouver ou chercher quand on appelle différents fichier CSS ou JS. 

##### Attention redemarrage serveur requis

Vu que le fichier Assets est dans le dossiers d'initialisation du serveur, il faudra redemmarer le serveurs. 

---

#### Appeler les librairies dans les manifest

#CSS 

Pour que Rails puissent comprendre nos différentes librairies, il faut qu'on les appelles à partir de nos deux gros fichiers (`application.css` et `application.js`).

Donc il faudra spécifier dans ces fichiers comment faire.

##### Configurer nos propres codes CSS

Pour faire appel à nos propre code CSS il faudra l'indiquer sous forme de require, avec une bonne logique à prendre en compte. 


- Le CSS qui concerne toutes l'application --> `main.css`
> Le fichier sera dans `app/assets/stylesheets`

- Le CSS qui concerne un élement précis --> `navbar.css` ou n'importe quelle nom
> Le fichier sera dans `app/assets/stylesheets`

Puis dans le manifest il ne restera plus qu'a les appelé : 

```ruby
    *= require main
    *= require navbar
    *= require user
```

---

#### Retirer les mauvaises ligne des manifest.

##### Retirer "require_tree" et "require_self"

`require_tree` dit à ton manifest : ajouter à l'Asset Pipeline tous les fichiers qui sont dans `app/assets/stylesheets`. Exactement comme la commande `git add .` qui permet de tout ajouter, cette dernière est fort pratique, mais te donnera des résultats inattendus : déjà tu ne maitrises pas l'ordre d'ajout, mais aussi il se peut que tu ne veuilles pas ajouter certains fichiers CSS à ton manifest. Une bonne maîtrise de ce dernier t'évitera ce genre de soucis.

`require_self` dis à ton manifest : hey les lignes de CSS qui sont dans ce fichier sont aussi à prendre en compte. La force du Ruby est la lisibilité, et le code bien rangé. Avoir un fichier qui fait deux choses à la fois (manifest + du CSS) est antithétique à la philosophie de Ruby. Il te faudra donc deux fichiers :

-   Un fichier `application.css` qui est le manifest
-   Un fichier `main.css` qui contient le CSS au niveau global de ton application ___

##### Exemple d'un projet

Prenons un exemple concret: pour un petit projet de calendrier interne de la boite ACME_inc, tu veux utiliser Bootstrap pour faire une design simple mais efficace, mais la Direction Artistique insiste pour qu’on utilise les couleurs officielles définies dans le fichier idoine.

![[CleanShot 2022-11-10 at 17.36.19@2x.png | 300]]

Pour gérer tous ces fichiers voici à quoi cela ressemblerais dans le `application.css`. 

```ruby
    /* ...
    *= require bootstrap
    *= require acme_ui_kit
    *= require main
    *= require day
    */
```

