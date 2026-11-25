# EXAMPLE OVERCLOCK
#overclock_arc_furnace_overdrive = {
#	icon = GFX_overclock_arc_overdrive	# icon shown on the button
#										# This icon should also have a version with the "_selected" suffix.
#	overclock_group = arc_furnace_minerals	# optional, defaults to the mode's own key. When a megastructure upgrades to a level
#										# that offers a different set of modes, the active mode is replaced by the mode in the
#										# new set that shares its group. This costs nothing and starts no cooldown. With no
#										# match in the new set, the new level's default mode is picked instead.
#										# A megastructure that offers the same modes at every level needs no grouping.
#	potential = {						# trigger, scope: megastructure. Used to check if the button should even appear
#		owner? = {
#			has_origin = origin_arc_welders
#		}
#	}
#	possible = {						# trigger, scope: megastructure. Used to check if the button should be greyed out
#										# Both potential and possible are ignored when using the set_overclock script effect.
#		owner? = {
#			has_technology = tech_mega_engineering
#		}
#		solar_system = {
#			NOT = {
#				has_star_flag = arc_furnace_burnout
#			}
#		}
#	}
#
#	resources = {						# category, cost, produces and upkeep
#		category = megastructures
#		cost = {
#			alloys = 250
#		}
#		produces = {
#			minerals = 40
#		}
#		upkeep = {
#			energy = 60
#		}
#	}
#	country_modifier = {				# modifier = {} is a deprecated alias for this
#		country_minerals_produces_mult = 0.10
#	}
#	system_modifier = {					# applies to the owner's planets and fleets in the solar system, like a starbase
#										# system modifier. It does not reach anything owned by another empire.
#		planet_jobs_minerals_produces_mult = 0.15
#	}
#	megastructure_modifier = {			# applies to the megastructure itself, so it reaches its own upkeep
#		megastructures_energy_upkeep_mult = 0.25
#	}
#	custom_tooltip = LOC_KEY			# replaces the three modifier sections above wherever this mode lists its effects,
#										# so it can state them in its own words instead. This takes priority over
#										# custom_tooltip_with_modifiers.
#	custom_tooltip_with_modifiers = LOC_KEY	# as above, but prepended to the sections rather than replacing them.
#										# Both keys resolve on a megastructure scope.
#	on_overclock_start = {				# effects, scope: megastructure. Runs every time this mode becomes the active one.
#		set_megastructure_flag = arc_furnace_overdrive
#	}
#	on_overclock_end = {				# effects, scope: megastructure. Runs every time this mode stops being the active one.
#		remove_megastructure_flag = arc_furnace_overdrive
#	}
#	ai_weight = {						# scope = megastructure, checked monthly. Also selects the starting mode: whenever no mode
#										# is stored, on creation and on reset, the highest weighted mode is picked, ties going to
#										# the first listed. Starting-mode selection reads only the flat weight and ignores the
#										# modifier blocks, so state the intended default as a base or a plain number.
#										# A mode with no ai_weight block, or a block that states no base, weighs 100.
#										# The AI only switches to a mode weighing strictly higher than the active one, so equal
#										# weights never oscillate and giving every mode the same weight means it never switches.
#										# A megastructure with no mode set yet is the exception: anything above 0 will be picked.
#		modifier = {
#			weight = 50
#			owner? = {
#				resource_income_compare = {
#					resource = minerals
#					value < 0
#				}
#			}
#		}
#	}
#}
