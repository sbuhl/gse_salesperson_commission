# Salesperson Commission

Based/Extend the OE partner_commission module

Autre spec, par rapport au commissions.
Un module existe dans OE: partner_commission.
Il permet de définir des commissions plan pour des referrer.
Une fois qu’un referrer a renseigné des clients, et que ce client a payé la facture,
cela va créer une purchase order et ensuite une vendor bill. 

J’aimerais appliquer le même mécanisme pour mes salesperson.
En se basant sur ce module. Pourquoi pas faire des modèles qui en héritent. 
Je pensais à faire quelque chose comme cela:

Part 1: 
commissions pour vendeurs

Part 2: commissions par bureau

SalesPerson Commission 

commission_plan.py
CommissionsPlan:
add field: 
	- commission_type : referrer | salesperson

CommissionsRule:
add field	
	- salesperson_level = related du groupe salesperson (id= module_category_salesperson_level)
		- if type = salesperson, display field in the commission rule tree view

add constrains: si type = referrer, dans la rule, on ne peut pas avoir de salesperson de set. 
Du coup, il faut peut être un onchange pour vider le champ? 

account_move.py
AccountMove
add fields:
	- commission_type
	- salesperson

purchase_order.py

sale_order.py
add fields
	- commission_type
	- salesperson
	- salesperson_level 
	- sales_commission_plan

def _compute_commission

