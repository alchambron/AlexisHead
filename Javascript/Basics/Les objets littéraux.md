Related to : [[Javascript]]

---

### Introduction 

**Javascript** est un language orienté objet, il permet donc de créer des objets et de les appelé comme on le souhaite. 

---

#### Création d'un objet

On crée un objet avec `let` 

```js
let THPSessionNum2 = {
  numOfMouss: 80,
  cities: ["Paris", "Lyon", "Montpellier"],
  successRate: 0.80,
  sessionMoto: "keep pushing to the top"
};
```
> Voici un objet avec l'équivalent de 4 def en ruby

---

#### Appeler les éléments de cette def

On peut appeler des attribut d'un objet en faisant `myObject.attribut`

```js
console.log(THPSessionNum2.numOfMouss);
console.log(THPSessionNum2.sessionMoto);
```
> Cela affichera donc 80, et "keep pushing to the top"

---

#### Modifier les éléments d'un objet`

Pour modifier les éléments d'un objet il suffit de faire `myObject.attribut = xxxx`

```js
THPSessionNum2.numOfMouss = 79; // je modifie un attribut existant
console.log(THPSessionNum2.numOfMouss);
THPSessionNum2.favoriteLesson = "Présentation de Sinatra" //je rajoute un attribut
console.log(THPSessionNum2); //j'imprime tout l'objet pour voir
```
> Voici des modification d'objets 

#### Acceders aux attributs 

On peut également accéder aux attributs en utilisant la syntaxe `myObject['attribut']`.

```js
let attributName = "successRate";
console.log(THPSessionNum2[attributName]);
```
> Cette fonctionnalité est utile quand le nom de l'attribut est contenu dans une autre variable.