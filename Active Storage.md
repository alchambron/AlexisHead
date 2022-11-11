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



