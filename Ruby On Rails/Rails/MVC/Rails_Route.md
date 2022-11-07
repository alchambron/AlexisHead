- Sujet : Comprendres les commandes lié aux routes
- Related to : [[MVC]]

--- 

## Fonctionnement

Aller dans le fichier : `routes.rb`

Exemple d'ajout d'une route : 

```ruby
get '/static_pages/contact', to: 'static_pages#contact'
```

Décortiquons :

- `get` : C'est le verbe utiliser par HTTP pour créer la route. 
- `'/static_pages/contact'` : C'est l'URL sur laquel l'utilisateur va faire ça requete (l'url sur on ordinateur qu'il va taper). 
- `to: 'static_pages#contact'` : Indique vers quel méthode et quel controleurs la route va pointer. 


## Différens type de routes 


![[Routes.png]]

## Voir ces routes 


```ruby
rails routes
```

Permet de voir les différentes routes existantes dans notre app. 

```shell
root                  GET  /                                controller#index
static_pages_home     GET  /static_pages/home(.:format)     static_pages#home
static_pages_contact  GET  /static_pages/contact(.:format)  static_pages#contact
```

Décomposons 
- `Préfix` :  Montre vers quoi pointes la route
- `Verb` : Montre le verb de la route
- `URI Patter` : L'adresse au sein de notre app Rails. 
- `Controller#Action`  : Indique vers quel controleurs la méthode de la route renvoie. 


## Routes dynamique 

Une route dynamique sert à récupérer l'information d'une adresse mail et de lancer certaines fonction. 

Voici à quoi ressemble une route dynamique :
```ruby
    get '/users/:un_nom_de_variable', to: 'users#méthode'
```

Le  `:un_nom_de_variable`  créer une variable qui prendra l'information tapé par l'utilisateur dans l'url (Par exemple `localhost:3000/users/123`, notre variable prendra le `123`).

Pour récupérer cette information et l'exploiter on utilise : `params`

-   Si l'utilisateur tape comme URL `localhost:3000/users/jose_aldo`, on aura `params{"un_nom_de_variable"} = "jose_aldo"`

Exemple de la vision dans un controlleurs : 
```ruby
    class UsersController < ApplicationController
      def méthode
        @user = User.find(params[:un_nom_de_variable])
      end
    end
```
Dans cette exemple on demande au controller de rechercher dans une data base, l'utilsateur lié à l'information rentré dans l'URL. Donc on récupère l'information de la route dynamique.

### Au cas où perdu avec les routes dynamique

![[CleanShot 2022-10-31 at 10.39.15@2x.png]]

## Routes automatisés

Related to [[Convention REST]]

---
