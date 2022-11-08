Related to : [[Gem]]
Related to : 

---
## Introduction

### Présentation

Devise est une gem permettant de faire toutes l'authentification de l'app pour toi. 

La Gem permet de créer un système d'authentification complet, elle genere : 

-   L'inscription, avec mot de passe et e-mail sécurisé ;
-   La notion de login, logout, session, current user ;
-   La récupération de mot de passe par e-mail ;
-   La confirmation de compte par e-mail ;
-   Le comptage de login ;
-   Le logout après un certain temps d'inactivité ;
-   Le blocage de compte après un certain nombre de tentatives de login ratées.

--- 

### Les différentes fonctionnalités de Devise

-   **Database Authenticatable** : possibilité de stocker les mots de passe dans leur version hashée pour valider l'authenticité d'un utilisateur pendant sa connexion (la base quoi) ;
-   **Registerable** : possibilité de créer un compte via un formulaire. Aussi, possibilité d'éditer et de supprimer son compte ;
-   **Recoverable** : possibilité de réinitialiser le mot de passe et d'envoyer des instructions par e-mail ;
-   **Rememberable** : possibilité d'utiliser le fameux cookie [remember me](https://www.youtube.com/watch?v=fKKNPLowteY) (la session reste ouverte) ;
-   **Validatable** : possibilité de donner des validations pour les e-mails et mots de passe (taille, regex, etc) ;
-   **Omniauthable** : possibilité de gestion de OmniAuth (un service pour se connecter via son compte Google, Facebook ou autre) ;
-   **Confirmable** : possibilité de forcer la confirmation par e-mail du compte ;
-   **Trackable** : possibilité de tracker le nombre de login, leurs timestamps, et les adresses IP ;
-   **Timeoutable** : possibilité d'expirer des sessions après un certain temps d'inactivité ;
-   **Lockable** : possibilité de verrouiller un compte après trop de tentatives échouées de connexions

## Installation

#### Etape 1 - Rajouter Devise

Rajouter devise dans le Gemfile.
```ruby
gem 'devise'
```


#### Etape 2 - Initialiser Devise

```bash
rails generate devise:install
```
> Cette commande generera deux fichiers : devise.rb et devise.en.yml. 

-   `config/initializers/devise.rb` : le fichier de configuration de Devise. On s'en servira par exemple pour paramétrer le service que l'on va utiliser pour les envois d'e-mails ;
-   `config/locales/devise.en.yml` : un fichier contenant les messages d'erreur de Devise. Tu pourras utiliser [ses version françaises](https://github.com/plataformatec/devise/wiki/I18n#french-devisefryml) quand tu seras plus à l'aise avec la gem.

--- 

Après la géneration, Devise va demander d'effectuer des actions, certaines sont importante comme le branchement f



#### Etape 4 - Generation Model

```shell
rails g devise User
```
> Cette commande va dire à Devise de generer tout les model  