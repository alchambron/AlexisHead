Related to : [[Rails]]
Related to : [[Créer Formulaire]]

---

[Lien](https://github.com/bcrypt-ruby/bcrypt-ruby)

### Installation

```shell
gem install bcrypt
```

### Mise en place

#### Ajouter une colonne

Créer une colonne nommé précisement `password_digest` 

Dans le cas d'une migration, ou d'une table déja existante ajouter une colonne

```ruby
    def change
      add_column :users, :password_digest, :string
    end
```

#### Modifier les modele

Pour initialiser bcrypt il faut l'indiquer au modele pour que la base de donnée comprenne. 

Pour cela ajouter dans le modele comprennant la colonne cette ligne 

```ruby
has_secure_password
```

#### Ajouter une confirmation

```ruby
password_confirmation
```

Enregister une seconde colonne du formulaire avec cette sortie. 