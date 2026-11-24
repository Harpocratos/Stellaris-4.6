# AI Budget
#
# One entry defines one AI budget category.
#
# An AI budget entry tells the AI how much of one resource to set aside for one purpose.
#
# ai_budget_test_01 = {
#
#	resource = <resource>						# Resource the budget covers.
#	type = expenditure							# One of: expenditure, upkeep.
#	category = <economic_category>				# Economic category the budget belongs to.
#												# The error log warns about a category that needs no AI budget.
#												# It does not warn about a category that is missing one.
#
#	potential = { <trigger> }					# The AI skips the entry when this fails. Country scope.
#
#	weight = {									# Share of total income to spend here.
#		weight = 0.2							# The values are relative, not absolute. The game adds every weight
#		modifier = {							# together, then gives this entry its own share of that total.
#			factor = 2.5						# So the real share is this weight divided by the sum of all weights.
#		}
#	}
#
#	desired_min = {								# Lowest amount the AI tries to hold in the budget. A guideline only.
#		base = 1000								# Below this level the AI works harder to reach it.
#	}											# Income under this figure keeps the minimum out of reach.
#												# Heavy use of this field can allocate the same resource twice.
#
#	desired_max = {								# Highest amount the AI tries to hold in the budget. A guideline only.
#		base = 1500								# With many static maxes set, and fractions that push the AI past all
#	}											# of them, it probably will not correct far enough to sit below every max.
#												# It does correct downwards, and moves what it cuts to another budget.
#
# }
#
# Rules
#
#	A category used here must have use_for_ai_budget = yes in economic_categories.
#	Several entries may share the same category and resource.
#
# File layout
#
# The prefix groups the files by resource class. Order does not matter, and no two files share an
# entry key.
#
#	00	energy, food, minerals
#	01	alloys, consumer goods, biomass, trade
#	02	exotic gases, rare crystals, volatile motes
#	03	astral threads, minor artifacts, nanites, dark matter, living metal, zro
#	04	advanced logic, influence, unity
#
# The sr_ prefix on the dark matter, living metal and zro files matches their resource keys.
