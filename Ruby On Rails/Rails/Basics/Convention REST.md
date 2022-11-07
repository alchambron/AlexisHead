Related to : [[Rails]]

### REST

Convention permettant de structurer la manière dont on conçoit les routes.

Exemple : 

- Avant la mise en place de la convention
```ruby
/check_order?order_id=2 
/place_new_order 
/pizza_details?type=1 
/pay_for_my_order?order_id=12 
/cancel_order?order_id=3 
/expedite_order?order_id=13
```

- Après la mise en place de REST
```ruby
GET /orders/2 
POST /orders 
GET /pizzas/1 
POST /orders/12/payments 
DELETE /orders/3 
POST /orders/13/expeditions
```

On remarque cette logique prenant en consideration surtout les **nom** et les **ressources** des éléments. Par exemple les verbes vont très vite être supprimé (`check` est supprimé ligne 1).
On remarque aussi la logique des id, permettant de structuer quelle seront nos routes dynamiques...

Lorsque 
