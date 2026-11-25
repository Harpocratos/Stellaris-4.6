# Pop categories
# Updated: 2026-10-06
#
# One entry defines one pop category. All fields are optional unless marked Required.
# Defines named below are in common/defines/00_defines.txt.
#
# A pop category is a stratum, for example ruler, specialist, or worker. Each job names one in its
# category field. Each pop group has one category.
#
# pop_category_test_01 = {
#
#	### Identity ###
#
#	rank = 3									# Default 1. A category with a higher rank shows first in the
#												# planet view and last in the resettlement view. Capped jobs
#												# reject pops of a higher rank.
#	icon = <icon_key>							# Icon file pop_cat_<icon_key>.dds.
#	display_category = <pop_category_key>		# Interface group for the category.
#	swappable_data = {}							# Icon and description swaps, scope: colony. swap_type fields:
#												# name, trigger, weight, icon, desc. See ../pop_jobs/00_README.txt.
#	is_civilian_job = yes						# Pops in the category are civilians.
#	is_unemployment_job = yes					# Pops in the category are unemployed.
#
#	### Job assignment ###
#
#	change_job_threshold = 1.14					# Default: define NPop.DEFAULT_CHANGE_JOB_THRESHOLD (1.05).
#												# Job weight multiplier for pops that already hold a job of this
#												# category, up to the number already assigned. Job assignment
#												# assigns pops in order of stratum rank, then job weight. A pop
#												# keeps its job unless a pop of the same stratum rank has a job
#												# weight above its job weight × change_job_threshold. Not applied
#												# in a reshuffle month of the job.
#	job_reshuffle_interval = 13					# Months between reshuffles of each job of this category.
#												# Default 0. If 0, no reshuffle.
#	can_change_category = no					# Default yes. Values: yes, no, pre-trigger block. See
#												# ../pop_jobs/000_pretriggers.txt.
#												# If it fails, pops cannot move to a job of another category.
#
#	### Resettlement ###
#
#	allow_resettlement = {}						# Trigger, scope: pop group.
#	resettlement_cost = {}						# Repeatable. Cost to resettle a pop group of this category. Each
#												# block holds resource amounts, an optional trigger, scope: pop
#												# group, and an optional mult, a value that multiplies the block
#												# (default 1). No category field. The amounts of every block whose
#												# trigger is true add up.
#												# No cost for a pop group that is not sapient. See "Resettlement
#												# cost".
#
#	### Output ###
#
#	# The output scales with group size ÷ define NPop.POP_BULK_UNIT_SIZE (100). For example,
#	# 125 pops apply the 1.25× the output. pop_group_modifier and triggered_pop_group_modifier
#	# do not scale.
#
#	resources = {}								# Production and upkeep of each pop group in the category,
#												# × group size ÷ define NPop.POP_BULK_UNIT_SIZE (100). The owner
#												# of the colony pays and receives them. None on an occupied
#												# colony. Scope: pop group. From: owner.
#	automation_resources = {}					# Production and upkeep added to each job of the category that
#												# has automated workforce, × automated workforce ÷ define
#												# NPop.POP_BULK_UNIT_SIZE (100). The owner of the colony pays
#												# and receives them. None on an occupied colony. Scope: colony.
#												# From: owner.
#	pop_group_modifier = {}						# Pop group modifier applied to the pop group.
#	planet_modifier = {}						# Planet modifier applied to the colony.
#	country_modifier = {}						# Country modifier applied to the owner.
#	triggered_pop_group_modifier = {}			# Repeatable. Pop group modifier applied to the pop group.
#												# Scope: pop group.
#	triggered_planet_modifier = {}				# Repeatable. Planet modifier applied to the colony.
#												# Scope: pop group.
#	triggered_country_modifier = {}				# Repeatable. Country modifier applied to the owner.
#												# Scope: pop group.
#	triggered_planet_pop_group_modifier_for_all = {}
#												# Repeatable. Pop group modifier, scope: colony.
#	triggered_planet_pop_group_modifier_for_species = {}
#												# Repeatable. Pop group modifier, scope: pop group.
#
#	### Leader generation ###
#
#	# These fields change how often a leader background gets this stratum. They do not
#	# change the ethic of the leader.
#
#	leader_background_weight = 1				# Applies to every leader. Default 1. Scriptable value, scope: colony.
#	leader_background_class_weight = {}			# Applies when the leader has the class. Key: leader class key.
#	leader_background_ethic_weight = {}			# Applies when the empire holds the ethic, not the leader.
#												# Key: regular tier of the ethic.
#												# See "Leader generation" in ../leader_classes/00_README.txt.
#
# }
#
#
# ### Resettlement cost ###
#
#	resettlement cost =
#		Σ Block									# The amounts × mult of each resettlement_cost block with a
#												# true trigger.
#		× min(
#			group size,
#			POP_BULK_UNIT_SIZE					# Define NPop.POP_BULK_UNIT_SIZE (100).
#		)
#		÷ POP_BULK_UNIT_SIZE
#		× max(
#			1 + MIN_ECONOMIC_MODIFIER_MULT,		# Define NEconomy.MIN_ECONOMIC_MODIFIER_MULT
#												# (-0.9).
#			1
#			+ pop_resettlement_cost_mult
#			+ pop_organic_resettlement_cost_mult
#		)
#
# pop_organic_resettlement_cost_mult applies only to a pop group that passes the game rule
# is_organic_pop_group. Both modifiers are read from the pop group.
