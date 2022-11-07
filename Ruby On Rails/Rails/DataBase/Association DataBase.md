Fonctionnalité [[Rails]]

--- 
### Logique 

Il est possible de lié les différents tableau entre eux. 

Dans l'idée, il est possible pour un patients d'avoir plusieurs rendez-vous, mais un rendez vous ne peux avoir qu'un seul patients. 

---

### Modification/Creation d'un tableau.

Pour la modification d'un tableau existant, on va créer un fichier de migration lié à cette modification sans avoir à créer de model avec la commande : 

```bash
rails generate migration linkdoctorpatient
```


Dans ce nouveau fichier de migration, on va créer une reference entre deux tableau. 

```ruby
add_reference :patients, :doctor foreign_key: true
```
> add_reference : permet de créer un lien entre les différentes tables
> foreign_key : true  :  Permet de lié une clé pour faire le lien. 

Lors d'un lien, un schema.rb sera créer permettant de visualiser quel lien existe entre chaque tableau.


---



