Related to : [[Javascript]]

---

### Compréhension

Comme dans tous les languages, on peut facilement créer des fonctions. 


#### Créer une fonction

Une fonction se défini avec la syntaxe suivante : 

```js
function nomDeMaFonction(){ //le code };
```

**Attention** en Javascript, contrairement au Ruby, une fonction est toujours exécutée avec des parenthèses

---

#### Appeler une fonction

Pour appeler une fonction : 

```js 
nomDeMaFonction()
```

---

#### Exemples de fonctions

##### Exemple type

```js
function sayHello() {
  console.log("Bonjour toi !");
}

sayHello();
```

##### Avec des entrées 

```js
function multiply(inputNumber1, inputNumber2) {
  let outputNumber = inputNumber1 * inputNumber2;
  return outputNumber;
}

console.log(multiply(2, 3));
console.log(multiply(2, multiply(2,3)));
console.log(outputNumber); // Va créer une erreur car la variable en let n'existe pas en dehors de la fonction
```
> Exemple avec une entrée

L'utilisation de **return**, permet de renvoyer la valeur. 

#### Autre type de déclarations de fonction

Quelques chose qui n'existe pas en ruby, mais il est possible de déclarer nos **fonctions de façon anonymes.** 

Cette fonction peut être **affilié à une variable**, et donc cette variable lancera la fonction.

```js
const multiply = function(inputNumber1, inputNumber2) {
  let outputNumber = inputNumber1 * inputNumber2;
  return outputNumber;
}

console.log(multiply(2, 3));

const otherMultiply = multiply; //On peut ainsi affecter la fonction à une autre variable
console.log(otherMultiply(2, 3));
```
> Exemple d'une fonction anonyme déclarer dans la variable constante "multiply" 
> Ce qui permet de multiplier les différentes possibilité

A savoir, on peut depuis les dernière version de javascript déclarer des choses différements avec `=>`

```js
const multiply = (inputNumber1, inputNumber2) => {
  let outputNumber = inputNumber1 * inputNumber2;
  return outputNumber;
}
```
> Exemple

