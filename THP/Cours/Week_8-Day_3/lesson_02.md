# Alertes et Rails

Comment afficher une alerte sous Rails et la brancher à Bootstrap ? Cette ressource est faite pour toi

## 1\. Introduction

Il est très important de donner des nouvelles à son utilisateur lorsque ce dernier fait les choses correctement (ou l'inverse). Par exemple, lorsque ce dernier se plante dans le mot de passe, on s'attend [à voir un message d'erreur](https://i.stack.imgur.com/T7Xl1.png) nous disant le pourquoi. Cela s'appelle les alertes, et Rails gère ceci grâce aux Flash.

## 2\. Contexte et historique

Le web considère les alertes comme très importantes, et on les voit partout. Elles font partie de toute application qui se respecte.

## 3\. La ressource

Cette ressource sera en plusieurs parties :

- Nous allons voir flash, un hash où l'on stocke les messages que l'on va donner à l'utilisateur
- Puis nous allons voir comment faire concorder le Flash à deux choses
    - [Les alertes Bootstrap](https://getbootstrap.com/docs/4.3/components/alerts/)
    - Aux erreurs de model

### 3.1\. Le Flash

#### 3.1.1\. C'est quoi ?

Tu te souviens du hash `session` qui te servait à stocker ce que tu voulais pendant une session d'utilisateur ? Figure-toi qu'il existe un autre hash dans Rails nommé `flash` et qui ne stocke les données que pour une page (`session` reste pour toute la session, mais `flash` disparait au bout d'une page). Tu peux essayer et mettre dans un controller une ligne du genre `flash[:warning] = "Salut je suis flash"` et dans la vue correspondante la ligne `<%= flash[:warning] %>`.

Ce système est utilisé principalement par Rails pour annoncer des informations aux utilisateurs. Ainsi, quand on crée un utilisateur, on peut faire `flash[:success] = "Utilisateur bien enregistré"`, ce qui aura pour effet de le stocker dans un hash que l'on n'aura qu'à appeler dans notre view à la prochaine page.

Ainsi, dans les controllers on mettra plein de messages concernant l'état de l'application, puis on les affichera grâce à une partial bien placée.

#### 3.1.2\. Définir un flash

Pour définir un flash, il suffit de faire dans la méthode concernée de ton controller : `flash[:ton_type] = "Ceci est un message !"`

___
**🚀 ALERTE BONNE ASTUCE**

On dit souvent "les controllers sont sous strictes conventions, ne mets rien dedans qui n'est pas validé". Et bien figure-toi que définir un flash est typiquement une tâche de controller. Open bar pour mettre du flash dans ton controller 🎉
____

Rails utilise par convention 4 types de flash :

- `notice`, pour les informations
- `success`, pour les opérations fructueuses
- `alert`, pour annoncer une information importante
- `error`, pour annoncer une erreur

Ainsi, si tu veux créer un flash pour annoncer que le post que tu voulais créer a bien été créé en base, tu auras un controller qui ressemble à ceci :
```ruby
    def create
      @post = Post.new(post_params)
      if @post.save
        flash[:success] = "Post was successfully created."
        redirect_to @post
      else
        flash.now[:error] = @post.errors.full_messages.to_sentence
        render :new
      end
    end
```

### 3.2\. Un système d'alertes solide

Nous allons voir comment transformer le flash en alertes stylées que l'on peut appeler partout dans l'application.

#### 3.2.1\. Les flash dans application.html.erb

Les alertes s'affichent entre le contenu d'une page et le header. Tu peux donc mettre dans ton fichier `application.html.erb` les lignes suivantes :
```ruby
    <%= render 'layouts/header' %>
    <%= render 'layouts/flash'%>
    <%= yield %>
    <%= render 'layouts/footer'%>
```

Et dans ton fichier `app/views/layouts/_flash.html.erb` nous allons afficher les flash.

#### 3.2.2\. Flash et alertes Bootstrap

Bootstrap a [une page dédiée aux alertes](https://getbootstrap.com/docs/4.3/components/alerts). Il suffit juste de reprendre notre flash, et de l'afficher dans une alerte cool. J'aime beaucoup [celle que l'on peut faire disparaitre](https://getbootstrap.com/docs/4.3/components/alerts/#dismissing) avec une croix. Le code est :
```html
    <div class="alert alert-TON_TYPE alert-dismissible fade show" role="alert">
      Ton message 👋
      <button type="button" class="close" data-dismiss="alert" aria-label="Close">
        <span aria-hidden="true">×</span>
      </button>
    </div>
```

Il suffit de s'arranger pour mettre ce message quand y'a bien un flash. Pour ceci, il n'y a qu'à mettre ce code dans un `flash.each`. S'il n'y a pas de flash de défini, cela n'affichera rien. S'il y a un ou plusieurs flash de définis, cela les affichera. Voici le code :
```html
    <% flash.each do |type, msg| %>
      <div class="alert <%= bootstrap_class_for_flash(type) %> alert-dismissable fade show" role="alert">
        <%= msg %>
      <button type="button" class="close" data-dismiss="alert" aria-label="Close">
        <span aria-hidden="true">×</span>
      </button>
      </div>
    <% end %>
```

Dernier détail, il faudrait pouvoir transformer le mot `notice` (le type du flash) en `alert-info` (la classe bootstrap), le mot `success` en `alert-success`, le mot `alert` en `alert-warning` et le mot `error` en `alert-danger`. Cela tombe bien, c'est typiquement le rôle du helper de faire ceci. Va donc dans le fichier `application_helper.rb` puis colle-lui les lignes suivantes :
```ruby
    def bootstrap_class_for_flash(type)
      case type
        when 'notice' then "alert-info"
        when 'success' then "alert-success"
        when 'error' then "alert-danger"
        when 'alert' then "alert-warning"
      end
    end
```

Et voilà, c'est converti, pour TOUTES les views de ton app.

#### 3.2.3\. Appeler les alertes dans le controller

Dans ton controller, tu peux facilement créer des flash en faisant `flash[:ton_type] = "Ton message"`. Comme tu as codé des models robustes avec plein de validations, tu as envie de pouvoir appeler les erreurs sans trop te prendre la tête. C'est possible en faisant `@user.errors` ! Ainsi, si tu veux pouvoir créer un flash et lui donner les erreurs de ton model, tu peux écrire : `flash[:error] = @user.errors.full_messages.to_sentence`.

#### 3.2.4\. Flash.now ou flash ?

Lorsque tu n'arrives pas à faire `.save`, tu fais `render :la_view` alors que tu fais un `redirect_to` lorsque tu arrives à faire `.save`. Pourquoi ? Car en faisant `render` tu gardes la variable d'instance `@user`, ce qui est bien pour pouvoir afficher ses erreurs ou encore préremplir le formulaire avec ce que l'utilisateur a mis auparavant. Le soucis est que ton flash va s'afficher pour deux pages puisque tu ne fais pas de redirection. Il te faudra faire un `flash.now[:ton_type] = "Ton message"`.

Donc pour rappel :

- Si tu fais un `render :some_view`, tu fais un `flash.now[:ton_type] = "Ton message"`
- Si tu fais `redirect_to`, tu fais un `flash[:ton_type] = "Ton message"`

## 4\. Points importants à retenir

Tu peux créer facilement un hash `flash` qui tiendra sur une page de ton application. Ce hash sera modifié dans les controller et affiché dans les views. Avec Bootstrap, c'est facile de transformer ce hash en jolies alertes. On va commencer par mettre dans son fichier `application.html.erb` les lignes suivantes dans le body :
```ruby
    <%= render 'layouts/header' %>
    <%= render 'layouts/flash'%>
    <%= yield %>
    <%= render 'layouts/footer'%>
```

Puis dans le fichier `app/views/layouts/_flash.html.erb` :
```html
    <% flash.each do |type, msg| %>
      <div class="alert <%= bootstrap_class_for_flash(type) %> alert-dismissable fade show" role="alert">
        <%= msg %>
      <button type="button" class="close" data-dismiss="alert" aria-label="Close">
        <span aria-hidden="true">×</span>
      </button>
      </div>
    <% end %>
```

Enfin, dans le fichier `application_helper.rb` :
```ruby
    def bootstrap_class_for_flash(type)
      case type
        when 'notice' then "alert-info"
        when 'success' then "alert-success"
        when 'error' then "alert-danger"
        when 'alert' then "alert-warning"
      end
    end
```

Et voilà, tu peux facilement créer des flash dans les controllers.

## 5\. Pour aller plus loin

Devise est un peu capricieuse et pour les messages d'alerte il te faudra redoubler [de patience](https://github.com/plataformatec/devise/wiki/How-To:-Integrate-I18n-Flash-Messages-with-Devise-and-Bootstrap), mais c'est toujours possible