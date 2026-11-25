# Agendas
# -----------------------
# Agendas appear in the empire council view.
#
#  EXAMPLE
#  -----------------------
#  All scopes are this/root = country
#
#
# example_agenda = {							# For loc, it needs council_agenda_EXAMPLE_AGENDA_name and council_agenda_EXAMPLE_AGENDA_desc
# 	agenda_cost = <int>							# Can be a value or a global variable, like @base_agenda_cost
# 	agenda_cooldown = <int>						# (Optional) Overrides COUNCIL_AGENDA_COOLDOWN define, how many days until the agenda can be selected again
# 	potential = {}								# Does it appear on the list? # default/empty: Hide
# 	allow = {}									# Is it selectable?
# 	modifier = {								# Modifier(s) active while the agenda is being enacted
#		custom_tooltip = <loc_key>				# (Optional) Replaces the modifier description with a custom loc string
#		show_only_custom_tooltip = <yes/no>		# (Optional) If yes (default), hides individual modifier lines and shows only the custom_tooltip
#	}
#	init_effect = {								# (Optional) Effect triggered when the agenda is selected.
#	}
#	on_cancel = {								# (Optional) Effect triggered when the agenda is replaced or removed before it is launched.
#	}
# 	effect = {									# (Optional) Effect triggered when the agenda is launched.
# 	}											# If you need a tooltip, the loc key needed is council_agenda_agenda_EXAMPLE_AGENDA_effect
# 	agenda_finish_modifier_duration = <int>		# Optional, Overrides the COUNCIL_AGENDA_FINISH_MODIFIER_DURATION value to define how many days the agenda's finish_modifier lasts for
# 	finish_modifier = <static_modifier>			# Static modifier applied when the agenda is launched
# 	ai_weight = {}								# (Optional) AI weights
# }
