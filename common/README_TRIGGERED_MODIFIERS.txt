###################################
# Triggered Modifiers - Default
###################################
#
# key = KEY									Localization key used for the triggered modifier's name.
# potential = {}							Trigger that determines whether modifiers are applied, can be displayed in tooltips.
# modifier = {}								Modifiers applied if "potential" is true.
# mult = {}									Multiplier for the "modifier" values.
# multiplier = {}							Alternative for "mult".
#
# should_mult_desc = yes/no					Prevents the "mult" on the displayed value (default = yes)
#
# fix_key = KEY								Localization used in to clarify the "modifier"'s behavior (will be applied to each given modifier).
#											 - $NAME$ will be filled with the modifier name
#											 - $VALUE$ will be filled with the modifier value
#											Can also be used to display the current value of each modifier if "mult" or "multiplier" are used
#											 - Needed prefixes: '_mult_desc' or '_mult_desc_plural'
#											 - $MULT$ will be filled with the multiplier
#											 - $VALUE$ will be filled with the current modifier value, with the multiplier applied (not affected by 'should_mult_desc')
#
# Members other than the ones listed above are read as members of "modifier" (so modifiers can be listed outside the "modifier" block).

###############################################
# Triggered Modifiers - With trigger details
###############################################
# Possible in (last updated 27/03/2026):
# - Civic types				(common/governments/civics/)
# - Councilor types			(common/governments/councilors/)
# - Ideology types 			(common/ideologies/)
# - Psionic aura types		(common/patrons/psionic_auras/)
# - Resolution types		(common/resolutions/)
# - Traits					(common/traits/)
#
# Everything from Triggered Modifiers - Default also applies here
#
# (By default triggered modifiers are shown only if the "potential" trigger is true.)
# show_trigger_if_true = yes				If "potential" is true, the "potential" description and the "modifier" will be shown in the tooltip
# trigger_true_key_override = KEY			Localization shown instead of the "potential" description when the "potential" is true (will enable "show_trigger_if_true")
#
# (Most of the time a false "potential" grays out the modifier.)
# show_if_trigger_false = yes				If "potential" is false, every modifier will still be shown in the tooltip
# show_trigger_if_false = yes				If "potential" is false, the "potential" description will be shown in the tooltip
# trigger_false_key_override = KEY			Localization shown instead of the "potential" description when the "potential" is false (will enable "show_trigger_if_false")

#######################################################
# Triggered Modifiers - With static modifier details
#######################################################
# Used in (last updated 13/04/2026):
# - Job types			(common/pop_jobs/)
# - Resolution types	(common/resolutions/)
#
# Everything from Triggered Modifiers - Default also applies here
#
# Static modifiers in triggered modifiers are displayed properly in tooltip (with the right multiplier, custom tooltip, etc...)

#################################
# Complex Triggered Modifiers
#################################
# Used in (last updated 13/04/2026):
# - Tenet types				(common/ideologies/tenets/)
#
# key = KEY									Localization key used for the triggered modifier's name.
# potential = {}							Trigger that determines whether modifiers are applied.
# possible = {}								Trigger that determines whether modifiers are applied, can be displayed in tooltips.
# modifier = {}								Modifiers applied if "potential" and "possible" are true.
# mult = {}									Multiplier for the "modifier" values.
# multiplier = {}							Alternative for "mult".
#
# should_mult_desc = no						Prevents the "mult" on the displayed value
#
# fix_key = KEY								Localization used in to clarify the modifier's behavior (will be applied to each given modifier).
#											 - $NAME$ will be filled with the modifier name
#											 - $VALUE$ will be filled with the modifier value
#											Can also be used to display the current value of the modifier if it uses "mult" or "multiplier"
#											 - Needed prefixes: '_mult_desc' or '_mult_desc_plural'
#											 - $MULT$ will be filled with the multiplier
#											 - $VALUE$ will be filled with the current modifier value, with the multiplier applied (not affected by 'should_mult_desc')
#
# (By default, complex triggered modifiers are shown only if the "possible" trigger is true. A false "potential" will always hide them.)
# show_trigger_if_true = yes				If "possible" is true, the "possible" description and the "modifier" will be shown in the tooltip
# trigger_true_key_override = KEY			Localization shown instead of the "possible" description when the "possible" is true (will enable "show_trigger_if_true")
#
# (Most of the time a false "possible" grays out the modifier.)
# show_if_trigger_false = yes				If "potential" is false, every modifier will still be shown in the tooltip
# show_trigger_if_false = yes				If "potential" is false, the "potential" description will be shown in the tooltip
# trigger_false_key_override = KEY			Localization shown instead of the "possible" description when the "possible" is false (will enable "show_trigger_if_false")
#
# Members other than the ones listed above are read as members of "modifier" (so modifiers can be listed outside the "modifier" block).
#
# Static modifiers in triggered modifiers are displayed properly in tooltip (with the right multiplier, custom tooltip, etc...)
