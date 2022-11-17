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
- `!=` signifie "comparer le contenue"
- `!==` signifie "comparer le contenue et le type"

### Comprendre

#### Les " === "

```js
    console.log("36" == 36); // va retourner TRUE car le contenu est identique
    console.log("36" === 36); // va retourner FALSE car d'un côté on a un string et de l'autre un number
```
> Il est important de comprendre les différence entre les deux

Il est **conseillé** d'utiliser le " === ", pour être sur de ne pas se tromper lorsque l'ont compare deux éléments. De même pour `!==`.

#### Exemple de blocs de comparaison

-   Un bloc `if` de base se construit ainsi :

```js
let number = 2; //fais ensuite le test avec d'autres valeurs
if(number > 0) {
	console.log("number est positif");
 } 
```

-   On peut rajouter des résultats alternatifs avec `else if` et `else`. Exemple :

```js
let number = 0; //fais ensuite le test avec d'autres valeurs (positives et négatives)
if(number > 0) {
	console.log("number est positif");
} else if(number === 0) {
      console.log("number est nul");
} else {
      console.log("number est négatif");
} 
```

- Avec d'autre type de comparateur

	**Attention**
	- `&&` = ET
	- `||` = OU
	- `!` = NON

```js
if (true && true) {
  console.log("ce message s'affiche car avec un ET, si les deux conditions sont à TRUE, le résultat est TRUE");
}
if (true || false) {
  console.log("ce message s'affiche car avec un OU, si l'une des conditions est à TRUE, le résultat est TRUE");
} 
if (!false) {
  console.log("ce message s'affiche car un NON sur FALSE donne TRUE");
}
```

#### Le "switch" ()

Quand on a plusieurs scénarios possibles, on peut utiliser la condition `switch … case`.

C'est l'**équivalent** `case ... when` en ruby.

A noter que `break` permet de sortir de la condition, donc d'annuler la suite. 

A noter aussi que dans un cas ou rien ne correspont on peut mettre un **default** qui sera la valeur par défaut.

```js
weekNum = 1; //teste avec plusieurs valeurs
switch (weekNum) {
  case 1:
    console.log("Semaine 1 - Introduction au Code");
    break;
  case 2:
    console.log("Semaine 2 - Découverte de Ruby");
    break;
  case 3:
    console.log("Semaine 3 - Programmation Orientée Objet");
    break;
  case 4:
    console.log("Semaine 4 - Initiation à Rails");
    break;
  case 5:
    console.log("Semaine 5 - Rails intermédiaire");
    break;
  case 6:
    console.log("Semaine 6 - Rails avancé");
    break;
  case 7:
    console.log("Semaine 7 - HTML / CSS et intro au JS");
    break;
  case 8:
    console.log("Semaine 8 - JavaScript de front");
    break;

  default:
    console.log("Cette entrée n'est pas reconnue");
    break;
}
```
> Exemple d'un choix multiples

#### Les variation en cas de nil / undefined

Certaines valeurs peuvent être évaluées à FALSE dans le code. Mais en Ruby, ça n'est valable que pour la valeur `nil` alors qu'en JS, c'est le cas de la valeur `undefined`, du nombre `0` et du string vide `""`. Illustration

```js
let number = 0; //fais aussi le test avec un chiffre non nul
if (number) {
  console.log("ce message ne s'affiche que si number est non nul ");
}

let string = ""; //fais aussi le test avec un mot non vide
if (string) {
  console.log("ce message ne s'affiche que si string est non vide");
}

let myVariable // ici, myVariable sera undefined. Fais aussi le test en lui donnant une valeur: number, string, array ou autre.
if (myVariable) {
  console.log("ce message ne s'affiche que si myVariable contient une valeur ");
}
```
> Voici un exemple, ou on peut faire des condition en fonction si les éléments sont nul ou non.