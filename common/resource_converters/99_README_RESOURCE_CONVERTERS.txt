# Example of a resource converter, to be set on a country economy module via the set_resource_converter effect.
#
# example_resource_converter = {
#	 resource_conversions = {
#		 energy = {                    # Needs to match the key for the strategic resource.
#			 should_cap = no           # default: yes. Cap the resource to the current max allowed to the country.
#			 visible = no              # default: yes. Visible for the country.
#			 visible_stockpile = no    # default: yes. Visible stockpile amount.
#			 can_buy = no              # default: yes. Can be bought on the market/acquired in trades.
#			 can_sell = no             # default: yes. Can be sold on the market/offered in trades.
#									   # If both can_buy and can_sell are false, will be hidden in market UI.
#			 bottomless = yes          # default: no. If yes: Spending always succeeds even if the stockpile is insufficient (affordability check is skipped).
#									   # Conversion alternatives (can_be_paid_with) are still tried before depleting the stockpile.
#									   # The stockpile is still capped at 0 after spending; it cannot go negative.
#			 override_trade_restriction = yes  # default: no. If yes: the country can buy/sell this resource on the market regardless of its income or
#											   # galactic market access (the normal income/galactic-market gate is skipped). Does not bypass the
#											   # resource's own tradable_in_market gate, and is still subject to the can_buy/can_sell flags above.
# 
#			 affected_situation = situation_nomad_economy  # Any income/expense of this resource will affect the progress
#														   # of all of the country's situations of this type.
#			 affected_situation_mult = 3                   # For each unit of income/expense, the situation progress will be affected by this amount
#														   # (with positive multiplier: resource income adds progress, spending decreases progress).
# 
#			 can_be_paid_with = {  # If the resource is not enough for a particular expense, alternative resources can be used to pay,
#								   # according to the specified conversion rates.
#				 # The following reads as: 1 unit of energy can be paid either by 2.4 units of minerals or 1.1 units of alloys.
#				 minerals = 2.4    # Needs to match the key for the strategic resource.
#				 alloys = 1.1      # If multiple alternative resources are specified, they will be spent in the order they are listed in the script.
#			 }
#		 }
#		 minerals = {
#			 should_cap = no
#			 visible = yes
#			 can_buy = no
#			 can_sell = no
# 
#			 affected_situation = situation_nomad_economy
#			 affected_situation_mult = 3
# 
#			 can_be_paid_with = {
#				 energy = 3.5
#			 }
#		 }
#	 }
#	visibility_overrides = {   # visibility override for resource GUI groups (interface/resource_groups/)
#							   # overrides each group's default_visible value
#							   # only affects the ones used as a category (i.e. they list several other resources)
#							   # (for individual resource groups the visible_stockpile parameter should be used instead,
#							   # found in resource_conversions above)
#		tb_operational_reserves_group = yes
#		tb_others_group = no
#	}
# }
