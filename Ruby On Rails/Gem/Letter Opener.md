Related to : [[Gem]]
Related to : [[Mailer]]

---

[Lien du repo](https://github.com/ryanb/letter_opener)

### Installation

##### Etape 1 - Ajouter la gem au bundle

```shell 
gem "letter_opener", group: :development
```

##### Etape 2 - Changer la méthodologie d'utilisation de rails

Aller dans `config/environments/development.rb`

```ruby
config.action_mailer.delivery_method = :letter_opener
config.action_mailer.perform_deliveries = true
```


**Note importante** : la ligne avec `perform_deliveries = true` permet d'éteindre (en la passant à `false`) tout envoi d'email de la part de ton app Rails. C'est bon de savoir qu'elle existe !