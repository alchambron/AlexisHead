### Résumé des étapes from scratch

#### Etape 1 - Creer de tables / Modeles

Regarder [[Migration]]

1- Créer une table + Model
```bash
rails generate model NomDeTonModel name:string
```
> A partir des conditions on peut préremplir les tableaux dans les migrate au préalable


2- Remplir les tableau si non fait

Regarder "Créer une table" dans [[Migration]]

#### Etape 2 - Créer des liens entre les tableaux

Regarder [[Association DataBase]]

1- Créer une migration pour initialiser la migration

```shell
rails generate migration linkdoctorpatient
```
> Créer une migration sans créer de model

>ATTENTION, le seul moyen de modifier une migration déja effectuer est dereplacer le status en "down", sinon recréer une migration.

---

2- Initialiser les liens

Dans le ficher de migration fraichement créer, selectionner les différents 
```ruby
add_reference :patients, :doctor, foreign_key: true
```
> add_reference : permet de créer un lien entre les différentes tables
> foreign_key : true  :  Permet de lié une clé pour faire le lien. 

--- 

3- Créer les liens dans les models

Aller dans les différents models des différentes table pour initialiser les liens pour obtenir les droits de liens. 

Il existe différentes manière de pouvoir faire des liens entre les différents tableaux. 

Pour l'exemple on va utiliser, un medecin, un docteur, et des rendez-vous

```ruby
has_many 
```
>Permet de faire en sorte d'appeler un tableau plusieurs fois. (Un patients peut avoir plusieurs rendez-vous)

```ruby
belongs_to
```
> Permet de faire en sorte d'être lié à un tableau. (Un rendez vous n'a qu'un patient, mais pas plusieurs docteurs)


4- Liens entre différents tableau par le biais d'un autre

![[CleanShot 2022-10-27 at 11.22.40@2x.png]]

L'utilisation de `through` permet de passer via un tableau pour accéder à un autre. 

L'idée dans notre exemple, est que pour connaitre le nom du docteur d'un patient, le tableau patient va demande au tableau appointment qu'elle est le nom du docteur.

#### Etape 3 - Manipuler les données dans la consoles 



