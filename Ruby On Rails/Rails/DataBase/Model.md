Fonctionnalité [[Rails]] 
Attention [[Convention over configuration]]

Les modeles suivent une convention particulière, c'est le nom de la table au singulier

Chaque base de donnée doit être lié à un model !

---

### A quoi sert un model ?

Un modèle sert à lié une base de donnée SQL à une classe dans ruby. 


*Extrait du cours* 

>Mais quel est le rôle du fichier model ? Il sera dans le dossier `app/model` et aura pour objectif de définir plusieurs choses :
>
>-   Les méthodes de classe qu'on veut pouvoir utiliser sur les instances 
>
>-   Les validations qui sont les conditions à remplir pour qu'une entrée soit considérée comme OK et sauvegardée (ex : impossible de créer un utilisateur si le champ e-mail est vide) 
>
>-   Les liens entre les différentes tables / models (1-N, N-N)

**Exemple**

Si on prend l'exemple d'une table `users` liée au model `User`, voici comment les deux sont liés :

-   Chaque entrée de la table SQL `users` est en fait une instance de la classe Ruby `User`**.

-   On peut créer une nouvelle entrée en BDD en faisant les lignes de Ruby** : `julie = User.new("julie", "julie@gmail.com")` puis `julie.save`. La table `users` est alors complétée en BDD d'une nouvelle entrée avec les bonnes infos.

-   Chaque colonne de la table est automatiquement une variable d'instance qui est déjà en `attr_accessor`. Par exemple si je fais en Ruby `julie.email`, je récupère bien le contenu de la colonne `email` de cet objet (par ex : "julie@gmail.com"). Et si je fais en Ruby `julie.email = nil`, puis `julie.save`, la colonne est bien modifiée en BDD.

---

### Créer un model 

```bash
$ rails generate model NomDeTonModel
```

### Ajouter des obligation

On peut obliger la présence de certains champs avec `validates`.

[Docs](https://guides.rubyonrails.org/active_record_validations.html#presence)


Exemples d'obligation

```ruby
# Pour la colonnes "terms", obligation de accepté une case
validates :terms,  acceptance: true

# Pour la colonnes "password", obligation de confirmation
validates :password, confirmation: true

# Pour la colonnes "password", obligation de présence 
validates :password, prensence ( if: :password_required? )

# Pour la colonnes "username", exclusion si admin superuser
validates :username, exclusion: { in: %w(admin superuser) }

# Pour la colonnes "email" obligation d'un format précis en regex
validates) :email, format: { with: /\A([^@\s]+)@((?:[-a-z0-9]+\.)+[a-z]{2,})\z/i, on: :create }

# Pour la colonnes "name", obligation d'une longueur minimum de 2
validates :name, length: { minimum: 2 }

# Pour la colonnes "bio", obligation d'une longueur max de 500
validates :bio, length: { maximum: 500 }

# Pour la colonne "password", obligation d'une longueur entre 6 et 20
validates :password, length: { in: 6..20 }

# Pour la colonnes "registration_number", obligation d'un nombres de 6
validates :registration_number, length: { is: 6 }
```

 