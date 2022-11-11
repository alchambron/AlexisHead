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

##### Alerte erreur

**Attention** il ne faut pas ajouter n'importe comment du CSS dans un sous fichier (par exemple au dessus, ne pas ajouter du CSS général dans le day.css). 

Certes le CSS sera compris, mais ce sera vite un problème. 

Donc tout CSS généralisé doit absolument être dans `main.css`.

---

#### Lancer l'asset pipeline

Pour lancer le processus de réduction et de compilation du code on va indiquer à rails que notre code est pret et qu'il peut tout réduire. 

```ruby
rails assets:precompile
```
>Cette commande va lancer le compiler et générer un fichier qui comprendra tous le code en un, et qui sera donc plus facilement lisible. 

Voici à quoi ressemble les logs à ce moment : 

```shell
  INFO -- : Writing /thp/public/assets/application-ff05acb16c68bfa2f1464c09aeeba8ce0374d32bfd5cb007f366f5e7d69234c1.css
    INFO -- : Writing /thp/public/assets/application-ff05acb16c68bfa2f1464c09aeeba8ce0374d32bfd5cb007f366f5e7d69234c1.css.gz
    INFO -- : Writing /thp/public/assets/favicon/apple-touch-icon-120x120-precomposed-372de868f08319961b72ba7e3b1ed7121e75e29c8294334cb2c911409ea18131.png
    INFO -- : Writing /thp/public/assets/favicon/apple-touch-icon-120x120-372de868f08319961b72ba7e3b1ed7121e75e29c8294334cb2c911409ea18131.png
    INFO -- : Writing /thp/public/assets/application-661b0c4ab5de949af640c3fb9b4c885edc3beeec72f2e393338b3eee2f9daf39.js
    INFO -- : Writing /thp/public/assets/application-661b0c4ab5de949af640c3fb9b4c885edc3beeec72f2e393338b3eee2f9daf39.js.gz
```

Si l'ont regarde les logs, on remarque une clé de hash généré pour chaque fichier. 

A savoir en cas de relance, un fichier non modifier gardera le même hash, donc ne sera pas modifier ici ce qui est pratique.

#### Quelques commandes

-   `$ rails assets:clean` va **supprimer tous les assets précompilés** avant et ne laisser que ceux créés par la dernière génération de l’Asset Pipeline

-   `$ rails assets:clobber` va **simplement supprimer tout le répertoire** `public/assets`. Comme ça au moins, c’est clair et propre, ya juste plus rien !! On peut repartir sur de bonnes bases

#### Dans le cas de rails en mode production

Il faut savoir que le **rails asset precompile sera lancé par l'hebergeur** (heroku, fly...). 
Donc nous utilisons cette commande pour **se rendre compte en local** de ce qui se passera en production. 

Pour tout bien configurer comme si voici la marche à suivre : 

```shell
rails assets:precompile
```

Puis ensuite pour lancer le serveur rails comme si on était en production voici la commande 

```ruby
RAILS_ENV=production RAILS_SERVE_STATIC_FILES=true rails server
```
> Conseil créer un alias pour cette commande : Alias = rsprod

Lorsque Puma va lancer le serveur en local il affichera ça 

```shell
    => Booting Puma
    => Rails 7.0.4 application starting in production 
    => Run `rails server -h` for more startup options
    Puma starting in single mode...
    * Version 5.6.5 (ruby 3.0.0-p0), codename: Llamas in Pajamas
    * Min threads: 5, max threads: 5
    * Environment: production
    * Listening on tcp://0.0.0.0:3000
    Use Ctrl-C to stop
```

S'il affiche `Environment: production`, tu es bien en production !

#### Et les images ?

Pour toutes les images à ajouter il faut les stocker dans le répertoire `app/assets/images/`.
> L'asset pipeline fera le lien entre le fichier et son chemin "réel" une fois en production.

Maintenant il faut dire à l'Asset Pipeline qu'on veut utiliser une image. 
Dans l'idée on le spécifiera dans le fichier css. Voici un exemple

```css
body {
      background: url(asset_path('backgrounds/bg1.png')) no-repeat center center;
    }
```
> Cette ligne veut dire que la source de notre background sera une URL et que l’URL en question est déterminée par l’Asset Pipeline pour une fichier dont la fin du chemin est `backgrounds/bg1.png`

