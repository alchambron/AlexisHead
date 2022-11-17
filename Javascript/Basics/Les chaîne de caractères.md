Related to : [[Javascript]]

---

### Fonctionnement des string en JS

#### Les conversions et mouvement 

On peut mélanger nombre et string, par exemple

```js
let a = 3;
  console.log("Bonjour à tous les "+ a);
  console.log(a + "3");
```
> Voici deux exemples, qui donnerais "Bonjour à tous les 3" et 6

##### Par contre impossible de multiplier

```js
let a = "coucou" * 2
```
> Cela ne marchera pas et retournera une erreur

---

#### Ajouter la valeur d'une variable dans un string

On peut ajouter des variables dans un string avec `${}`

```js
let numStudent = 4;
let statement = `Dans mon groupe on est ${numStudent} moussaillons`;
console.log(statement);
```
> Exemple d'insertion d'une variable dans une phrases

---

#### Savoir la longueur d'une chaine de caractère

Comme en Ruby, on peut obtenir la longueur d'une chaine de caractère avec `.length` ou encore savoir qu'elle est quelle lettre avec []. 

```js
let word = "The Hacking Project"
word.length
```
> Cela donnera la longueur de la chaine de caractere, dans cette exemple 

```js
"The Hacking Project"[0]
```
> Dans notre exemple ça ressortirais "T"

---

#### Faire une recherche au sein d'une chaine de caractère

On peut faire une recherche au sein d'une chaine de caractère avec `indexOf`. 

```js
"The Hacking Project".indexOf("Hack")
```
> Cela retournera 4

**Attention** si tu obtient **-1** c'est rien n'as été trouvé

---

#### Faire passer des chaine de majuscule à minuscule

On peut passer des éléments de majuscule à minuscule avec `toLowerCase()` et `toUpperCase()`.

```js
toUpperCase("hello")
```
> Cela retournera "HELLO"

---

#### Découper une chaine de caractère

La fonction `split` permet comme pour [[Les arrays]] de découper des élement en fontion d'un élément.

```js
const contentOfTHP = "Git-Ruby-Rails-HTML-CSS-JS";
const lesson = contentOfTHP.split("-");
console.log(lesson[0]); // "Git"
console.log(lesson[5]); // "JS"
```
> Dans cette exemple, on peut découpé dans un nouvel array, en fonction des "-"

La fonction `join(",")` fait l'exact inverse de `split(",")` : elle produit un string en concaténant tous les éléments d'un tableau et en rajoutant, entre chaque élément, un séparateur (une virgule ici).