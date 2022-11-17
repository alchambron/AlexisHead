Related to : [[Javascript]]

---

### Introduction 

Il existe différents type de boucles en javascript, qui se rapproche de ce que l'ont peut voir en "C". 

#### Boucle "For"

La boucle **for**, est basé sur la valeur d'une variable (un compteur). 
Voici la syntaxe : 

```js
for([initialisation]; [condition]; [incrémentation]) { };
```

```js
for(let count = 0; count <=5; count++){
  console.log(`on va compter jusqu'à 5 : ${count}`);
}

console.log(count); // Va créer une erreur car count est en let et donc son scope est limité au bloc for.
//passe count en var pour tester ce que ça donne
```
> Exemple de base d'une boucle for

---

#### Boucle "While"

La boucle **while** est une boucle qui tourne à l'infini tant que la condition n'est pas valable. 
Voici la syntaxe : 

```js
while([condition]) { };
```

```js
let answer = "";
while(answer !== "oui") {
  console.log("alors ?")
  answer = prompt("Tu kiffes THP ?");
} 

console.log("haaa, tu nous fais plaisir !") // Qui se lassera le premier entre toi et ton ordi ? :D
```
> Exemple de l'utilisation d'une boucle while

On remarque l'**utilisation** de `prompt` qui ouvre une fenêtre d'input dans ton navigateur.

On peut sortir d'une boucle **while** en utilisant `break`

```js
let word = "";
let letter;

while (true) {
    letter = prompt('Tape UNE lettre stp :');

    if (letter) {
        word += letter; //on rajoute la lettre saisie à la suite du mot
        console.log(word);
    } else { // on rentre dans ce else si letter est vide (l'utilisateur ne saisit rien)
        break; // On quitte la boucle
    }
}
console.log(`voilà ce que tu as tapé : ${word}`);
```
> Exemple de l'utilisation d'une boucle while, avec un break

---

#### Boucle "for in"

La boucle `for in` permet de parcourir les informations  dans un array. 

Elle permet de prendre en compte les différentes valeurs entre zéro et le dernier index. 

**Pour un objet**, le compteur va prendre chaque valeur des attributs, une à une. Exemple :

```js
//On déclare d'abord un array
  let weeksOfTHPArray = ["Semaine 1 - Introduction au Code", "Semaine 2 - Découverte de Ruby", "Semaine 3 - Programmation Orientée Objet", "Semaine 4 - Initiation à Rails"];

//On déclare ensuite un objet
let weeksOfTHPObject = {Semaine5: "Rails intermédiaire", Semaine6: "Rails avancé", Semaine7: "HTML / CSS et intro au JS", Semaine8: "JavaScript de front"};

console.log("**********Parcourons le array :")
for(let index in weeksOfTHPArray) {
  console.log(index); // index va aller de 0 à 3
  console.log(weeksOfTHPArray[index]);
}

console.log("**********Parcourons l'objet :")
for(let weekAttribut in weeksOfTHPObject) {
  console.log(weekAttribut); //weekAttribut va avoir les valeurs "Semaine5" à "Semaine8"
  console.log(weeksOfTHPObject[weekAttribut]);
}
```
> Exemple complet des possibilités

---

#### Boucle "forEach"

**Attention** le `forEach` ne fonctionne que sur des Array. 

Il permet d'obtenir directement la valeur stockée à chaque index du array. Illustration en reprenant le array `weeksOfTHPArray` ci-dessus :

```js
console.log("**********Parcourons le array en forEach :")
weeksOfTHPArray.forEach(weekContent => {
  console.log(weekContent)
});
```
> Exemple d'une boucle forEach