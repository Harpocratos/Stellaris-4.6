# Jobs
# Updated: 2026-10-20
#
# One entry defines one job. All fields are optional unless marked Required.
# Defines named below are in common/defines/00_defines.txt.
#
# A job is an object on a colony that pops are assigned to. Its production, upkeep, and modifiers
# scale with its output multiplier. See "Job output". The stratum of a job is its pop category.
#
# job_test_01 = {
#
#	### Identity ###
#
#	category = <pop_category_key>				# Stratum of the job. See ../pop_categories/00_README.txt.
#	swappable_data = {}							# Name, icon, and description swaps. See "Swaps".
#	tags = { <job_tag_key> }					# Job tags.
#	triggered_tags = {}							# Repeatable. Job tags that apply while a trigger is true.
#												# Scope: colony.
#	auto_generate_description = no				# Default yes. If yes, the description is generated from the job
#												# output.
#
#	### Availability ###
#
#	possible_pre_triggers = {}					# Fast checks before possible. See 000_pretriggers.txt.
#	possible_precalc = can_fill_worker_job		# Precalculated game rule check. Values: can_fill_drone_job,
#												# can_fill_worker_job, can_fill_specialist_job,
#												# can_fill_ruler_job, can_fill_precursor_job.
#	possible = {}								# Trigger, scope: pop group. Pops of the group can be assigned to the job.
#	weight = {}									# Scriptable weight, scope: pop group. Default 1. A negative
#												# weight excludes the job. See "Job weight".
#	is_capped_by_modifier = no					# Default yes. If yes, job assignment stops assigning pops when
#												# workforce reaches the maximum workforce. Bonus workforce is not
#												# limited. See "Maximum workforce".
#												# Pops whose current category has a higher rank than this job's
#												# category cannot take the job, unless can_change_category of
#												# this job's category fails for them.
#												# If no, the job has no workforce limit.
#	allow_only_same_rank_pops = yes				# Default no. If yes, the rank of the current category of a pop
#												# group must equal the rank of this job's category. If
#												# can_change_category of this job's category fails for the pop
#												# group, there is no rank check.
#	first_come_first_served = yes				# Default no. If yes, job assignment assigns pops to this job
#												# before every job without it, whatever the stratum rank.
#	is_pre_sapient = yes						# Default no. If yes, only sapient pop groups can take the job.
#												# No effect with ignores_sapience = yes. Despite the name, the
#												# code requires sapience, not pre-sapience. Not used in vanilla.
#	ignores_sapience = yes						# Default no. If yes, is_pre_sapient has no effect. No other
#												# effect, so it does nothing in vanilla.
#	purge = <purge_type_key>					# Purge type key. The only effect: pops assigned to the job add no
#												# diplomatic weight. Not used in vanilla.
#
#	### Output ###
#
#	# Every field in this section is multiplied by the output multiplier of the job:
#	# (workforce + bonus workforce) ÷ define NPop.POP_BULK_UNIT_SIZE (100). See "Job output".
#
#	resources = {}								# Production and upkeep, scope: colony.
#	overlord_resources = {}						# Production and upkeep for the overlord of the owner. The overlord
#												# pays and receives them. None when the owner has no overlord or
#												# the colony is occupied. Scope: colony.
#	planet_modifier = {}						# Planet modifier applied to the colony.
#	country_modifier = {}						# Country modifier applied to the owner.
#	system_modifier = {}						# System modifier applied to the system of the colony.
#	triggered_planet_modifier = {}				# Repeatable. Planet modifier applied to the colony.
#												# Scope: colony.
#	triggered_country_modifier = {}				# Repeatable. Country modifier applied to the owner.
#												# Scope: colony.
#	triggered_system_modifier = {}				# Repeatable. System modifier applied to the system of the
#												# colony. Scope: colony.
#	triggered_planet_pop_group_modifier_for_all = {}
#												# Repeatable. Pop group modifier applied to every pop group on the
#												# colony, × the output multiplier of the job. A modifier that
#												# divides over pop groups is also × group size ÷ colony pops.
#												# Scope: colony.
#	triggered_planet_pop_group_modifier_for_species = {}
#												# Repeatable. Pop group modifier applied to each pop group on the
#												# colony for which the trigger is true, × the output multiplier of
#												# the job. A modifier that divides over pop groups is split by
#												# size among those pop groups. Scope: pop group.
#
#	### Interface and AI ###
#
#	can_set_priority = no						# Default yes. If yes, the player can set a priority for the job.
#												# Only with is_capped_by_modifier = yes.
#	can_be_automated = no						# Default yes. The job can take automated workforce.
#	contributes_to_diplo_weight = no			# Default yes. If yes, the pops assigned to the job add
#												# diplomatic weight. A job with purge never adds it. See
#												# "Diplomatic weight".
#	exempt_from_ai_amenity_prioritization = yes	# Default no. If yes, AI amenity adjustment does not change the
#												# job.
#	count_as_available_for_ai = yes				# Default no. If yes, the AI counts pops assigned to the job as
#												# available. AI resettlement moves only these pops. The AI
#												# evaluates a building or district for a colony only when the
#												# colony has these pops, or the building or district sets
#												# ai_estimate_without_unemployment = yes.
#	auto_trait_prio = { <trait_key> }			# Trait preference, in order, for the automatic modification of
#												# pops assigned to the job.
#
#	### Leader generation ###
#
#	# These fields change how often a leader background gets this job. They do not
#	# change the ethic of the leader.
#
#	leader_background_weight = 0				# Applies to every leader. Scriptable value, scope: colony.
#	leader_background_class_weight = {}			# Applies when the leader has the class. Key: leader class key.
#	leader_background_ethic_weight = {}			# Applies when the empire holds the ethic, not the leader.
#												# Key: regular tier of the ethic.
#												# See "Leader generation" in ../leader_classes/00_README.txt.
#
# }
#
#
# ### Job weight ###
#
# Job assignment assigns pops in order of stratum rank, then job weight.
#
#	job weight =
#		weight									# The weight field. A negative weight skips the
#												# workforce factor below. For example, with
#												# Σ Workforce + Σ Bonus = 0.5, a weight of 10
#												# gives 10 × 1.5³ = 33.75, and a weight of −5
#												# stays −5.
#		× (
#			1
#			+ Σ Workforce						# pop_workforce_mult and
#												# pop_<job_key>_workforce_mult.
#			+ Σ Bonus							# pop_bonus_workforce_mult,
#												# pop_<job_key>_bonus_workforce_mult, and
#												# pop_cat_<category_key>_bonus_workforce_mult.
#		) ^ POP_JOB_WORKFORCE_WEIGHT_POWER		# Define NPop.POP_JOB_WORKFORCE_WEIGHT_POWER
#												# (3).
#
# The modifiers are read from the pop group.
#
#
# ### Workforce sources ###
#
# Job assignment rebuilds the workforce of each job in this order:
#
#	1. Automated workforce, only with can_be_automated = yes and a workforce limit above 0.
#	2. Pop groups fill the rest. A capped job stops at the maximum workforce.
#	3. Virtual workforce replaces step 2 for capped jobs. It applies when the owner has the
#	   country flag, or the colony carrier has the carrier flag, named by define
#	   NGameplay.VIRTUAL_JOBS_FLAG ("virtual_jobs").
#
# A virtual capped job that at least one pop group can take:
#
#	Workforce								# min(maximum workforce, workforce limit), rounded down.
#	Assigned pops							# None. On this colony, pops can only work jobs with
#											# is_capped_by_modifier = no.
#	Automated workforce						# Adds nothing to the output of the job. The owner still
#											# pays the upkeep and receives the production of the
#											# automation_resources of the pop category.
#	Virtual pop group						# Set by each pop group that can take the job, in
#											# assignment order. The last one stays.
#	Bonus workforce							# From the virtual pop group. Replaces the automated bonus.
#
# For example, a job with a maximum workforce of 200 and an automated workforce of 100 has an
# output multiplier of 2.0 on both a normal and a virtual colony, and applies
# automation_resources × 1.0 on both.
#
# Each job has two limits, both between 0 and its maximum workforce. Only the owner of the
# colony changes them, and only for a job with can_set_priority = yes and
# is_capped_by_modifier = yes.
#
#	Workforce limit							# The job slider and buttons in the planet view, or the
#											# AI.
#	Automated workforce limit				# The automated workforce slider in the planet view.
#											# Only with can_be_automated = yes. It cannot exceed
#											# the automated workforce the colony provides.
#	Maximum workforce rises					# Both limits rise by the same amount.
#	Maximum workforce falls					# A limit falls only when it is above the new maximum.
#
#	automated workforce = min(
#		job_<job_key>_add
#		× min(
#			Σ Automation,						# planet_district_automated_workforce and
#												# job_<job_key>_automated_workforce_mult, on
#												# the colony.
#			AUTOMATED_WORKFORCE_MAX_PERC		# Define NGameplay.AUTOMATED_WORKFORCE_MAX_PERC
#												# (1.0).
#		),
#		workforce limit,
#		automated workforce limit
#	)
#
#
# ### Job output ###
#
#	output multiplier = max(
#		0,
#		(
#			Workforce
#			+ Bonus workforce
#		)
#		÷ POP_BULK_UNIT_SIZE					# Define NPop.POP_BULK_UNIT_SIZE (100).
#	)
#
#	workforce =
#		Automated workforce						# See "Workforce sources".
#		+ Σ (									# Each pop group assigned to the job.
#			Assigned pops
#			× (
#				1
#				+ Σ Mult						# pop_workforce_mult and
#												# pop_<job_key>_workforce_mult.
#			)
#		)
#
#	bonus workforce =
#		Automated workforce
#		× bonus_automated_workforce_mult		# Modifier on the colony.
#		+ Σ (									# Each pop group assigned to the job.
#			Workforce of the pop group
#			× Σ Bonus							# pop_bonus_workforce_mult,
#												# pop_<job_key>_bonus_workforce_mult, and
#												# pop_cat_<category_key>_bonus_workforce_mult.
#		)
#
# The pop group workforce modifiers are read from each pop group. For example, 125 workforce
# applies the 1.25× the output. A virtual job uses a different workforce. See "Workforce
# sources". automation_resources of the pop category scales with automated workforce only.
#
#
# ### Maximum workforce ###
#
# Only for a job with is_capped_by_modifier = yes. The modifiers are read from the colony. The
# result is in workforce: 100 is one job at full output. For example, job_criminal_per_pop =
# 0.05 on a colony with 1000 sapient pops adds 50.
#
#	maximum workforce =
#		(
#			Σ Base								# job_<job_key>_add, job_<job_key>_per_pop × the number
#												# of sapient pops on the colony, and
#												# job_<job_key>_per_crime × the crime of the colony.
#												# Each count is used as is, and only when above 0.
#		)
#		× (
#			1
#			+ Σ Mult							# job_max_workforce_mult and
#												# job_<job_key>_max_workforce_mult.
#		)
#		+ Σ Add									# job_max_workforce_add and
#												# job_<job_key>_max_workforce_add.
#
#
# ### Diplomatic weight ###
#
# For each pop group assigned to a job with contributes_to_diplo_weight = yes:
#
#	diplomatic weight =
#		Assigned pops
#		× DIPLOMACY_WEIGHT_POP_BASE				# Define NGameplay.DIPLOMACY_WEIGHT_POP_BASE
#												# (0.01).
#		× (
#			1
#			+ DIPLOMACY_WEIGHT_POP_HAPPINESS	# Define
#												# NGameplay.DIPLOMACY_WEIGHT_POP_HAPPINESS (2.0).
#			× Happiness							# Happiness of the pop group.
#		)
#
# A pop group with no happiness, such as one of a species that the owner does not give
# happiness, skips the happiness term.
#
#
# ### Swaps ###
#
# swappable_data contains one default block and 0 or more swap_type blocks.
#
#	swap_type								# Replaces name, icon, and description while its trigger is true.
#	trigger									# Optional. A swap without a trigger is always true.
#	weight									# Default 0. The true swap with the highest weight applies.
#											# If weights are equal, the first swap in the list applies.
#
# Each swap starts as a copy of the default block. Write the default block first.
#
#	swappable_data = {
#		default = {
#			icon = politician					# Icon key. Default: the job key.
#			building_icon = building_capital	# Sprite of the job entry in the planet view and the
#												# Synaptic Lathe view. The file is
#												# gfx/interface/icons/buildings/<key>.dds.
#			condition_string = RULER_JOB_TRIGGER
#												# Loc key for the job requirements text.
#			desc = <loc_key>					# Default: job_<key>_desc.
#		}
#		swap_type = {
#			name = executive					# Display key, as job_<name>.
#			trigger = {}						# Trigger, scope: colony.
#			weight = 5							# Scriptable value, scope: colony.
#			icon = executive
#			desc = job_executive_desc
#		}
#	}
#
# A swap is not a job. A swap name needs no job to display.
# 99_swap_jobs.txt defines jobs with possible = { always = no }. They let swap names pass the
# job key check at load, for example in leader_background_job_weight. Triggers that compare
# jobs, such as num_assigned_jobs or has_background_job, never match them.
