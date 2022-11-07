Related to : [[Helpers Tag]]. 

---
## Fonctionnement

[Lien vers la doc](https://api.rubyonrails.org/classes/ActionView/Helpers/FormTagHelper.html#method-i-form_tag)

Permet de créer un formulaire via des options supplémentaire. 


Exemple de formulaire avec le form_tag :

```ruby
<html>
  <body>
    <!-- ... -->

    <%= form_tag url_for(action: 'create'), method: "post" do %>

      <%= label_tag 'Title' %>
      <%= text_field_tag 'title', @post.title %>
      <br /> <br />

      <%= label_tag 'Body' %>
      <%= text_area_tag 'body', @post.body %>
      <br /> <br />

      <%= label_tag 'Author' %>
      <%= text_field_tag 'author', @post.author %>
      <br /> <br />

      <%= submit_tag "Create Post" %>

    <% end %>

    <!-- ... -->
  </body>
</html>
```


### Si on décortique 

```ruby 
<%= form_tag url_for(action: 'create'), method: "post" do %>
```

#### Créer le formulaire

- `form_tag` : Appelle le helper
- `url_for(action: 'create')` : Permet de dire quel lien on veut concerner, dans notre exemple la def `create` de notre controller.
- `method: "post"` : Permet de dire par quel méthode on va discuter avec la base de données. 

#### Contenu de notre formulaire

Comparaison entre HTML et notre helper

-   `label_tag` → `<label></label>`
-   `text_field_tag` → `<input type='text'>`
-   `text_area_tag` → `<textarea><textarea>`
-   `submit_tag` → `<input type='submit'>`

```ruby
<%= label_tag 'Title' %>
<%= text_field_tag 'title', @post.title %>
```

- `table_tag 'Title'` : On créer le titre de notre formulaire
- `text_field_tag 'title'` : Permet d'enregistrer les informations 





