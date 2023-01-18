
Related to : [[Javascript]]

------

### Introduction

Une **API** (Application Programming Interface) désigne la nomenclature d'un programme qui peut être utilisé de manière normalisée **depuis l'exterieur**.

##### Les types d'API

Il existe plusieurs types d'API, la plus utilisé est l'API **REST** qui suit la [[Convention REST]].
Mais il en existe d'autres comme : 
- SOAP
- GraphQL

L'idée général derrière l'API est donc de permettre à une personne exterieur d'avoir accès à des fonctionnalité de ton application.

>L'avantage des API est que leur accès est simple et rapide, depuis n'importe où. Ainsi, AirBnb, qui a une application mobile ainsi qu'un site Web, pourra donner l'accès à la "même base de données" facilement à ces deux types d'application.

### Comment utiliser des API

Pour comprendre l'utilisation d'une API, lors de la mise en place d'un projet, il est souvent possible que l'equipe de développement **prépare des fonctionnalités** qui seront ensuite développé pour être **accessible**.

Imagineons un site qui heberge et stock les photos d'un photographe, les developpeurs peuvent créer une API REST qui renvoie ce genre de JSON pour **chaque** photo en base de donnée. 
```json
[
  {
    "image": "PictureImageURL.jpeg",
    "replacementText": "Replacement text of the picture",
    "title": "This is the title of the picture",
    "description": "Hey, this is the description of the picture",
    "linkToShop": "arandomlinktoshop.fr/article/idOfTheProduct"
  }
]
```
> Exemple de retour que peut faire une API, avec l'exemple d'une photo. 

Ainsi les developpeur Front End pourront utiliser ce JSON à leurs souhait pour faire des appel et afficher des éléments. 

```html
<article>
  <a href="{picture.linkToShop}">
    <img src="{picture.image}" alt="{picture.replacementText}" />
    <h1>{picture.title}</h1>
    <p>{picture.description}</p>
  </a>
</article>
```
> Exemple d'utilisation d'une API au sein d'un fichier HTML


#### Les méthodes de requête HTTP

On accède à une API pour en général faire plusieurs actions : 

-   Récupérer des informations
-   Envoyer des informations
-   Modifier des informations
-   Supprimer des informations

Il y a donc plusieurs possibilité de récupérer ses informations. Via le protocole HTTP, on appelle les différentes méthodes : 

-   `GET`
-   `POST`
-   `PUT` (ou `PATCH`)
-   `DELETE`

Donc **une même** route peut être appelé de différentes manière, suivant la logique REST.

Par exemple, si on imagine une ressource "utilisateur", une API REST fournira les URL et méthodes HTTP suivantes permettant de gérer les utilisateurs :

-   `GET https://monsuperapi.com/users/1` → **Récupère** les données de l'utilisateur avec l'ID #1
-   `PUT https://monsuperapi.com/users/1` (+ des données) → **Modifie** l'utilisateur #1 avec les données fournies
-   `DELETE https://monsuperapi.com/users/1` → **Supprime** l'utilisateur #1

>Dans le cas d'une requête `PUT` ou `POST`, il faudra envoyer des données avec notre requête HTTP. Ces données pourront être envoyées dans le "corps" ("body", aussi appelé "payload") de notre requête.

#### Les Headers

Dans certains cas de situations lors d'un appelle à une API, il faudra envoye des informations diverses pour que l'api renvoie les **bonnes informations**.

On va donc utiliser les en-têtes HTTP, ou "Headers" de la requête. 

Un header est **simplement une clé + une valeur.** Voici des exemples de headers HTTP :

-   `Content-Type: application/json; charset=UTF-8`
-   `Accept-Language: fr-FR`
-   `Authorization: Bearer token-super-secret`
-   `User-Agent: Mozilla/5.0`

>La réponse HTTP contient aussi des headers, qui pourront te servir à mieux comprendre la réponse, par exemple pour savoir comment la décoder, etc.


#### La réponse HTTP

Lorsque l'ont envoie des requêtes HTTP, on attend à recevoir une **réponse**. 
Les réponses en temps normal devrait recevoir : 

-   un statut (ou "code" de la réponse)
-   un payload (ou "body", le contenu de la réponse)
-   des headers (les méta-données de la réponse)

##### Le Status

il indique si la requêtes à fonctonné, et d'autres informations. 

Voici en fonction des numéros des **exemples** : 

-   `1` -> **Informationnel** : Réponses intermédiaires qui donnent des instructions pour poursuivre la requête (par ex. `100 Continue`). Ces codes sont rarement rencontrés, et ne sont pas utilisé avec REST.
-   `2` -> **Succès** : Quand la ressource a été trouvée, ou que tout a bien fonctionné (par ex. `200 OK`, ou `201 Created`). Ce sont les codes de réponse les plus courants, du moins ceux qu'on aimerait avoir tout le temps ! :)
-   `3` -> **Redirection** : Quand il y a une redirection de la réponse sur une autre adresse (par ex. `301 Moved Permanently`). Là aussi, c'est très peu utilisé dans le cadre d'une API REST.
-   `4` -> **Erreurs "client"** : Quand il y a eu une erreur dûe à la requête elle même. C'est donc à celui qui fait la requête (la partie "front-end") de corriger le problème (par ex. `400 Bad Request`, ou `401 Unauthorized` - il faut s'authentifier pour accéder à la ressource - ou encore `403 Forbidden`). Ces codes sont très utilisés dans une API REST, car ils permettent de guider les utilisateurs de l'API en cas de mauvaise utilisation.
-   `5` -> **Erreur "serveur"** : Quand il s'est produit une erreur sur le serveur qui a traité la requête (par ex. la classique `500 Internal Server Error`). Celui qui a effectué la requête ne peut rien faire pour remédier au problème, l'erreur doit être corrigée côté serveur pour que ça fonctionne à nouveau.

[Listes complètes des erreurs HTTP](https://restfulapi.net/http-status-codes/)

