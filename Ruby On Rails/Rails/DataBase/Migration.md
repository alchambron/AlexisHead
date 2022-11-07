Fonctionnalité [[Rails]]
Permet d'utiliser Rails pour faire une migration vers notre base de donnée [[SQL]]. 

-----
### Learn

Vidéo de [[Grafikart]]

https://youtu.be/LBtCqTeJvfg

-------

Avantage : 

- Permet de faire un ou des changement dans des bases de donnée sans perdre le contenu.
- Permet d'externaliser la création / modification de base de donnée SQL, permettant ainsi de faire des modification depuis n'importe ou même sans avoir accès à la base de donée. 
- Permet de déployer des modification bcp plus rapidement.

----- 

--- 

### Créer une migration 


```bash
rails generate migration NomDeTaMigration
```


---

### Configuration


Le fichier va générer une fichier de migration avec une classe.

```ruby
class NomDeTaMigration < ActiveRecord::Migration[7.0]
  def change
    # ici tu mettras les modifications que tu aimerais apporter à ta base de données
  end
end
```

---
#### Creation de table
Attention [[Convention over configuration]]

Une convention est présente, le nom d'une table est toujours au 

Liste des possibilité 
[Wiki Rails](https://api.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/Table.html)

```ruby
change_table :table do |t|
  t.primary_key
  t.column
  t.index
  t.rename_index
  t.timestamps
  t.change
  t.change_default
  t.change_null
  t.rename
  t.references
  t.belongs_to
  t.check_constraint
  t.string
  t.text
  t.integer
  t.bigint
  t.float
  t.decimal
  t.numeric
  t.datetime
  t.timestamp
  t.time
  t.date
  t.binary
  t.blob
  t.boolean
  t.foreign_key
  t.json
  t.virtual
  t.remove
  t.remove_foreign_key
  t.remove_references
  t.remove_belongs_to
  t.remove_index
  t.remove_check_constraint
  t.remove_timestamps
end
```

Exemple de création de table. 

```ruby
def change
  create_table :users do |t|
    t.string :name
    t.boolean :is_admin
    t.timestamps
  end
end
```

> Je créer une table "users" qui va ajouter 3 colonnes : 
> - :name qui sera un string
> - :is_admin qui sera un boolean
> - j'initialise .timesstamps qui créera une date de création / updated.


---


#### Add / Remove Collumn

Pour voir la docs [Wiki Rails Collumn](https://api.rubyonrails.org/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-add_column)

Permet d'ajouter ou modifier les collumn d'une table déja créer. 

- Add a collumn
Dans cette exemple, on décide d'ajouter une colonne à une tables qui s'appelle **:users**,  cette colonne se nommera **:email** et aura comme type **:string**

```ruby
def change
  add_column :users, :email, :string
end
```


- Remove a collumn 
Dans cette exemple, on décide de retirer la colonne **:is_admin** présente dans la table **:users** celle ci étant **boolean**
```ruby
def change
  remove_column :users, :is_admin, :boolean
end
```

--- 

### Lancer des migrations

Il existe des commandes pour ne pas se perdre dans les différentes migrations. 

- Lancer toutes les migrations
```bash
rails db:migrate
```

>Cette commande lance TOUS les fichiers de migrations, du plus vieux au plus récent. 
  Il lance tous les fichiers de migration qui ont le status "Down"

---

- Regarder les status
```bash
rails db:migrate:status
```

> Cette commandes affiche le status de chaque fichers de migrations présents dans le dossiers migrations.

---
- Retour en arrière
```bash
rails db:rollback
```

 >Permet de revenir en arrière sur la dernière migration. Très pratique quand on a fait une coquille qu'on détecte de suite.
 
 ---
 - Annules les migration posterieurs
```bash
rails db:migrate VERSION=20180905201547
```

> Annule toutes les migrations postérieures à celle portant le nom "20180905201547".

