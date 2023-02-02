Related to : [[Javascript]]

---

[Cours complet](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array)

### Fonctionnement



#### Créer un array

Pour créer un array, c'est un peu comme définir une variable

```js
let statusDeTHP = ["Moussaillon", "Corsaire", "Renegat"]
```
> Cela créera un array avec 3 valeurs, on peut mélanger nombre, string, boolean etc etc 


#### Faire appel au array 

Pour faire appel au array il suffit de l'appeler avec []

```js
statusDeTHP[0]
```
> Cela retournera "Moussaillon"


#### Connaitre la taille d'un array

Pour connaitre la taille d'un tableau, on peut utiliser des `.length` 

```js
statusDeTHP.length
```
> Cela retournera 3 dans notre exemple


#### Modifier la valeur d'un array

Il suffait juste de réécrire sur le chiffre concerné

```js
statusDeTHP[0] = "La moussaille"
```
> La 1e valeur du tableau va donc devenir "la moussaille" et non "Moussaillon" comme c"était avant.


#### Ajouter de nouvelle valeur à la fin du tableau

Tout comme dans d'autre languages, on peut utiliser `push`

```js
statusDeTHP.push("Flibustier")
```
> Cela rajoutera "Flibustier comme nouvelle valeur dans le tableau"

#### Ajouter une nouvelle valeur au début du tableau

Tout comme pour au dessus il existe `unshift`

```js
statusDeTHP.unshift("Pirate")
```
> Cela ajoutera "Pirate" au début du tableau

#### Supprimer des éléments

Ils existes plusieurs moyens de supprimer des éléments des tableaux. 
C'est un peu comme au dessus 

- Supprimer le dernier élément du tableau

```js
statusDeTHP.pop()
```

- Supprimer le premier élément du tableau

```js
statusDeTHP.shift()
```

- Supprimer plusieurs éléments d'un coup 

```js
statusDeTHP.splice(0,2)
```
> Cela indique qu'il enlevera 2 elements à partir de l'indice 0


#### Recréer un array (sous array)

On peut faire en sorte de retourner un array issus d'un array initial. 

```js
statusDeTHP.slice(2,4)
```
> Ses valeurs seront celles comprises entre l'index 2 (inclus) et 4 (exclus).

**Attention** à ne pas confondre `splice` et `slice`

---

#### Refaire un array à partir d'un autre array

On peut utiliser la fonction `map` pour refaire un array. Elle fonctionne de la même manière qu'une boucle, avec une variable d'instance. 


```javascript
const numbers = [1, 2, 3, 4];
const doubled = numbers.map(item => item * 2);
console.log(doubled); // [2, 4, 6, 8]
```
> On prent item comme variable d'instance, et c'est avec celle ci que l'ont agis. 

---

#### Filtrer les éléments d'un array 

Pour filtrer les éléments d'un array, on peut utiliser `filter`.

```javascript
const numbers = [1, 2, 3, 4];
const evens = numbers.filter(item => item % 2 === 0);
console.log(evens); // [2, 4]
```

--- 

#### Sortir une réponse boolean d'un array

Pour ressortir une réponse **true** or **false**, on p

