Related to : [[Rails]]

---

Stripe est un moyen de paiement, mais aussi un moyen de mettre en place de quoi payer sur nos application. 


### Installation / Mise en place

#### 1- Avoir un compte Stripe

S'incrire sur [Stripe](https://dashboard.stripe.com/register)
Se login sur [Stripe](https://dashboard.stripe.com/login?locale=fr-FR)

#### 2- Récuperer la clef API

Sur le [dashboard](https://dashboard.stripe.com/test/developers) une fois connecter il y aura deux clé présent à droite.

![[CleanShot 2022-11-09 at 18.27.42@2x.png]] 

#### 3- Configurer Stripe avec Rails

##### Installer les Gems "dotenv" et "Stripe" dans le Gemfile

```ruby
gem 'dotenv'
gem 'stripe'
```

---

##### Créer un fichier .env

Créer un fichier .env à la racine, c'est ici que l'ont mettra la clef API. 
Attention à bien configurer le [[GitIgnore]] ! 

```shell
touch .env
```

Dans ce `.env` on va ajouter nos clef. 

```ruby
PUBLISHABLE_KEY="puclic-key"
SECRET_KEY="secret-key"
```

---

##### Ajouter Stripe à l'initializer de Rails

-   Même démarche que pour Legacy : il s'agit de créer un fichier `stripe.rb` dans `config/initializers`. et d'y ajouter les lignes suivantes :

```ruby
 Rails.configuration.stripe = {
    :publishable_key => ENV['PUBLISHABLE_KEY'],
    :secret_key      => ENV['SECRET_KEY']
  }Stripe.api_key = Rails.configuration.stripe[:secret_key]
```

Attention à que les dénomination soit identique pour les key

---

##### Ajouter stripe à l'application pour l'appeler

Aller dans `app/views/layouts/application`

Ajoute quelque part dans la balise **head**

```html
<script src="https://js.stripe.com/v3/"></script>
```

#### 4- Implémentation

##### Ajouter les premières routes

Dans un premier temps il faut créer des routes pour les redirections lié à Stripe. 

Dans le fichier `config/routes.rb`, ajouter les lignes suivantes :

```ruby
scope '/checkout' do
    post 'create', to: 'checkout#create', as: 'checkout_create'
    get 'success', to: 'checkout#success', as: 'checkout_success'
    get 'cancel', to: 'checkout#cancel', as: 'checkout_cancel'
end
```

Décorticons le code : 

-   La ligne `post 'create'` va représenter la demande concrète de création d'une session sécurisée de paiement Stripe. Schématiquement, cette requête `POST` est envoyée à notre serveur, qui "fait suivre" le tout à Stripe via des appels d'API, qui lui-même nous renverra du contenu à l'écran.

> Le système de Stripe veut que lors d'une session de paiement, on indique 2 URLs de redirection : une URL `success` sur laquelle on atterrit lorsque la session arrive à son terme, et une URL `cancel` lorsque la session est annulée par le client ou que le paiement échoue.

Pourquoi le scope ?

-   La notion de `scope`, tout comme celle de `namespace`, peut être vue comme un "pack" de routes qui sera accompagné de son ou ses controllers.
-   Si le sujet vous branche, je vous laisse apprécier la [différence entre scope et namespace](https://devblast.com/b/rails-5-routes-scope-vs-namespace).
-   Ici, j'ai choisi le `scope` pour minimiser la quantité de code à produire. Avec cette configuration de routes et un seul et unique controller `checkout`, j'aurai tout ce qu'il me faut pour exécuter le paiement sur mon app.

Différence avec **resources**

-   Ca pourrait sembler être une bonne idée... Mais en fait pas tant que ça 
-   Je m'explique : dans mon `scope` checkout, j'ai déjà mes deux routes customisées `success`et `cancel`, qui sortent des clous si on utilise un `resources`.
-   Par ailleurs, en partant sur un `resources`, on crée par défaut des actions "edit", "update", "delete" etc. qui n'ont pas vraiment lieu d'être ici. [Bon chance](https://www.youtube.com/watch?v=cOsqUta2ol4&feature=youtu.be&t=45) si vous voulez permettre à l'utilisateur d'éditer ses infos de paiement sur Stripe avec un combo edit/update 😅
-   Bref, la seule route du schéma de `resources` qui compte, c'est la ligne `post 'create'`, donc autant s'en contenter !

---

##### Créer le bouton de paiement

Dans notre **view** créer un bouton de paiment est via un `button_to`. 

```ruby
<%= button_to "Passer commande (NEXT GEN)", checkout_create_path(total: MONTANT À PAYER), class: "btn btn-primary", remote: true %>
```
> Exemple de création de bouton

Si on le décrypte ? 

-   `button_to` permet d'exécuter sans problème la requête `POST`, a.k.a l'action de créer la session. For some reason, si on met un `link_to` ça ne fonctionnera pas 

-   Il est important ici de passer comme argument un `MONTANT À PAYER`.

-   Charge à chacun donc d'extraire le prix du produit/panier et de l'insérer ici.

-   Dans le contexte de la boutique en ligne, nous avions codé ceci : `(total: @cart.total)`. Cela permettait de récupérer le montant final du panier de l'utilisateur, afin que le paiement soit basé sur un prix cohérent.

-   Si vous ne l'avez pas encore codé, en attendant, vous pouvez toujours écrire en dur : `(total: 10)`. De cette façon, le produit vaudra 10 euros dans le paiement effectué sur le formumaire Stripe.

-   Enfin, `remote: true` est une requête AJAX, qui s'avèrera indispensable pour "injecter" du code Javascript dans notre page HTML. Et ce code Javascript... est tout simplement le formulaire de paiement Stripe lui-même ! Bref, impossible de s'en passer 

---

##### Connecter le tout avec le controller


Commencer par créer un controller pour gérer Stripe.

```ruby
rails g controller checkout
```

Puis dans le **controller**, ajouter : 

```ruby
class CheckoutController < ApplicationController

    def create
    @total = params[:total].to_d
    @session = Stripe::Checkout::Session.create(
      payment_method_types: ['card'],
      line_items: [
        {
          name: 'Rails Stripe Checkout',
          amount: (@total*100).to_i,
          currency: 'eur',
          quantity: 1
        },
      ],
      success_url: checkout_success_url + '?session_id={CHECKOUT_SESSION_ID}',
      cancel_url: checkout_cancel_url
    )
    respond_to do |format|
      format.js # renders create.js.erb
    end
  end

  def success
    @session = Stripe::Checkout::Session.retrieve(params[:session_id])
    @payment_intent = Stripe::PaymentIntent.retrieve(@session.payment_intent)
  end

  def cancel
  end

end
```

Quelques précision : 

- Le **moment total du paiement** visible dans le bouton est précisé ici avec `@total = params[:total].to_d` 

- Il faut aussi préciser à stripe deux routes de redirection pour les deux pages de succes ou echec de paiement. 
>		`success_url: checkout_success_url + '?session_id={CHECKOUT_SESSION_ID}`>	`cancel_url: checkout_cancel_url`

-   Le paragraphe `respond_to do...` reprend la requête AJAX `remote: true` vue précédemment, pour injecter du contenu Javascript dans la page `create.js.erb` , qui sera une sorte de "réceptacle" à notre formulaire de paiement.

-   Le code `@session` de la méthode "success" vise à extraire de l'info sur la session de paiement qui vient d'avoir lieu. Le code `@payment_intent`, quant à lui, vise à extraire le montant qui a _réellement_ été payé par l'utilisateur. Logique, nous sommes sur la page `success`, donc forcément celà signifie que l'utilisateur aura bien payé son produit.

---

##### Ajouter du contenu dans les views checkout

Il faut maintenant faire en sorte de générer la page qui sera utilisé pour faire les paiement. 

Dans `app/views/checkout` , créer plusieurs fichiers : 

- `create.js.erb`

```ruby
const stripe = Stripe('<%= Rails.configuration.stripe[:publishable_key] %>');
stripe.redirectToCheckout({
  sessionId: '<%= @session.id %>'
}).then(function (result) {
  console.log(result.error.message);
});
```

- `success.html.erb`

```html
Succès  
Nous avons bien reçu votre paiement de <%= number_to_currency(@payment_intent.amount_received / 100.0, unit: "€", separator: ",", delimiter: "", format: "%n %u") %>.  
Le statut de votre paiement est : <%= @payment_intent.status %>.
```

- `cancel.html.erb`

```html
Echec  
Le paiement n'a pas abouti.
```

##### En cas de probleme dans le controller 

Boris à partager un code de remplacement pour le controller 

```ruby
class CheckoutController < ApplicationController
  def create
    @total = params[:total].to_d
    @session = Stripe::Checkout::Session.create(
      payment_method_types: ['card'],
      line_items: [
        {
          price_data: {
            currency: 'eur',
            unit_amount: (@total*100).to_i,
            product_data: {
              name: 'Rails Stripe Checkout',
            },
          },
          quantity: 1
        },
      ],
      mode: 'payment',
      success_url: checkout_success_url + '?session_id={CHECKOUT_SESSION_ID}',
      cancel_url: checkout_cancel_url
    )
    redirect_to @session.url, allow_other_host: true
  end

  def success
    @session = Stripe::Checkout::Session.retrieve(params[:session_id])
    @payment_intent = Stripe::PaymentIntent.retrieve(@session.payment_intent)
  end

  def cancel
  end
end
```

Il spécifie qu'après ça, le `create.js.erb` n'est plus utile et peut être supprimé. 