A noter : tu peux utiliser `image_path` au lieu de `asset_path` si tu veux. La fonction `asset_path` sait retrouver toute ressource présente dans le répertoire `app/assets/`, ce qui fait qu’elle fonctionne aussi pour les fonts ou même les vidéos si tu en stockes dans les assets (mauvaise idée pour les vidéos).

#### Pour les polices d'écriture 

Même logique, créer un dossier `app/assets/fonts/` et de la même manière tout reste rangés.

## Integration d'un thème Boostrap

#### La logique

Related to : [[Bootstrap]]
Related to : [[Thème Bootstrap]]

[Exemple d'un thème Bootstrap](https://startbootstrap.com/template/modern-business)

Lorsqu'on trouve un thème qui nous plait il faut dans un premier temps essayer de le comprendre. 

Ce pas à pas va être en **deux parties** :

-   la première est la compréhension d’une librairie externe. En comprenant ce que tu as dans le dossier, son intégration sera d’autant plus simple
-   le seconde sera son intégration : une fois que tu as compris comment marche le template

#### Comprendre un thème

Dans la quasi totalité des thèmes bootstrap, il est présent un `README.md`
Le lire peut aider, et souvent parle d'installation de prérequis. 

```shell
    .
    ├── 404.html
    ├── about.html
    ├── blog-home-1.html
    ├── blog-home-2.html
    ├── blog-post.html
    ├── contact.html
    ├── css
    │   └── modern-business.css
    ├── faq.html
    ├── full-width.html
    ├── gulpfile.js
    ├── index.html
    ├── js
    │   ├── contact_me.js
    │   └── jqBootstrapValidation.js
    ├── LICENSE
    ├── mail
    │   └── contact_me.php
    ├── package.json
    ├── package-lock.json
    ├── portfolio-1-col.html
    ├── portfolio-2-col.html
    ├── portfolio-3-col.html
    ├── portfolio-4-col.html
    ├── portfolio-item.html
    ├── pricing.html
    ├── README.md
    ├── services.html
    ├── sidebar.html
    └── vendor
        ├── bootstrap
        │   ├── css
        │   │   ├── bootstrap.css
        │   │   ├── bootstrap.css.map
        │   │   ├── bootstrap-grid.css
        │   │   ├── bootstrap-grid.css.map
        │   │   ├── bootstrap-grid.min.css
        │   │   ├── bootstrap-grid.min.css.map
        │   │   ├── bootstrap.min.css
        │   │   ├── bootstrap.min.css.map
        │   │   ├── bootstrap-reboot.css
        │   │   ├── bootstrap-reboot.css.map
        │   │   ├── bootstrap-reboot.min.css
        │   │   └── bootstrap-reboot.min.css.map
        │   └── js
        │       ├── bootstrap.bundle.js
        │       ├── bootstrap.bundle.js.map
        │       ├── bootstrap.bundle.min.js
        │       ├── bootstrap.bundle.min.js.map
        │       ├── bootstrap.js
        │       ├── bootstrap.js.map
        │       ├── bootstrap.min.js
        │       └── bootstrap.min.js.map
        └── jquery
            ├── jquery.js
            ├── jquery.min.js
            ├── jquery.min.map
            ├── jquery.slim.js
            ├── jquery.slim.min.js
            └── jquery.slim.min.map
```
> Voici la structure d'un thème boostrap

**Astuce** : La plupart des thèmes contienne un `index.html` qui sera une sortie d'exemple du thème pour tester. Une sorte de démo. 

Donc si on oublie les fichier HTML, voici à quoi ressemble un thème : 

```shell
  ├── css
    │   └── modern-business.css
    ├── gulpfile.js
    ├── js
    │   ├── contact_me.js
    │   └── jqBootstrapValidation.js
    ├── LICENSE
    ├── mail
    │   └── contact_me.php
    ├── package.json
    ├── package-lock.json
    ├── README.md
    └── vendor
        ├── bootstrap
        │   ├── css
        │   │   ├── bootstrap.css
        │   │   ├── et plein d’autres fchiers CSS de Bootstrap
        │   └── js
        │       ├── bootstrap.js
        │       ├── et plein d’autre fichiers JS de Bootstrap
        └── jquery
                ├── jquery.js
                └── et plein d’autres fichiers pour jQuery
```
> Vu de la structure d'un template bootstrap sans les html.

Si on décompose 

-   un dossier `css/` qui **contient le css** du thème : c’est important pour nous

-   un fichier `gulpfile.js` : après une recherche Internet, on peut voir que ce dernier **permet d’automatiser des tâches**. Cela ne nous concerne pas pour la librairie

-   un dossier `js/` qui **contient le javascript** de notre application. On verra avec JS tout ce qui est JS : pas besoin d’en tenir compte pour le moment

-   un fichier `LICENSE` qui nous explique la license de la librairie. Elle est en MIT license donc c’est cool

-   un dossier `mail/` qui **contient un programme en PHP pour faire tourner le mailer**. Nous on s’en fout : poubelle

-   deux fichiers `package.json` qui permettent à **Webpack de gérer la librairie** : on n’en n’a pas besoin non plus

-   un dossier `vendor/` **qui contient deux librairies : Bootstrap et jQuery**. C’est important pour nous

Donc **en résumé** ce qui nous interesse : 

-   le dossier `vendor/` qui contient les librairies externes
-   le dossier `css/` qui contient le CSS de notre thème
-   le dossier `js/` qui contient le js de notre app (mais on verra cela plus tard)

##### Verifier qu'un template marche bien

```html
 <!-- Bootstrap core CSS -->
    <link href="vendor/bootstrap/css/bootstrap.min.css" rel="stylesheet">

    <!-- Custom styles for this template -->
    <link href="css/modern-business.css" rel="stylesheet">

    (plein de lignes de HTML)

    <!-- Bootstrap core JavaScript -->
    <script src="vendor/jquery/jquery.min.js"></script>
    <script src="vendor/bootstrap/js/bootstrap.bundle.min.js"></script>
```
> Exemple d'un index.html

Cela veut dire que le fichier `index.html` pour marcher parfaitement a besoin de :

-   le fichier css de Bootstrap
-   le fichier css du thème
-   le fichier JS de jQuery
-   le fichier JS de Bootstrap

Bam, cela veut dire que tu as besoin des librairies suivantes :

-   Bootstrap (CSS et JS)
-   du thème (CSS)
-   jQuery (JS)

#### Installer un thème 

Voici les étapes pour bien placer tout les éléments au bon endroit au sein de notre application. 

##### Créer les fichiers nécessaire 

Dans un premier temps il faut mettre les librairie dans l'asset pipeline.
Dans notre exemple il s'agit de : 

-   Bootstrap (CSS et JS)
-   le thème (CSS)
-   jQuery (JS)

Ces trois librairies iront dans le dossier `vendor/` donc je te laisse créer les bons sous-dossiers :

-   `vendor/assets/`
-   `vendor/assets/stylesheets/`
-   `vendor/assets/javascripts/` (nous verrons plus en détails comment s’occuper de JS quand on fera du JS, mais je te montre quelques bases)

Ensuite, tu vas devoir intégrer 4 fichiers :

-   `vendor/assets/stylesheets/bootstrap.css` que tu trouves dans `ton_thème/vendor/bootstrap/css/`
-   `vendor/assets/stylesheets/modern-business.css` que tu trouves dans `ton_thème/css/`
-   `vendor/assets/javascripts/bootstrap.bundle.js` que tu trouves dans `ton_thème/vendor/bootstrap/js/`
-   `vendor/assets/javascripts/jquery.js` que tu trouves dans `vendor/jquery/`

##### Configurer assets.rb

Il faut dire à l'asset pipeline que maintenant il peut avoir accès à de nouveaux fichiers. 

Pour cela dans le fichier `assets.rb`  il faut ajouter les lignes suivantes 

```ruby
Rails.application.config.assets.paths << Rails.root.join("vendor", "assets", "stylesheets")

Rails.application.config.assets.paths << Rails.root.join("vendor", "assets", "javascripts")
```
> Ne pas oublier de relancer le serveur


##### Les manifests

Pour rappel ce sont les deux gros fichiers `application.css` et `application.js`.

Retire les lignes

```ruby
     *= require_tree .
     *= require_self
```

Et remplace-les par les lignes suivantes :

```ruby
     *= require bootstrap
     *= require modern-business
```

Idem pour le fichier application.js, retire la ligne `//= require_tree .` et remplace-la par les lignes suivantes :

```ruby
    //= require jquery
    //= require bootstrap
```

##### Ouvrir le template

Une fois tout télécharger et parametrer plus qu'a copier le body du `index.html`

Et si tout marche cela devrait apparaitre sur le serveur. 

**Ne pas oublier** de lancer le serveur avec cette commandes : 

```shell
    $ RAILS_ENV=production RAILS_SERVE_STATIC_FILES=true rails s
```

