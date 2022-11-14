Related to : [[Rails]]

#rails #import


---

Active Storage est une fonctionnalité de rails qui permet de mettre en ligne des fichiers. C'est à dire que l'utilisateur pourra ajouter des fichiers sur votre site.

Par exemple une photo de profil, ou encore un documents pdf

## Introduction

Active Storage permet de **mettre en ligne des images** depuis un environnement de developpement, c'est à dire qu'il permet de facilement faire des test.

Dans le **cas d'une mise en production**, il faudra utiliser des services payant comme Amazon S3, Google cloud ou encore Microsoft Azure. 

## Mise en place

#### Installation

Pour activer **Active Storage** il faut lancer la commande 

```shell
rails active_storage:install
```

Cette commande créera deux fichiers : 

-   `active_storage_blobs` : qui contient toutes les métadonnées des fichiers uploadés (taille, nom, type, etc.).
-   `active_storage_attachments` : une table jointe entre tes modèles et les uploads.

Cette commande **créera aussi une nouvelle migration**. 
> Cette migration à pour but de mettre en place une nouvelle table dans la base de données qui sauvegardera le tout. 

#### Lier les fichiers à des entrées en BDD

Maintenant il faut faire en sorte d'utiliser ces nouvelle fonctionnalités. 

En **exemple** nous allons utiliser l'idée d'une photo de profil : 

##### Dire au Model User qu'il doit se connecter avec la table

```ruby
    class User < ApplicationRecord
      has_one_attached :avatar
    end
```
> Exemple de model User 

Dans un premier temps un utilise `has_one_attached` pour indiquer à la table de User qu'elle va se lier à notre active storage. 

Dans un second temps on décide d'une variable, à qui on fera appel dans nos controller / view, dans notre exemple `:avatar` (Mais on peut donner le nom que l'ont veut).

##### Possible méthodes grace à ce lien 

-   Tu peux tester si une instance dispose d'un avatar en faisant `user.avatar.attached?`. Il te retourne le booléen correspondant.

-   Tu peux permettre l'upload de fichier en utilisant un formulaire de type `<%= form.file_field :avatar %>` dans ta view.

-   Finalement, tu peux lier à un `user` l'avatar fraîchement uploadé, depuis le controller qui traite le formulaire d'upload. Cela se fait ainsi : `user.avatar.attach(params[:avatar])`

#### Mise en place dans une page show

Dans un premier temps, il faut aller dans le controller pour préparer une page view idéal. 
Une fois avoir tout préparer (routes, controller, view), on va pouvoir en HTML préparer une page pour récupérer des éléments.

```ruby
<h1>Page Profil</h1>

    <p>Bienvenue sur la page d'ajout d'un avatar pour le User portant l'id : <%=@user.id%></p>
    <h3>Avatar actuel</h3>
    <%if @user.avatar.attached?%>
      <%= image_tag @user.avatar, alt: 'avatar' %>
    <%else%>
      <p>=== Il n'y a pas encore d'avatar lié à cet utilisateur ===</p>
    <%end%>
```
> Exemple de chose possible à faire avec l'idée d'un avatar d'utilisateur. 

Donc nous allons faire un formulaire qui va viser à demander à l'utilisateur de mettre à jour sa photo de profil par exemple. 

```ruby
    <%= form_tag do %>
      <%= file_field_tag :avatar %>
      <%= submit_tag "uploader l'avatar" %>
    <% end %>
```
> Voici un formulaire qui cherche à demander un fichier, et l'enregistrer sous la variable :avatar. 

**Attention** le formulaire n'est pas encore complet. Suite plus bas. 

Maintenant plus qu'a récuperer les information dans notre controller et mettre à jour la base de donnée. 

#### Le controller "avatars"

Bien que nous pouvons récupérer les éléments dans une base de données nous ne faisons pas toujours comme ça. 

Dans cette exemple, nous allons créer un controller `avatars`. 

Dans ce controller nous allons faire une def create qui **aura pour rôle d'ajouter** un avatar à un utilisateur. 

```ruby
  class AvatarsController < ApplicationController
      def create
        @user = User.find(params[:user_id])
        @user.avatar.attach(params[:avatar])
        redirect_to(user_path(@user))
      end
    end
```
> Exemple d'une def create qui aura pour but de récup les infos depuis la page initiale

Explication du code : 

1.  la ligne `@user = User.find(params[:user_id])` nous permet d'identifier l'utilisateur concerné. 
 
 2. Ensuite nous lui attribuons l'avatar dont la référence est contenue dans `params[:avatar]` avec la commande `@user.avatar.attach(params[:avatar])`. 
 
 3. Une fois cette association faite, on redirige vers la page show de cet utilisateur en suivant la route dynamique `user_path(@user)`.

Evidemment maintenant il faut faire en sorte que notre premier controller comprenne le second, pour ça il va falloir faire quelques modification au niveau des routes. 


```ruby
 Rails.application.routes.draw do
      resources :users, only: [:show] do
        resources :avatars, only: [:create]
      end
    end
```
> Faire cette modification dans les routes permet de faire en sorte que lorsque quelqu'un utilise la route users, le create puisse être relié au controller avatar.

Maintenant il ne reste plus qu'a **finaliser la page show**, pour qu'elle pointe vers le bon controller. 

#### Finaliser le formulaire complet

Dans la partie précedente, nous n'avions pas finaliser le formulaire. 

Ce qu'il manque : 

-   Lui indiquer la route qu'il doit pointer (par défaut, `form_tag` est déjà en `POST` donc ça, c'est ok) ;
-   Rajouter un élément indispensable à un `form_tag` lorsqu'on veut qu'il puisse uploader des fichiers : l'option `multipart: true`

```ruby
    <h3>Changer d'avatar ?</h3>
    <%= form_tag user_avatars_path(@user), multipart: true do %>
      <%= file_field_tag :avatar %>
      <%= submit_tag "mettre à jour" %>
    <% end %>
```
> Formulaire complet. 

#### Pour une mise en production

A faire 

[Regarder le cours ](https://www.thehackingproject.org/fr/dashboard/courses/1/weeks/4/days/4)
