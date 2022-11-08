## Objectif du projet

L'application sera une version minimaliste (mais fonctionnelle, c'est le plus important) d'[Eventbrite](https://www.eventbrite.fr/), un site qui propose plein d'événements que tu peux rejoindre. Les événements ne concernent qu'une seule ville, la ville où tu te trouves. Voici ce que tu peux faire :

-   En arrivant sur la page d'accueil, un visiteur a accès aux événements. Un header donne un lien d'accès aux pages importantes : accueil, créer un événement, s'inscrire / se connecter, mon profil
-   Il est possible de s'inscrire sur le site avec une adresse email
-   Une personne inscrite sur le site peut proposer un événement. Il renseignera le titre, une description, une date de début, une durée, un prix
-   Sur la page qui affiche les événements, tu verras les infos de l'événement (description, date, durée, prix, nombre de participants)
-   Une personne connectée peut rejoindre un événement. Elle va cliquer sur un lien pour accéder à un formulaire d'inscription à un événement. Sur ce formulaire on donnera son prénom, nom, et on mettra son numéro de carte bleue pour payer l'événement
-   Une personne qui a créé un événement peut accéder à une page qui affiche la liste des invités. À partir de cette page, ils peuvent accéder à une page pour éditer l'événement, voir avoir le bouton pour le supprimer
-   Chaque utilisateur aura une page profil, avec ses informations de base (prénom, nom, description). Si un utilisateur est sur **sa** page profil, il a accès à deux liens : un pour éditer ses informations primordiales (email, mot de passe) avec le bouton pour supprimer son compte, l'autre pour éditer les informations de profil telles que le prénom, le nom, ou la description
-   Actions impossibles à faire si la personne n'est pas connectée : rejoindre un événement, créer un événement, accéder à la page "mon profil"



## Structure du projet

#### Base de donnée / Model 

-  Un model `User`, qui représente les utilisateurs de notre site
-   Un model `Event`, qui représente les événements de notre site
-   Un model `Attendance`, qui représente la participation à un événement. C'est la table de jointure entre les événements et les participants à un événement (un peu comme les rendez-vous entre les docteurs et les patients)

##### User 

- first_name --> String
- last_name --> String
- email -->  String
- description --> Text
- password --> (Gem bycript)

##### Event

- start_date --> datetime
- duration --> Integer
- title --> String
- description --> text
- price --> integer
- location --> string

- user_id (administrator)
- user_id through attendance_id

##### Attendance

- stripe_customer_id --> string

- user_id 
- event_id


### Journée Validante

#### 2.1 - Branchement de Bootstrap 

1.  Aller chercher une navbar et l'integrer dans le layout
2. Mettre en places les différents liens dans la navbar et les tester
3. Aller configurer un drop down (Voir jeudi dernier). 

#### 2.2 Branchement de devise

1. Lancer les installation [[Devise]]
2. Genere le devise avec Users
3. Modifier le fichier de migration et supprimer les lignes incorect 
4. Generer les views de devise
5. Modifier le layout avec les bon liens

Push sur fly

#### 2.3 Faire les premieres views

1. Verifier que tout au dessus fonctionne en deploy
2. Faire la page d'accueil du site 
3. Faire en entier la view du profil d'un utilisateur
4. Faire la page de création d'un evenement
5. Faire la page d'affichage de l'event. 


