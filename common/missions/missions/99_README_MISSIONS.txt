# Missions are situation log tasks that have some sort of counter(s) to complete them.
# Missions are started by using the enable_mission effect.
# Missions are progressed by using the add_mission_counter or set_mission_counter effects.
# Missions can be stopped using the stop_mission effect.

# MISSION_EXAMPLE = {
# 	icon = "gfx/interface/icons/situation_log/situation_log_quest.dds"			# Icon used for the situation log entry. Overrides mission category log_icon if such exists.

# 	counter = {																	# Counter to define and track what is needed for the player to complete the mission.
# 		days_storm_rider_spend_in_storm = {										# Multiple of these can be used.
# 			max = 180
# 		}
# 	}

# 	picture = GFX_evt_cool_mission_picture										# The image used for the mission in the situation log.
# 	small_picture = GFX_small_contract_issue_picture							# The image used in the list when players Issue Contracts. Not needed for internal contracts.
# 	event_chain = totally_cool_event_chain										# OPTIONAL. The event chain this mission is part of. (Only REQUIRED for contracts)
# 	location = yes/no															# OPTIONAL, defaults to no. Sets whether the mission has a specific location or not.
# 	time_to_accept = XX															# OPTIONAL, defaults to no time limit. Sets the maximum amount of days to accept the mission before it times out. Only used for contracts.
# 	time_to_complete = XX														# OPTIONAL, defaults to no time limit. Sets the maximum amount of days to complete the mission before it fails.
# 	ai_behaviour = attack/raid													# OPTIONAL, defaults to none. Sets the AI military behaviour for this contract. 'attack' makes the AI treat the contract target system as hostile (e.g. pest control). 'raid' makes the AI raid any planet belonging to the target, not limited to the contract's target system (e.g. raid contracts).

# 	desc/desc_operator = {														# OPTIONAL, defaults to [mission_name]_desc. The description of the mission in the situation log. Supports triggered descriptions.
# 		trigger = {																# Both desc and desc_operator can be used here, prefer the latter if there is also a desc_issuer (for example for contracts).
# 			owner = {
# 				is_hive_empire = no
# 			}
# 		}
# 		text = MISSION_EXAMPLE_DESC
# 	}
# 	desc/desc_operator = {
# 		trigger = { owner = { is_hive_empire = yes } }
# 		text = MISSION_EXAMPLE_DESC_HIVE
# 	}

# 	desc_issuer = {																# OPTIONAL, defaults to [mission_name]_issuer_desc. The description of the mission in the situation log, for the issuing side. Supports triggered descriptions.
# 		trigger = {
# 			owner = {
# 				is_hive_empire = no
# 			}
# 		}
# 		text = MISSION_EXAMPLE_DESC
# 	}
# 	desc_issuer = {
# 		trigger = { owner = { is_hive_empire = yes } }
# 		text = MISSION_EXAMPLE_DESC_HIVE
# 	}

#	lore_issued = <key>															# supports scripted loc. scopes: this = issuer, from = operator
#	lore_completed = <key>														# supports scripted loc. scopes: this = issuer, from = operator
#	lore_failed = <key>															# supports scripted loc. scopes: this = issuer, from = operator

#	potential/potential_operator = {											# OPTIONAL. Trigger that determines whether the contract can be seen by a potential operator.
#	}																			# this: operator country
#																				# from: contract location
#																				# fromfrom: issuer country

#	possible/possible_operator = {												# OPTIONAL. Trigger that determines whether the contract can be accepted by a potential operator.
#	}																			# this: operator country
#																				# from: contract location
#																				# fromfrom: issuer country

#	potential_issuer = {														# OPTIONAL. Trigger that determines whether the contract can be seen as an option by a potential issuer.
#	}																			# this: issuer country
																				# from: system to issue in

#	possible_issuer = {															# OPTIONAL. Trigger that determines whether the contract can be issued by a potential issuer.
#	}																			# this: issuer country
																				# from: system to issue in

# These two effects are executed in the mission scope

# 	on_daily = {																# OPTIONAL. Effect to be run on daily update while the mission is active.
# 	}

# 	on_monthly = {																# OPTIONAL. Effect to be run on monthly update while the mission is active.
# 	}

# this: issuer
# from: the scope from the mission
# fromfrom: contract location, if applicable
# 	on_issue = {																# OPTIONAL, Contracts only, Effect to be run when a country issues up the contract
# 	}

# For all the effects below, the scopes are
#  this: operator (the country doing the mission/contract)
#  prev: issuer if applicable (the country that issued the contract)
#  from: the scope from the mission
#  fromfrom: contract location, if applicable

# 	on_accept = {																# OPTIONAL, Contracts only, Effect to be run when a country picks up the contract
# 	}

# 	abort_trigger = {															# OPTIONAL. Trigger to abort the mission.
# 	}

# 	on_cancel = {																# OPTIONAL. Effect to be run when the mission is ended early (cancelled/failed/timed out).
# 	}

# 	on_start = {																# OPTIONAL. Effect to be run when the mission is started.
# 	}

# 	on_success = {																# OPTIONAL. Effect to be run when the mission is completed.
# 	}

# 	on_stop = {																	# OPTIONAL. Effect to be run after the mission ends, in any way (success/abort/time out).

# 	}

# this: issuer
# from: the scope from the mission
# fromfrom: contract location, if applicable
#	issued_abort_trigger = {													# OPTIONAL. Trigger to abort the mission, from the issuer side.
#		
#	}

# 	sound = yes/no																# OPTIONAL, defaults to yes. Doesn't actually do anything.
# }

#	ai_weight = {																# OPTIONAL. Only used for contracts. Weight used to determine what contracts will be picked up by an AI operator.
#		weight = 1																# If the weight is equivalent between contracts, the closest contract will be selected.
#		modifier = {															# The AI will heavily prefer picking up player-issued contracts adding the PLAYER_ISSUED_CONTRACT_PREFERENCE define to the weight.
#			factor = 2															# this: operator country
#			has_origin = origin_sacred_path										# from: contract location
#		}																		# fromfrom: issuer country
# }