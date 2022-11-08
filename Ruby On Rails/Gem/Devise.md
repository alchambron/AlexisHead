Related to : [[Gem]]
Related to : [[Rails]]

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

## Installation / Fonctionnement

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


Après la géneration, Devise va demander d'effectuer des actions, certaines sont importante comme le branchement de ActionMailer en local et sur Heroku.

Pour cela **verifier** que cette ligne est présente dans `config/environments/development.rb`

```ruby
 config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }
```

#### Etape 3 - Generation Model

```shell
rails g devise User
```
> Cette commande va dire à Devise de generer tout les model  

Voici ce que generera Devise dans le dossier `migrate`.

```ruby
    # frozen_string_literal: true

    class DeviseCreateUsers < ActiveRecord::Migration[5.2]
      def change
        create_table :users do |t|
          ## Database authenticatable
          t.string :email,              null: false, default: ""
          t.string :encrypted_password, null: false, default: ""

          ## Recoverable
          t.string   :reset_password_token
          t.datetime :reset_password_sent_at

          ## Rememberable
          t.datetime :remember_created_at

          ## Trackable
          # t.integer  :sign_in_count, default: 0, null: false
          # t.datetime :current_sign_in_at
          # t.datetime :last_sign_in_at
          # t.inet     :current_sign_in_ip
          # t.inet     :last_sign_in_ip

          ## Confirmable
          # t.string   :confirmation_token
          # t.datetime :confirmed_at
          # t.datetime :confirmation_sent_at
          # t.string   :unconfirmed_email # Only if using reconfirmable

          ## Lockable
          # t.integer  :failed_attempts, default: 0, null: false # Only if lock strategy is :failed_attempts
          # t.string   :unlock_token # Only if unlock strategy is :email or :both
          # t.datetime :locked_at

          t.timestamps null: false
        end

        add_index :users, :email,                unique: true
        add_index :users, :reset_password_token, unique: true
        # add_index :users, :confirmation_token,   unique: true
        # add_index :users, :unlock_token,         unique: true
      end
    end
```

> Cette migration concerne la création d'une table users, qui comprendrais les différents prérequis pour que Devise fonctionne correctement. 

 De base, Devise ne gère que les attributs sous les sections `Database Authenticatable`, `Registerable`, `Recoverable`, `Rememberable`, et `Validatable`.
 Les autres paramètres sont donc optionnels. 

---

**!!! Dans le cas d'une table déja créer !!!** 

La gem Devise va **reconnaitre** qu'il existe déja une table, et modifier son code en fonction. 

**MAIS ATTENTION !** 

>-   Indispensable : Si jamais tu as déjà dans ta table users une colonne que Devise utilise (email, encrypted_password, etc), la migration plantera puisque Devise les ajoute aussi (impossible de créer 2 fois un attribut ayant le même nom). Il te faudra enlever ces lignes de la migration de Devise.

>-   Optionnel : La migration générée est séparée en 2 parties: `self.up` qui liste les changements qui vont avoir lieu sur la table `users` si la migration est passée et `self.down` qui liste les changements si on rollback la migration. Tu peux voir un exemple [dans la documentation](https://edgeguides.rubyonrails.org/active_record_migrations.html#using-the-up-down-methods). Il faudra (idéalement - sinon tout rollback sera inefficace) penser à compléter à la main la partie `self.down` pour lister ce qui doit être enlevé avec des : `remove_column` ou des `remove_index`.

#### Le fichier Model

```ruby
    class User < ApplicationRecord
      # Include default devise modules. Others available are:
      # :confirmable, :lockable, :timeoutable, :trackable and :omniauthable
      devise :database_authenticatable, :registerable,
             :recoverable, :rememberable, :validatable
    end
```
> Voici ce qui est généré en model par Devise.

Ce fichier permet d'indiquer à Devise quoi faire, et comment il peut communiquer avec la base de donnée. 
Les options commenté sont "optionnel".

#### Le fichier des routes

Devise va rajouter dans routes la ligne : 
```ruby
devise_for :users
```

Si on execute la commande `rails routes` ça donnera ça : 

![[CleanShot 2022-11-08 at 10.18.53@2x.png | 500]]

Voici l'explication de chaque routes : 

-   `devise/sessions#new` : pour accéder à *la view de connexion.*
-   `devise/sessions#create` : le POST pour *se connecter.*
-   `devise/sessions#destroy` : le DELETE pour *se déconnecter.*
-   `devise/passwords#new` : pour accéder à l'écran "*mot de passe oublié* *?*" où tu rentres ton adresse email pour recevoir un email de réinitialisation de mot de passe.
-   `devise/passwords#create` : le *POST pour réinitialiser* le mot de passe.
-   `devise/passwords#edit` : pour accéder à la *view où tu rentres ton nouveau mot de passe* (tu y accèdes en cliquant dans le lien "réinitialiser le mot de passe" dans ton email de réinitialisation de mot de passe)
-   `devise/passwords#update` : le PATCH/PUT pour changer de mot de passe.
-   `devise/registrations#cancel` (rarement utilisée) : pour accéder à la view permettant de supprimer une inscription.
-   `devise/registrations#new` : pour accéder à la *view d'inscription au site.*
-   `devise/registrations#create` : le POST pour s'inscrire sur le site.
-   `devise/registrations#edit` : pour accéder à la view de modification d'une inscription (notamment son email et son mot de passe).
-   `devise/registrations#update` : le PATCH/PUT pour modifier son email et mot de passe
-   `devise/registrations#destroy` : le DELETE pour détruire son compte


**Bonne nouvelle :** Les controllers sont déja configuré pour ces différerentes actions. Et dans 90% des cas nous n'aurons pas à les touchers. 




