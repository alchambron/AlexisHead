# Rails et composants

Rails permet grâce aux partials de décomposer son front en composants. C'est parfait pour la philosophie d'apprentissage par composants.

## 1\. Introduction

Tu vas voir comment conjuguer design atomique et applications Rails grâce au système de partials. Puis nous allons te montrer comment jouer avec le fichier `application.html.erb` pour avoir un joli front.

## 2\. Contexte et historique

Rails est très orienté DRY, donc coder un système pour éviter de répéter son code partout est dans la philosophie du framework. Rails a rapidement pensé à un système de _partials_ qui permet d'appeler très facilement des bouts de front dans ton application.

## 3\. La ressource

### 3.1\. Les partials

#### 3.1.1\. Introduction

Les partials permettent de mettre des bouts de code de front dans un fichier à part. Prenons l'exemple de ta navbar, qui s'affiche sur toutes les pages de ton application. Tu peux copier coller la même navbar sur toutes tes views, mais tu fais face à deux problèmes :

- Le premier est que tu restes trop dans l'état d'esprit page par page (#so_2005) alors que le web moderne se pense composant par composant
- Le second est que ce n'est pas DRY : si jamais tu veux ajouter un lien _Créer un événement_ à ta navbar, tu seras obligé de le faire dans tous tes fichiers views. Vraiment pas ouf

Rails a bien entendu prévu le coup et propose un système de partials qui permettent de mettre des bouts de front dans un fichier spécial qui sera appelé dans certaines parties. Prenons l'exemple de l'organisme d'un formulaire de contact. Ce dernier sera appelé principalement dans le controller _contacts_, sur la méthode _new_. Ainsi dans ta view `app/views/contacts/new.html.erb` tu mettrais :
```ruby
    <%= render "form" %>
```

Puis tu vas créer un fichier `app/views/contacts/_form.html.erb` dans lequel tu mettrais ton organisme du formulaire de contact. Et voilà ! Ton application va appeler ton formulaire très facilement. Grâce à ce système de partials, tu peux penser ton application Rails comme une application moderne : chaque page est une succession d'organismes. Et chaque organisme va être appelé par une ou plusieurs pages. C'est DRY, moderne, et permet d'aller extrêmement vite dans la réalisation du front d'une application. Que des avantages, 0 défaut.

___
** ⚠️ ALERTE ERREUR COMMUNE**

Comme tu peux le voir, la partial s'apelle en faisant `<%= render "form" %>` et le fichier s'appelle `_form.html.erb` et commence par un `_`. C'est une convention de rails qui permet de distinguer facilement une view (sans `_`) d'une partial (avec `_`).

Donc, tu appelles les partials sans `_`, mais les fichiers se nomment avec un `_`.
___

#### 3.1.2\. Où mettre ses partials

Tu peux mettre les partials dans n'importe quel dossier de views et les appeler depuis n'importe quelle view. Voici comment faire :

- Si la partial est dans le même dossier que la view, tu l'appelles en faisant `<%= render "ta_partial" %>`
- Si la partial n'est pas dans le même dossier que la view, tu précises le dossier. Ainsi si je voulais appeler la partial `app/views/contacts/_form.html.erb` dans la view _edit_ de la ressource _users_, tu écrirais dans `<%= render "contacts/form" %>`

Enfin, un peu comme le RESTway™, il faut ranger les partials dans le bon dossier. C'est assez simple, comme tu peux le voir avec les exemples que je vais te donner :

- Une partial que l'on appelle depuis le fichier `application.html.erb` (header, footer, alert) se met dans le dossier `app/views/layouts/`
- Une partial que l'on appelle dans plusieurs pages de l'application (une bannière) se mettra dans un dossier `app/views/shared/`
- Une partial qui concerne une ressource précise (une liste, un formulaire, un affichage précis) se met dans le dossier de la ressource. Ainsi, le formulaire pour créer un événement serait un fichier `app/views/events/_forms.html.erb`

#### 3.1.3\. Opérations de partials

Tu peux faire plein d'opérations sur les partials, comme par exemple passer des variables locales (pratique quand tu veux changer la photo de ta bannière). Je t'invite à t'inspirer de [la doc](https://guides.rubyonrails.org/layouts_and_rendering.html#using-partials) qui explique tout cela.

### 3.2\. application.html.erb

Il existe un fichier qui s'appelle `app/views/layouts/application.html.erb` qui contient les fondements du fichier html de ton application. Le `head`, et le `body`. Tu peux y mettre des CDNs facilement, et notamment le fondement d'une page web.

Certaines parties de ton application se retrouvent sur toutes les pages :

- Le header
- Le footer
- [Les alertes](https://getbootstrap.com/docs/4.0/components/alerts/)

Ainsi, nous te conseillons de faire une partial pour chacun de ces éléments (que tu mettras dans `app/views/layouts/`), et les mettre dans le body du fichier `application.html.erb`. Cela devrait ressembler à ceci :
```ruby
    <%= render 'layouts/header' %>
    <%= render 'layouts/flash'%>
    <%= yield %>
    <%= render 'layouts/footer'%>
```
____
**🤓 QUESTION RÉCURRENTE**

**Dis donc Jamy, comme les partials sont dans le même dossier que le fichier `application.html.erb`, ne faut-il pas faire simplement `<%= render 'ma_partial' %>` pour les appeler et non pas `<%= render 'layouts/ma_partial' %>` ? 🤔**

Oui pour tous les autres dossiers de views, mais pas celui-là 😉
___

Ainsi, chaque page de ton application contiendra le header, le footer, et tu n'auras qu'à mettre les dernières molécules concernant la page 🤠

## 4\. Points importants à retenir

Avec Rails, tu peux facilement décomposer le front de ton application en petits bouts de code nommés partials.

Le fichier `app/views/layouts/application.html.erb` contient la base du html de ton application. Dedans c'est bien d'appeler les partials que tu verras tout le temps : le header, le footer, et les alertes.

## 5\. Pour aller plus loin

Voici [un chouette article](https://goiabada.blog/rails-components-faedd412ce19) sur le composants UI dans Rails.