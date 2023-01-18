
Related to : [[API]]

----

### Introduction

Pour appeler une API, beaucoup de chose vont rentrer en jeu : 
- Connection internet
- Puissance de l'ordinateur

Vu que tout ces éléments peuvent prendre du temps à répondre, il va falloir générer le code de manière **asynchrone**. C'est à dire que le programme va attendre la réponse de l'api avant de continuer.

### L'asynchrone et les API

Une fonction asynchrone signifie "suivre une séquence définie", c'est à dire que l'instruction du code est exécutée une par une, dans l'ordre d'apparition. 

Donc, fondamentalement, **une instruction doit attendre** que l'instruction précédente soit exécutée.

Comprenons cela à l'aide d'un exemple :

```js
  document.write("Bonjour<br>"); // First
  document.write("Paul<br>") ; // Second    
  document.write("Ca va ?"); // Third
```

Dans notre page HTML, apparaîtra ceci :

Bonjour  
  
Paul  
  
Ca va ?

Ceci est une **exécution synchrone**. Tant que l'instruction `document.write("Bonjour<br>")` n'est pas terminée, l'instruction `document.write("Paul<br>")` ne sera pas exécutée.

Une **instruction asynchrone par contre**, ne va faire "**attendre**" les instructions suivantes du code. Elle sera exécutée en parallèle des autres. Selon la complexité du programme, cela peut faire gagner un temps considérable.

### Mais quand utilise l'asynchrone ?

Ce n'est pas toujours la meilleure méthode, il faut utiliser cette méthodes **que si on s'occupe de tâches indépendantes**. Donc lorsqu'on conçoit un système il faut identifier les dépendances entre chaque processus, et définir **qu'est-ce qui peut être executé indépendamment ou pas**.

#### Appeler une API 

##### AJAX

AJAX, qui signifie **"Asynchronous JavaScript + XML"**. L'idée de l'AJAX est de faire en sorte que des informations apparaissent à l'écran de l'utilisateur sans qu'il est à recharger la page.

Pour faire de l'AJAX, on va appeler une API en utilisant une **nouvelle fonction JavaScript** : `fetch()`.

La fonction `fetch` retourne une **promesse** (un Objet JS `Promise`) qui va permettre de récupérer la réponse à une requête HTTP dès qu'elle arrive (grâce à **l'objet** `Response`).

