Related to : [[Javascript]]

---

### Introduction

#### Quésako ?

DOM ou **Document Object Model** est une manière pour accéder / Modifier du contenu HTML.

Ainsi l'idée avec cette fonctionnalité, et de pouvoir récupérer les information et en faire ce que l'ont souhaite.

#### Les moyen d'appeler du HTML

Il existe 3 méthodes pour récupérer du contenu depuis un HTML 

Voici pour nos exemples l'éléments que l'ont veut récupérer depuis notre html.

```html
<div id="hello" class="hello"></div>
```

- **getElementById**

```js
var div = document.getElementById('hello')
```
> Permet de récupérer les éléments depuis un "ID"

Attention ! C'est le seul ou "Element" n'a pas de S. 

- **getElementsByTagName**

```js
var div = document.getElementsByTagName('div')
```
> Permet de récupérer les éléments depuis un tag HTML.

- **getElementsByClassName**

```js
var div = document.getElementsByClassName('hello')
```
> Permet de récupérer les éléments depuis la class mentionner dans le tag HTML


