
Related to [[Material UI]]

---

### Default installation

Pour installer Material UI par defaut : 

```
npm install @mui/material @emotion/react @emotion/styled
```
> Je specifie par défaut, car material ui comprend énormement de composant supplémentaire et d'addons.


### Installation with Styled Componants

Il est possible d'installer Material UI, et avec celui ci d'installer **Emotion** qui est une librairie Javascript permettant d'écrire du CSS dans du JS.

```
npm install @mui/material @mui/styled-engine-sc styled-components
```


### Installation avec des typographie spécifique

Par défaut, Material UI marche avec la police **Roboto**.
Pour mieux comprendre, Material Design utilise la librairie **Fontsource** qui permet d'importer des polices directement dans du JS.

Voici comment installer des police particulière 

```
npm install @fontsource/roboto
```

```tsx
import '@fontsource/roboto/300.css';
import '@fontsource/roboto/400.css';
import '@fontsource/roboto/500.css';
import '@fontsource/roboto/700.css';
```
> Fontsource can be configured to load specific subsets, weights and styles. Material UI's default typography configuration relies only on the 300, 400, 500, and 700 font weights.


### Installation des Icons 

Il existe aussi plus de 1000 icons inclus dans Material UI. 
C'est aussi un component à ajouter !

```sh
npm install @mui/icons-material
```

