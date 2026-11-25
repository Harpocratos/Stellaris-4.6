# Colony Types
#
# One entry defines a single colony designation. Every colony holds exactly one. It supplies the name,
# icon and tooltip, the modifiers the designation grants, and the hints the AI uses to judge it.
#
# Selection
#
# The engine keeps every entry whose potential passes, then takes the highest weight_modifier. Ties go
# to the entry that loaded first. Both evaluate in colony scope with FROM set to the controlling
# country. A designation set by hand overrides the pick until its potential fails.
#
# Weights compare against every other entry, so existing entries add @stickiness while current to stop
# a colony flipping between two designations of near equal weight.
#
# Localization
#
#	<key>		name
#	<key>_desc	mechanical description
#	<key>_tt	flavor text, shown delayed in the tooltip
#
# A key with no loc entry prints as raw text.
#
# Fields
#
# The list below comes from the fields the engine reads for this database.
#
# colony_type_test_01 = {
#
#	potential =											# trigger, scope = colony
#	weight_modifier =									# value
#	icon =												# value
#	custom_tooltip =									# value
#	planet_modifier =									# value
#	triggered_planet_modifier =							# triggered modifier
#	triggered_planet_pop_group_modifier_for_all =		# triggered modifier
#	triggered_planet_pop_group_modifier_for_species =	# triggered modifier
#	ai_building_set_affinity =							# block
#	ai_resource_conversion =							# block
#	ai_resource_current_conversion =					# block
#
# }
#
#	potential
#		Gates the designation. Also gates its place in the player's list, and clears a manual choice.
#
#	weight_modifier
#		Base value plus modifier blocks, read as a plain weight for the pick above.
#
#	icon
#		Sprite key. Defaults to the interface COLONY_TYPE_DEFAULT_SPRITE define.
#
#	custom_tooltip
#		A loc key. Its text is appended to the designation tooltip under the name. No entry sets it
#		today. The orphaned col_*_custom strings in the loc files are left over from when some did.
#
#	planet_modifier
#		The static modifier granted while active. Named after the designation in tooltips.
#
#	triggered_planet_modifier
#		Colony modifiers gated by their own potential, such as a galactic community resolution.
#
#	triggered_planet_pop_group_modifier_for_all
#		Modifiers for every pop group, gated the same way. One flagged as divided over pop groups is
#		spread across them instead of given to each.
#
#	triggered_planet_pop_group_modifier_for_species
#		Parsed but inert here. Nothing reads it back for a designation and no entry sets it. Use the
#		for_all variant. It works on buildings, deposits, traits and pop categories.
#
#	ai_building_set_affinity
#		Building set keys with a multiplier each. The AI weights a building, zone or district by the
#		single highest multiplier whose set it belongs to, so a foundry designation favors zones
#		carrying the alloy set. A district takes the best across the zones its slots allow. No match
#		weights at one, and a multiplier of one or below never applies, so these only promote.
#
#	ai_resource_conversion
#		Resource table of multipliers, one by default, telling the AI how output would change if it
#		switched to this designation. Needed only where the designation rewrites district jobs, which
#		the AI cannot read from modifiers. The forge and factory designations are why it exists.
#
#	ai_resource_current_conversion
#		The same table for the designation the colony already holds, so the AI compares like with
#		like. Set both or neither.
#
# File layout
#
# Keys must be unique across the folder. The split does not affect selection.
#
#	00_colony_types.txt					standard planets
#	01_habitat_colony_types.txt			habitats
#	02_special_planet_colony_types.txt	ring world, ecumenopolis, machine, hive, cosmogenesis, nanotech
#	03_wilderness_colony_types.txt		wilderness
#	04_nonplayable_colony_types.txt		fallen empire, pre-FTL, infested, contingency
#	05_nomad_colony_types.txt			arkships
