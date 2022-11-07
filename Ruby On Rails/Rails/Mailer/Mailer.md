Related to [[Rails]]

---
[Cours THP](https://www.thehackingproject.org/fr/dashboard/courses/1/weeks/4/days/1)

Mailer est une fonctionnalité integré à [[Rails]] pour envoyer automatiquement des mails selon ce que l'ont configure. 

---

### Le Concept

1.  **Des mailers**, qui sont ni plus ni moins que des sortes de controllers appliqués aux e-mails. Tout comme les controllers "normaux", ils contiennent des méthodes qui vont faire des appels à la BDD (via les models) et ensuite envoyer des e-mails (au lieu d'envoyer des pages web à des navigateurs).

2.  **Des views**, qui sont des sortes de templates des e-mails à envoyer. Tout comme les views de ton site, elles sont personnalisées grâce à du code Ruby inclus dedans (pour rajouter un nom, un e-mail, le contenu d'un objet récupéré en BDD, etc.). Il existe deux types de views : les `.text.erb` et les `.html.erb` car on peut envoyer des e-mails au format HTML comme au format text.

Le fonctionnement est très proche de ce que propose le MVC, tu appelle le mailer qui enverra automatiquement la view à l'utilisateur.

---

### Mise en place / Lancement

#### Création 

```shell
rails g mailer UserMailer
```

> Voici un exemple, on utilise le nom en **CamelCase** pour définir le titre. 

Cette commande va automatiquement généré un fichier `user_mailer.rb` dans le dossier "app/mailers".
C'est une sorte de [[Controller]] qui aura pour objectif de guider les différents moyen d'envoie d'email. 

#### Utilisation

##### Dans le Mailer

Pour **remplir le mailer** nous allons définir des fonctions, elle aurons pour but d'appeler les différentes  **views** et donc leurs dire quoi faire. 

```ruby
class UserMailer < ApplicationMailer
      default from: 'no-reply@monsite.fr'

      def welcome_email(user)
        #on récupère l'instance user pour ensuite pouvoir la passer à la view en @user
        @user = user 

        #on définit une variable @url qu'on utilisera dans la view d’e-mail
        @url  = 'http://monsite.fr/login' 

        # c'est cet appel à mail() qui permet d'envoyer l’e-mail en définissant destinataire et sujet.
        mail(to: @user.email, subject: 'Bienvenue chez nous !') 
      end
    end
```

> Exemple d'une page qui enverrais des mail automatiquement venant de s'inscrire. 

Si on décortique 

1. La première ligne permet de définir la valeur de `default[:from]`.
 > Le hash default permet de définir tout un ensemble de valeurs pa défaut

2. La nom de la fonction définir quel va être la view lié à cette utilité. Elle prend une valeur en entrée.
3. La valeur en entrée est le mail de l'utilisateur, mail que l'ont rentre dans une variable. 
4. On peut définir d'autre variable, qui seront utilisé lors de la création de la view. 
5. la ligne `mail` permet de lancer l'appel, donc d'envoyer le mail. 
 > Le début est le déstinataire `@user:email` et la deuxième partie est l'objet du mail. 
 


##### Dans le view

La view est un **template** de notre mail.

Cette view est stocké dans le dossier view, dans un dossier portant le nom de la def utilisé dans le **Mailer**.

```ruby
    <!DOCTYPE html>
    <html>
      <head>
        <meta content='text/html; charset=UTF-8' http-equiv='Content-Type' />
      </head>
      <body>
        <h1>Salut <%= @user.name %> et bienvenue chez nous !</h1>
        <p>
          Tu t'es inscrit sur monsite.fr en utilisant l'e-mail suivant : <%= @user.email %>.
        </p>
        <p>
          Pour accéder à ton espace client, connecte-toi via : <%= @url %>.
        </p>
        <p> À très vite sur monsite.fr !
      </body>
    </html>
```
> Exemple de view pour un mail. 

Cette view est un mail envoyé en **HTML**. 
On appelle nos différentes variable défini dans le mailer (comme **@user** pour obtenir l'email, ou encore **@url** pour les liens à afficher).

Il est aussi important de **prévoir une version texte** en créant un fichier `.txt.erb` qui lui sera plus brut, et sera aussi placé dans le dossier view. 

```ruby
    Salut <%= @user.name %> et bienvenue chez nous !
    ==========================================================

    Tu t'es inscrit sur monsite.fr en utilisant l'e-mail suivant : <%= @user.email %>.

    Pour accéder à ton espace client, connecte-toi via : <%= @url %>.

    À très vite sur monsite.fr !
```
> Exemple d'un fichier en .txt.erb


#### Définir l'envoie automatique

Quand tout est prêt entre notre **Action Mailer** et nos **Views** il faut maintenant signifier à Rails d'utiliser ces ressources.

Il existes plusieurs possibilités : 

-   Si tu veux envoyer un email à la **création d'un utilisateur**, c'est un callback `after_create` dans le model User
-   Si tu veux envoyer un email **quand un utilisateur vient de prendre un RDV** sur Doctolib, c'est un callback `after_create` à la création d'un Appointment
-   Si tu veux envoyer **une newsletter hebdomadaire**, c'est un Service qui tourne de manière hebdomadaire (on verra comment faire des services cette semaine 😉)
-   Un email pour **réinitialiser le mot de passe** peut se mettre dans le controller

##### Exemple de la création d'un mail de confirmation de création d'un User. 

```ruby
class User < ApplicationRecord
      after_create :welcome_send

      def welcome_send
        UserMailer.welcome_email(self).deliver_now
      end

    end
```
> Exemple de ce qui pourrait être présent dans **Controller "User"**.

Le `after_create` permet de définir un **call back**. C'est à dire qu'il fera appel à cette def à la fin.
Cela permet d'eviter de lancer un mail avant qu'un utilisateur soit créer.

En résumé, nous venons de paramétrer la chaîne d'actions suivante :

1.  Un utilisateur est créé en BDD par le model
2.  Grâce au callback `after_create`, on exécute la méthode `welcome_send` sur l'instance qui vient d'être sauvée en BDD
3.  `welcome_send` dit, en résumé, "exécute NOW la méthode `welcome_email` située dans le mailer `UserMailer`"
4.  `welcome_email` va appeler 2 templates en leur mettant à disposition une instance `@user` qui est l'utilisateur créé et une variable `@url` qui est juste un string. Cette méthode enverra ensuite les 2 templates à `@user.email` avec comme sujet "Bienvenue chez nous".
5.  Les 2 templates (un HTML et un text) sont personnalisés avec les entrées en Ruby (`@user.name`, `@user.email` et `@url`) avant d'être balancés par e-mail
6.  Et voilà ! 👩‍🍳


#### Parametrer l'Action Mailer

Parametrer son **Action Mailer** permet de faire en sorte qu'il envoie des mails pour de vrai. Pour cela il y a deux possibilité : 

1. Soit elle tourne en environnement de développement 
2. Soit elle tourne en environnement de production (Heroku, fly, etc etc...)

##### 1 - La config en développement 

Vérification à effectuer 

-   vérifier que notre app Rails déclenche bien des envois d’e-mails (=> ça confirmerait que la chaîne entière d’Action Mailer est bien codée et sans bug) ;
-   vérifier la tronche des e-mails qu'on envoie ;
-   ne surtout pas envoyer des e-mails par erreur, histoire de ne pas prendre le risque de spammer de vrais clients pendant nos tests.

On va utiliser la [[Gem]] nommée [[Letter Opener]].



### En résumé

- Etape 1 - Créer un mailer via le shell
- Etape 2 - Parametrer son Action Mailer
- Etape 3 - Créer ces différentes view 
- Etape 4 - Dire à rails d'utiliser le action Mailer pour l'envoie.
- 