En pratique, la fonction `fetch()` a besoin de l'endpoint d'API (l'URL) que tu souhaites appeler, et éventuellement des données à envoyer à cet endpoint, ainsi que les headers associés. Par **exemple**, prenons une API qui **renvoie une blague aléatoire** à chaque fois qu'on l'appelle. L'endpoint que la documentation de l'API nous fournit est celui-ci : `https://geek-jokes.sameerkumar.website/api?format=json`.

On remarque que le lien comporte l'appel à l'API, mais aussi le format que l'ont souhaite.

```js
fetch(`https://geek-jokes.sameerkumar.website/api?format=json`);
```
> Exemple en utilisation dans javascript

Nous avons dans cette exemple, une requête **get**, mais **attention !** c'est une fonction asynchrone ! Cela veut dire que pour pouvoir utiliser la réponse à cette requête, il faut qu'on manipule le `Promise` qu'elle nous retourne. 

On a donc **deux possibilités** : 

Première solution : en utilisant le chaînage de notre `fetch()` avec un ou plusieurs `then()`, qui prennent une fonction en paramètre, à exécuter quand la promesse est résolue :

```js
const getJoke = () => {
  fetch('https://geek-jokes.sameerkumar.website/api?format=json')
    .then((response) => {
      return response.json(); // Décodage JSON de la réponse (notez bien le `return` ici)
    })
    .then((joke) => {
      console.log(joke); // Utilisation des données décodées
    });
};
```
> Dans un premier temps on appelle l'API avec fetch, puis ensuite on retourne la response, c'est à dire on décode le JSON de la réponse. puis ensuite grace à ça, on peut récuperer la réponse (joke) et l'afficher.


Seconde façon de faire, plus linéaire : en utilisant les mots-clefs `async` et `await`, de cette manière :

```js
// Attention, notez bien le mot-clef `async` ici, avant les parenthèses de la fonction
const getJoke = async () => {
  const response = await fetch('https://geek-jokes.sameerkumar.website/api?format=json');
  const joke = await response.json(); // Décodage JSON de la réponse
  console.log(joke); // Utilisation des données décodées
};
```
>  On utilise les mots clef "async" et "await", explication ci-dessous

Comme je l'ai dit un peu plus tôt, `fetch()` est asynchrone, et donc utilise les **Promesses** de JS. Lorsque tu effectues ta requête, tu ne souhaites **PAS** bloquer l'exécution du reste de ton programme, qui risquerait de bloquer carrément toute l'interface ! 
L'utilisateur doit quand même **pouvoir utiliser l'interface** de ton site, quel que soit le temps de chargement.

Ainsi, l'utilisation de `then()` ou `async await` va permettre à ta page **d'attendre la réponse** du serveur **sans interrompre** les autres parties du code, et l'utilisateur **pourra continuer à utiliser le site** pendant tout le temps du chargement. 

###### Explication de Promise

Quand nous lançons notre requête avec `fetch()`, un objet `Promise` est initialisé.
Quand cette promesse est "résolue" (c'est à dire quand l'API nous a répondu), elle nous retourne un objet `Response`, qui contient toutes les infos de la réponse HTTP, et quelques méthodes permettant de lire son contenu, comme `.json()`. 
Cette méthode va aussi initialiser une `Promise` à son tour, qui une fois résolue contiendra les données décodées depuis le JSON de la réponse.

Si tu avais fait un `console.log` de l'objet `Response` lui-même, tu aurais **obtenu** quelque chose comme ça :

```js
{
  url: 'https://geek-jokes.sameerkumar.website/api?format=json',
  status: 200,
  statusText: 'OK',
  ok: true,
  headers: Headers {},
  body: (...),
  bodyUsed: false,
  redirected: false,
  __proto__: Response
}
```


##### Gérer les erreurs 

Il est possible parfois que lorsqu'on lance un appel API il y est des erreurs. 
Parfois il est nécessaire de récuperer l'erreur pour demander par exemple à l'utilisateur de recharger la page ou autre. 

On peut donc utiliser `catch()` en fin de code pour récupérer l'erreur et donc pouvoir l'afficher. 

```js
fetch(`https://geek-jokes.sameerkumar.website/api?format=json`)
  .then((response) => {
    return response.json();
  })
  .then((response) => {
    console.log(response);
  })
  .catch((error) => {
    console.error('Response error:', error.message);
  });
```
> Dans cette exemple, on récupère les informations comme au dessus, mais en cas d'erreur on permet de l'afficher

Si on utilise `async await`, on peut utiliser un simple bloc `try ... catch`, comme ceci :

```js
try {
  const response = await fetch('https://geek-jokes.sameerkumar.website/api?format=json');
  const joke = await response.json();
  console.log(joke);
} catch (error) {
  console.error('Response error:', error.message);
}
```

**Catch** permet de récupérer l'erreur et le stock dans un objet **Error**. 

------

##### Utiliser des méthodes et ajouter des Headers

Pour indiquer au code ce que tu souhaite comme options, méthodes de requêtes etc etc...
On peut donc utiliser une deuxième entrée à la fonction fetch, dans laquel on stockera en amont les options dans un objets, voici un exemple : 

```js
const url = 'theAPIEndpointThatYouWant.com';
const data = {
  name: 'Mathis',
  password: 'GigaPassword'
};
const options = {
  method: 'POST',
  body: JSON.stringify(data),
  headers: {
    'Content-Type': 'application/json'
  }
};

fetch(url, options)
  .then((response) => { return response.json(); })
  .then((response) => { console.log(response); })
  .catch((error) => { console.error(error); });
```

#### Introduction à l'asynchrone

