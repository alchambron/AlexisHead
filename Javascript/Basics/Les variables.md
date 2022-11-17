Related to : [[Javascript]]

---

### Création 

Pour créer une variable en Javascript.

```javascript
let myVariable
```
> Une variable fonctionnera comme toutes les autres. 

Pour tester une variable il suffit de faire : 

```js
console.log(myVariable)
```

##### Il existe un second type de variable

Ce n'est plus beaucoup utilisé depuis ES6, mais il est possible de créer une variable avec `var`.

La différence est la **portée de la variable** (= son scope). Une variable en `let` n'existe qu'au sein de son **bloc de code** alors qu'une variable en `var` persiste au-delà. Un bloc de code, en JS, est défini par des accolades `{ xxx }` (par exemple, une fonction JS sera délimitée par des accolades). Pour comprendre, teste donc le code ci-dessous :

Exemple 

```js
let data1 = "variable en let définie dans le bloc principal";

    { //début du sous-bloc

      data1 = "variable en let modifiée dans le sous-bloc";
      var data2 = "variable en var définie dans le sous-bloc";
      let data3 = "variable en let définie dans le sous-bloc";

    } //fin du sous-bloc

    console.log(data1); // "variable let modifiée dans le sous-bloc"
    console.log(data2); // "variable var définie dans le sous-bloc"
    console.log(data3); // On aura une erreur : data3 n'est pas visible dans le bloc principal
```

Si on décortique la logique : 

-   **la variable `data1` est en `let` et déclarée dans le bloc principal**. Elle est donc visible dans le bloc principal et tout sous-bloc. On peut aussi la modifier dans un sous-bloc.

-   **La variable `data2` est en `var` et déclarée dans le sous-bloc**. Elle persiste donc au-delà du sous-bloc : on peut l'appeler dans le bloc principal.

-   **La variable `data3` est en `let` et déclarée dans le sous-bloc**. Elle n'est pas visible en dehors du sous-bloc : on a donc une erreur en l'appelant dans le bloc principal.


### Utilisation






