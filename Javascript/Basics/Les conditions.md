Related to : [[Javascript]]

---

### Fonctionnement

Les conditions sont quasiment identique à ce qui est présent en ruby.

#### Type de condition

- `if` 
- `else`
- `else if`

#### Type de comparaison

Voici les différents type de comparaison possible

-   `>=` signifie "supérieur ou égal à". `>` signifie strictement supérieur
-   `<=` signifie "inférieur ou égal à". `<` signifie strictement inférieur
-   `!==` signifie "contenu ou type différent de". Veuillez noter qu'il y a 2 signes "égal".
-   `===` signifie "contenu ET type égal à". Veuillez noter qu'il y a 3 signes "égal".

### Comprendre

#### Les " === "

```js
    console.log("36" == 36); // va retourner TRUE car le contenu est identique
    console.log("36" === 36); // va retourner FALSE car d'un côté on a un string et de l'autre un number
```
> Il est important de comprendre les 