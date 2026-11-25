# Economic Categories
# -----------------------
#
# Economic categories are used to categorize *everything* that produces or consumes resources of any kind.
# The player country, buildings, planets, ships, jobs and megastructures all use categories, defined in the objects themselves with:
#	category = <economic_category>
#
# Categories are used to:
# - Generate new modifiers
# - Help the AI plan its economic budget (defined in ai_budget)
#
#
# GENERATING MODIFIERS FROM ECONOMIC CATEGORIES
# -----------------------
# Modifiers generated from an economic category are applied to every single building/planet/job/etc part of said category.
# For example, planet_miners_minerals_produces_mult will increase the production of every job in the planet_miners category, like
# miners, scrap miners, mote harvesting drones etc.
#
# Let's say I want to make a new modifier to specifically increase the output of scrap miners.
# I create a new economic category, set planet_miners as the parent category, and generate the modifier:
#
#	planet_scrap_miners = {
#	 	parent = planet_miners
#	 	generate_mult_modifiers = {
#	 		produces
#	 	}
#	 }
#
# I then find the scrap_miner job (in pop_jobs) and change its category from planet_miners to planet_scrap_miners.
# Since planet_scrap_miners is a child of planet_miners, Scrap Miners will now receive the effects of both
# planet_miners and planet_scrap_miners modifiers.
# IMPORTANT!  _add modifiers don't apply to children categories, only _mult ones do. This is working as intended.
# Limiting _add inheritance is necessary to avoid unintentional cascade effects.
#
# IMPORTANT!  An _add modifier is applied once per resource table filed under its category on the same object.
# Most objects declare their category once, so this makes no difference. A pop group is the exception. It holds one
# resource table from its species archetype, and one more from each trait, and once all of them used planet_pops. An _add
# modifier on planet_pops was applied once for each of those tables, and the total changes with the trait list of the
# species. Put such a modifier on a category that only one resource table uses. The archetype tables stay on planet_pops
# for this reason, and the trait tables use the hidden child category planet_pops_traits.
#
# You can also define triggered modifiers, which will apply in the same way as mult and add modifiers normally do, but with the extra condition that a trigger must return true.
# The format for these is triggered_produces_modifier, etc (see below)
# These are useful if e.g. you want to apply an effect only to biological pops. Note however that if you do something too complicated in these, and then use the modifiers in a lot
# of places, then it can have a bit of a performance impact (it will check these triggers whenever it is working out what resources a resource table contains, and there is a non-zero
# value for this triggered modifier. So not the worst, but don't go crazy!).
#
# Modifiers created by economic category can then be applied through edicts, static modifiers, etc.
#
# You can decide the category of the modifier via "modifier_category = <object e.g. country, planet, pop". This is basically helpful for performance, so the game can filter modifiers.
# The default is applicable to everything. But this means that your pop has modifiers that really don't matter to it that it inherits from the country. If you specify that the
# modifier's category should be "country", then you commit to a) applying it only to the country, and b) only using it at country level (e.g. a building is built at planet level, so
# that would not work). And then the game will filter it so that this modifier doesn't leak to any objects that are not countries.
# On the other hand, if you specify "pop", then the hierarchy of modifiers means you can apply it to a country, and it will be inherited to the country's colonies and then their pops.
# So always specify the lowest level at which it may be used.
# As a quirk of the system, you should specify the category before any triggered modifiers are declared.
#
# A log of all generated modifiers can be found at:
# Documents\Paradox Interactive\Stellaris\logs\script_documentation\modifiers.log
#
#
# EXAMPLE
# -----------------------
# category_name = {
# 	icon = "<name>"					# (Optional) set an icon from gfx/interface/icons/jobs
# 	hidden = yes					# not sure. Default = no
# 	use_for_ai_budget = yes/no		# specifies if the category can be manipulated by the files in ai_budget
# 	parent = <economic_category>	# specifies if the category has a parent
#
# 	generate_mult_modifiers = {
# 		# Only add the ones you need between:
# 		produces
# 		cost
# 		upkeep
# 	}
#
# 	generate_add_modifiers = {
# 		# Only add the ones you need between:
# 		produces
# 		cost
# 		upkeep
# 	}
#
# 	ai_use_parent_for_resources_upkeep = {
#		# This means that the AI budget will use the category's parent for all of the specified resources.
#		# Only comes into play if use_for_ai_budget = yes.
#		# This can used to combine all the energy upkeep into one bucket,
#		# because so many things need to use energy upkeep that it just becomes a mess to try to do it granularly.
# 		energy
# 		minerals
# 		food
# 		alloys
# 		consumer_goods
# 		exotic_gases
# 		rare_motes
# 		etc
# 	}
#
# 	triggered_produces_modifier = {
#		# This will generate modifiers based on the key and apply them if the triggers are true.
# 		key =
# 		use_parent_icon = yes/no
#
# 		trigger = {
# 		}
#
# 		modifier_types = {
# 			mult
# 		}
# 	}
#
# 	triggered_cost_modifier = {
#		# This will generate modifiers based on the key and apply them if the triggers are true.
# 		key =
# 		use_parent_icon = yes/no
#
# 		trigger = {
# 		}
#
# 		modifier_types = {
# 			mult
# 		}
# 	}
# }
#
#
# LOC STRINGS AND ICONS
# -----------------------
# Newly created modifiers will need localization keys, which always start with mod_.
# Example:
#		mod_planet_metallurgists_produces_mult:1 "£job_foundry£ [GetAlloyProducer] Output"
#		mod_planet_metallurgists_alloys_produces_mult:1 "£alloys£ $alloys$ from £job_foundry£ [GetAlloyProducerPlural]"
#		mod_planet_metallurgists_alloys_produces_add:0 "$mod_planet_metallurgists_alloys_produces_mult$"
#		mod_planet_metallurgists_energy_upkeep_add:0 "£energy£ $energy$ Upkeep of £job_foundry£ [GetAlloyProducerPlural]"
#
# To set an icon for a modifier, add an icon with the same name to gfx/interface/icons/modifiers.
#
