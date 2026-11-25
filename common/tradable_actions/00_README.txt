# Tradable Actions
#
# One entry defines one tradable action, a row a player can put into a trade deal beside resources,
# systems and leaders. Every field is optional unless its comment says otherwise.
#
# Scopes: ROOT gives the action and FROM receives it, in every trigger, effect and weight block. Only
# on_deal_ended_recipient_effect reverses this. Each block below states its own scopes.
#
# Names: an action takes no name or description field. The key of the entry is the name on the trade row.
# The key with a _desc suffix is the delayed half of the row tooltip. The instant half is built from the
# name, the possible failure text, and the described contents of on_traded_effect.
#
# AI pricing: the action is a cost to the giver, subtracted from what the giver gets out of the deal. The
# AI accepts once the rest of the deal covers that cost.
#	fire_and_forget = yes	cost = weight
#	fire_and_forget = no	accepted_years = ( value - negotiable_value_ai_baseline ) * negotiable_value_ai_years_per_unit
#							cost = weight * ( deal_length_years - accepted_years )
# Without a negotiable value accepted_years is 0, so a treaty action costs weight for each year of the deal.
# Trade willingness then multiplies that cost. It comes from the personality of the receiving AI.
#
# Related script, usable where a country is in scope:
#	is_action_active = {			# Is the action live in a deal with that country. Pass any as the country, or
#		action = <key>				# leave with_country out, to ask about a deal with anyone. The loader also
#		with_country = <country/any>
#	}								# accepts action = any, but that form never matches anything. Do not write it.
#	trade_action_value = {			# Compares the negotiated value. Only meaningful with has_negotiable_value.
#		action = <key>
#		with_country = <country>
#		value >= 0.5
#	}
#
# trade_action_test_01 = {
#
#	### Identity ###
#
#	fire_and_forget = no					# Default no. Yes fires the action on acceptance and clears it from the
#											# deal. No makes it a treaty for the length of the deal, which is at
#											# least MIN_TRADE_DEAL_LENGTH_YEARS.
#
#	### Availability ###
#
#	potential = {							# Whether the action is listed at all. Scope = Giver, From = Receiver
#		has_overlord = from
#	}
#
#	possible = {							# Whether the listed action can be selected. A failure keeps the row
#		custom_tooltip = {					# visible and blocks proposing or accepting the deal. Checked while the
#			fail_text = my_fail_tt			# deal is put together, not while it stands. Wrap it in custom_tooltip
#			always = yes					# so the row says why. Scope = Giver, From = Receiver
#		}
#	}
#
#	active = {								# The deal is cancelled on the day this turns false. Checked daily, and
#		has_overlord = from					# only while fire_and_forget = no. Scope = Giver, From = Receiver
#	}
#
#	### Negotiated Value ###
#
#	has_negotiable_value = no				# Default no. Gives the row a spinner holding one value. Every field in
#											# this section needs it. A percentage value is held between 0 and 1. Any
#											# other value has a floor of 0 and no ceiling. The value is stored per
#											# deal side, not per action, so two negotiable actions on one side share
#											# one number and overwrite each other. Use at most one per side.
#											# Separate deals keep their own values.
#
#	default_negotiable_value = 0			# Value seeded when the player adds the action to a deal.
#	negotiable_value_is_percentage = no		# Default no. Yes shows the value as a whole percentage, so 0.75 reads
#											# 75%. No shows it to two decimals.
#
#	negotiable_value_step_size = 0.05		# Spinner step with no modifier key held.
#	negotiable_value_step_size_ctrl = 0		# Steps with Ctrl, Shift, and both held. Each one falls back to
#	negotiable_value_step_size_shift = 0	# negotiable_value_step_size while it is 0. All three apply only while
#	negotiable_value_step_size_ctrl_shift = 0
#											# negotiable_value_is_percentage = yes. When it is no, the spinner
#											# takes the same modifier steps as a resource row.
#
#	### Effects ###
#
#	on_traded_effect = {					# Runs when the deal is accepted. Its described contents also form the
#		from = {							# effect section of the row tooltip. Scope = Giver, From = Receiver
#			set_galactic_custodian = yes
#		}
#	}
#
#	on_deal_ended_sender_effect = {			# Runs on the giver when the deal ends, however it ends. Only while
#	}										# fire_and_forget = no. FROM can be invalid here, because a deal also
#											# ends when a country dies. Check exists = from before scoping into
#											# it. Scope = Giver, From = Receiver
#
#	on_deal_ended_recipient_effect = {		# Runs on the receiver when the deal ends. Only while
#		set_galactic_custodian = no			# fire_and_forget = no. This block alone reverses the convention, and
#	}										# carries the same FROM caveat. Scope = Receiver, From = Giver
#
#	### AI ###
#
#	negotiable_value_ai_baseline = 0		# Value at or below which the negotiated value buys nothing.
#	negotiable_value_ai_years_per_unit = 0	# Years the AI accepts per full unit of value above the baseline. At
#											# 50, each 0.05 of value buys 2.5 years. Both default to 0, which
#											# keeps the negotiated value out of the pricing.
#
#	ai_weight = {							# Multiplies the cost above, so nothing here can move the value at which
#		weight = 1							# the AI starts to accept. It only makes a refusal smaller or an
#											# acceptance larger. Use ai_acceptance to move that threshold.
#		modifier = {						# Scope = Giver, From = Receiver
#			factor = 2
#			from = {
#				is_galactic_custodian = no
#			}
#		}
#	}
#
#	ai_acceptance = {						# A flat bonus to the acceptance of the whole deal by the giver, applied
#		modifier = {						# outside the trade willingness multiplier. The number written here is
#			add = 8							# the number the player sees. Use add and subtract only. Every modifier
#			has_embassy = from				# needs a desc, which names the reason in the acceptance tooltip. The
#			desc = SOME_LOC_KEY				# game sums it over every action in the deal, so a term about the
#		}									# relationship counts once per action that declares it.
#	}										# Scope = Giver, From = Receiver
# }
