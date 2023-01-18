
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

La fonction `fetch` 
 
