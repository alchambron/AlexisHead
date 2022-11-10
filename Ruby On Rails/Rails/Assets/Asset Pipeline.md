Related to : [[Rails]]

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

Ces deux fichiers `application.css` et `application.js` sont donc appelé par rails et ce sont eux 



--- 

