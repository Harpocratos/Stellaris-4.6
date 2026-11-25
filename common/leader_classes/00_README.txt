# Leader Classes
# Updated: 2026-10-20
#
# One entry defines one leader class. All fields are optional unless marked Required.
# Defines named below are in common/defines/00_defines.txt.
#
# Loc keys:
#
#	<class_key>								# Displayed name. Not configurable.
#	<class_key>_with_icon					# Displayed name with icon. Not configurable.
#	<class_key>_plural						# Default for name_plural.
#	<class_key>_description					# Default for description.
#
#
# ### Skill modifiers ###
#
# Static modifiers in common/static_modifiers, named skill_<class_key><suffix>.
# The applied value is the modifier × the effective skill level of the leader: the earned level
# plus bonus levels such as <class>_skill_add.
#
#	skill_<class_key>							# Applies to the leader in every location.
#	skill_<class_key>_army						# Applies to the leader while the location is an army.
#	skill_<class_key>_navy						# Applies to the leader while the location is a ship.
#	skill_<class_key>_colony_governor			# Applies to the leader while the leader governs a colony, on any
#												# colony carrier.
#	skill_<class_key>_background_colony_governor
#												# Applies to the leader while the leader governs their background
#												# colony.
#	skill_<class_key>_sector_governor			# Applies to each colony in the sector with no governor.
#												# Excludes occupied colonies and colonies the sector owner does not own.
#
# Renaming a class key requires renaming these six modifiers. A skill modifier that
# common/static_modifiers does not define has no effect and logs no error. Exception: a missing
# _sector_governor modifier fails an assertion.
#
#
# leader_class_test_01 = {
#
#	### Identity ###
#
#	name = <name_key>							# Prefix for the generated modifiers. Not a loc key. Default: class key.
#	name_plural = <name_plural_key>				# Loc key for the plural form. <name_plural_key>_with_icon is the
#												# plural form with icon.
#	description = <description_key>				# Loc key for the class description.
#
#	icon = 1									# Frame number in the leader class sprites, from 1. Default 1.
#	paragon_background_selector = <asset_selector>
#												# Portrait asset selector, scope: leader. Picks the class
#												# background sprite GFX_leader_<asset> behind the portrait of every
#												# leader of the class.
#
#	### Flags ###
#
#	# Boolean. Default no, except can_have_traits, can_rule_empire, recruitable, and
#	# valid_for_leader_pool.
#	# In leader scope, every flag is also a valid value for kill_leader = { ability = <flag> }.
#
#	can_lead_army = yes							# The leader can lead armies and transport fleets.
#	can_lead_navy = yes							# The leader can lead military fleets and hero ships.
#	can_govern_planet = yes						# The leader can govern a colony, on any colony carrier, and a
#												# sector.
#	can_be_envoy = yes							# Envoy class. The leader can take envoy tasks, for example
#												# diplomacy with an empire, a spy network, first contact, or the
#												# Shroud. The class has no leader upkeep and does not show in the
#												# top bar leader list. It is not an election fallback class, and
#												# not a ruler class in the empire designer.
#	can_research_tech = yes						# Scientist class. The scientist_count trigger counts it. The
#												# player can select it for the Tempest Invocator relic sacrifice.
#												# Its trait effects use the header SCIENCE_SHIP_EFFECTS_TXT.
#	can_research_special_projects = yes			# A special project selects a ship with a leader of this class first.
#	can_crew_science_ship = yes					# The leader can crew science ships, and military ships with a
#												# scripted survey order. The starting science ship leader has
#												# this class.
#	can_crew_cultural_envoy = yes				# The leader can crew cultural envoy ships.
#	can_research_anomalies = yes				# The fleet of the leader can research anomalies.
#	can_research_archaeology_site = yes			# The fleet of the leader can excavate archaeology sites.
#	can_survey = yes							# The fleet of the leader can survey.
#	can_boost_cloaking_detection = yes			# No effect. Used only as a kill_leader ability value.
#	can_explore_rifts = yes						# The fleet of the leader can explore astral rifts.
#	can_conduct_active_reconnaissance = yes		# No effect. Used only as a kill_leader ability value.
#	can_be_assigned_to_federation = yes			# The leader can take a federation delegate seat.
#	can_be_assigned_to_galactic_community = yes	# The leader can take a galactic community seat.
#	can_be_ideology_advocate = yes				# The leader can take an ideology advocate post.
#
#	can_have_traits = no						# Default yes. No effect on traits. If no, the leader does not
#												# gain define NGameplay.LEADER_ASSIGNED_MONTHLY_EXPERIENCE (5)
#												# experience each month while assigned, and the leader tooltip
#												# shows no skill level or experience progress.
#	can_rule_empire = no						# Default yes.
#	recruitable = no							# Default yes. If no, the player cannot hire the class.
#	valid_for_leader_pool = no					# Default yes. If no, the class is not in the recruitment pool and
#												# has no pool size modifiers.
#
#	### Resources ###
#
#	resources = {								# Resource tables for one leader, scope: leader. Takes cost, upkeep, and
#												# produces. Without this block, the class has no resource effect.
#												# No upkeep for a class with can_be_envoy = yes, or when the game rule
#												# should_pay_for_leader_upkeep (common/game_rules/00_rules.txt) fails.
#		category = leader_scientists
#		cost = {
#			unity = 1							# All vanilla recruitable classes cost unity × value:leader_cost.
#			mult = value:leader_cost
#		}
#		inline_script = "paragon/leader_base_upkeep"
#												# Shared unity upkeep. It varies with empire type and skill.
#	}
#
#	### Limits ###
#
#	max_trait_points = 3						# Trait points for a starting ruler of the class in the empire designer.
#	leader_capacity = 5							# Leader count of the class above which the empire takes a penalty.
#												# If 0, country_<class>_cap_add does not exist. Only
#												# country_leader_cap_add can raise the cap of the class.
#												# Script that uses country_<class>_cap_add logs "Invalid modifier",
#												# and the value has no effect.
#	assignment_cooldown = 30					# Days. Delay after a leader leaves an assignment before the next one.
#												# Default 0.
#
#	### Compatibility ###
#
#	replaces_old_class = "old_class"			# Repeatable. When a save loads, leaders of old_class convert to
#												# this class.
#
#	### AI ###
#
#	ai_weight = {								# AI hire preference for the class.
#		base = 10
#		modifier = {}
#	}
#
#	ai_location_weight = {						# Score for one leader at one location. AI only. Used for ships,
#												# colonies, galactic community and federation seats, and ideology
#												# advocate posts. See "AI leader assignment".
#		base = 10								# Scope: leader. From: the location, which is a colony, ship, galactic
#												# community, federation, or ideology.
#		modifier = {}							# If the score is ≤ 0, the leader cannot take the location.
#	}
#
#	minimum_ai_target = 2						# Leader count of the class that the AI keeps.
#
#	### Leader generation ###
#
#	leader_background_job_weight = {}			# Avoid. Use the job fields. See "Job weight" below.
#
# }
#
#
# ### Leader Generation Details ###
#
# The background of a generated leader has a species, colony, stratum, ethic, and job. They are
# picked in this order:
#
# 1. Species. See "Species weight".
#    If no pop group is eligible, the recruitment pool and the external pool generate no leader.
#    Other leader creation that names no species uses the founder species.
# 2. Pop group of that species, from all colonies of the empire.
#    The weight is group size × stratum weight. The leader takes the colony and stratum of the group.
# 3. Ethic. See "Background ethic".
# 4. Job, from the jobs that the group has pops assigned to. See "Job weight".
#
# A leader with a gestalt background ethic has no stratum and no job.
# The tooltip shows the job before the ethic.
#
#
# ### Species weight ###
#
#	species weight =
#		Σ Size									# Size of each eligible pop group of the species.
#		× max(
#			1 + MIN_MODIFIER_MULT,				# Define NEconomy.MIN_MODIFIER_MULT (-0.9).
#			1 + Σ Trait							# leader_species_weight_mult on each species trait,
#		)										# triggered species modifiers included.
#
# A pop group is eligible if all of these are true:
#
#	The empire owns and controls the colony of the group.
#	The species of the group is sapient.
#	The group is not enslaved.
#	The group is not being purged.
#	The game rule for the leader class passes:
#
#	can_generate_military_leader_from_pop_group	# Class with can_lead_army or can_lead_navy.
#	can_generate_leader_from_pop_group			# Every other class.
#
# The same rule filters the pop groups in step 2.
#
#
# ### Stratum weight ###
#
# The stratum of a pop group is its pop category.
#
#	stratum weight = max(
#		0,
#		leader_background_weight				# Field of the pop category. Default 1.
#		+ leader_background_class_weight		# Field of the pop category. The entry for
#												# the leader class. Not used in vanilla.
#		+ Σ Ethic								# For each empire ethic, the entry for that ethic in the
#												# leader_background_ethic_weight of the pop category.
#	)
#
# A pop group with no category has a stratum weight of 1.
#
#
# ### Background ethic ###
#
# A background ethic is always a regular tier, or gestalt. If the empire holds a fanatic or absolute
# ethic, a leader with that background ethic takes its regular tier.
#
#	Starting leader							# An ethic of the pop group that the empire also holds. Regular,
#											# fanatic, and absolute tiers count as one ethic. For example, a
#											# Fanatic Militarist empire starts with a Militarist leader.
#	Starting ruler							# If the empire holds a fanatic or absolute ethic, the ruler always
#											# takes the regular tier of that ethic. The pop group is one that
#											# holds it, if one exists.
#	Leader after game start					# Any ethic of the pop group, from all pop groups. It can be an
#											# ethic that the empire does not hold.
#
#
# ### Job weight ###
#
#	job weight =
#		Assigned								# Pops of the group assigned to the job.
#		× (
#			1
#			+ leader_background_weight			# Field of the job. Default 0.
#			+ leader_background_class_weight	# Field of the job. The entry for the
#												# leader class.
#			+ Σ Ethic							# For each empire ethic, the entry for that ethic in the
#												# leader_background_ethic_weight of the job.
#			+ Σ Job								# Avoid. Not used in vanilla. The entries for the job key in the
#												# leader_background_job_weight of each empire ethic, each empire
#												# civic, and the leader class.
#			+ Σ Swap							# Avoid. Not used in vanilla. As Σ Job, for the swap name key. Only
#												# when a swap changes the job name.
#		)
#
# A job with no weight fields has a multiplier of 1 and is valid.
# A job with a weight ≤ 0 is not valid.
# If no job has a weight > 0, the job is random.
# Weight fields on the jobs in pop_jobs/99_swap_jobs.txt have no effect, because no pop can be
# assigned to these jobs.
#
#
# ### Weight fields ###
#
# Fields on jobs and pop categories. Each field changes the chance that a leader background
# gets this job or stratum. No field changes the ethic of the leader.
#
# Example on a job. A pop category takes the same fields.
#
# job_test_01 = {
#
#	leader_background_weight = 50				# Applies to every leader.
#
#	leader_background_class_weight = {			# Applies when the leader has the class. Key: leader class key.
#		official = 100
#	}
#
#	leader_background_ethic_weight = {			# Applies when the empire holds the ethic. The ethic of the
#		ethic_militarist = 25					# leader has no effect. Key: regular tier of the ethic.
#												# A fanatic or absolute empire uses the regular tier.
#	}
#
# }
#
# Each value is a number, or a block with base and modifiers. Scope: colony.
# The block form is the only method to weight a job swap, because a swap has no fields.
#
#	leader_background_ethic_weight = {
#		ethic_spiritualist = {
#			base = 0
#			modifier = {
#				add = 25
#				OR = {
#					bureaucrat_is_priest = yes
#					bureaucrat_is_death_priest = yes
#				}
#			}
#		}
#	}
#
# Rules:
#
#	base									# Always set it. A block without base uses a base of 1.
#	modifier								# All modifiers with a true trigger apply and add. Put
#											# alternatives in one OR for one application.
#	Class or ethic condition				# Use the keyed field. Keys are checked at load.
#	Other condition, for example a civic	# Use leader_background_weight with modifiers.
#	leader_background_job_weight			# Avoid. Keys: job keys or swap names. The jobs in
#											# pop_jobs/99_swap_jobs.txt make swap names valid job keys at load.
#
#
# ### Generated modifiers ###
#
# Every class generates these modifiers. <class> is the name field. Script uses them as any other modifier.
#
# Country scope:
#
#	country_<class>_cap_add					# Exists only when leader_capacity > 0.
#	country_<class>_pool_size_add			# Recruitment pool candidates of the class. Adds to the empire pool
#											# size. Exists only when valid_for_leader_pool = yes.
#	country_<class>_external_pool_size_add	# As above, for candidates of other empires. The game rule
#											# can_get_external_leader_pool_candidate decides which empires
#											# supply them.
#	<class>_initial_skill					# Earned skill levels granted once, when the empire creates a
#											# leader of the class. Read from the empire, not the leader.
#
# Leader scope:
#
#	<class>_exp_gain						# Experience gain. Shown as a percentage: 0.1 shows as +10%.
#	<class>_skill_levels					# Skill cap of the class. Flat value, clamped by define NGameplay.LEADER_MAX_SKILL_CAP (10).
#											# Shown as a percentage: 1 shows as +100%. The generic
#											# leader_skill_levels shows as a flat value.
#	<class>_skill_add						# Bonus skill levels while the modifier applies. Added to the
#											# earned level, recalculated daily, and not limited by the skill cap.
#	<class>_lifespan_add					# Years added to the lifespan. See "Lifespan" below.
#	<class>_lifespan_mult					# Multiplier on the lifespan. 0.1 adds 10%. See "Lifespan" below.
#	<class>_starting_age_add				# Years added to both ends of the starting age range.
#	<class>_starting_age_mult				# Multiplier on both ends of the starting age range. 0.1 adds 10%.
#
# Each class modifier adds to the generic modifier with the same suffix, for example
# leader_lifespan_add.
#
#
# ### Lifespan ###
#
# Lifespan is the age at which a mortal leader starts to have a chance to die of old age.
#
#	lifespan = max(
#		leader_lifespan_min,					# Modifier.
#		(
#			max(								# The first argument is define
#												# NGameplay.LEADER_LIFESPAN_DEATH_CHANCE_AGE (80).
#				LEADER_LIFESPAN_DEATH_CHANCE_AGE,
#				leader_lifespan_min
#			)
#			+ Σ Add								# leader_lifespan_add and <class>_lifespan_add.
#		)
#		× (
#			1
#			+ Σ Mult							# leader_lifespan_mult and <class>_lifespan_mult. A leader
#												# that passes the game rule is_organic_leader also adds
#												# leader_organic_lifespan_mult.
#		)
#	)
#
# Σ Mult has no floor. At −1 or lower the lifespan falls to leader_lifespan_min.
#
# Once a month, a mortal leader above the lifespan can die. The chance is 0 for an immortal
# leader and for a leader whose aging is frozen, for example in an astral rift.
#
#	monthly death chance =
#		LEADER_LIFESPAN_DEATH_CHANCE_INC		# Define NGameplay.LEADER_LIFESPAN_DEATH_CHANCE_INC (0.002).
#		× max(
#			0,
#			min(
#				Age,
#				Lifespan × LEADER_LIFESPAN_HIGH_DEATH_CHANCE_AGE
#			)
#			− Lifespan
#		)
#		+ LEADER_LIFESPAN_HIGH_DEATH_CHANCE_INC	# Define NGameplay.LEADER_LIFESPAN_HIGH_DEATH_CHANCE_INC (0.02).
#		× max(
#			0,
#			Age
#			− Lifespan × LEADER_LIFESPAN_HIGH_DEATH_CHANCE_AGE
#		)
#
# Between the lifespan and 1.2 × lifespan, the chance rises by 0.2 percentage points each year.
# Above 1.2 × lifespan, it rises by 2 percentage points each year. For example, with a lifespan
# of 80, the monthly chance is 2% at age 90, 3.2% at age 96, and 11.2% at age 100.
#
# Define NGameplay.LEADER_LIFESPAN_HIGH_DEATH_CHANCE_AGE is 1.2. A value below 1 counts as 1.
#
# The leader_lifespan trigger reads the lifespan.
#
#
# ### Starting age ###
#
# The age of a new leader is random between leader_age_min and leader_age_max. Both come from
# the first of these sources that sets them:
#
#	1. The species class.
#	2. The first species trait that sets them.
#	3. Define NGameplay.LEADER_AGE_MIN (25) and define NGameplay.LEADER_AGE_MAX (45).
#	   For an heir of a dynastic government: define NGameplay.LEADER_AGE_HEIR_MIN (18) and
#	   define NGameplay.LEADER_AGE_HEIR_MAX (26).
#
# The modifiers change each end:
#
#	leader_age_min or leader_age_max, after modifiers =
#		(
#			leader_age_min or leader_age_max	# From the sources above.
#			+ Σ Add								# leader_starting_age_add and <class>_starting_age_add. A ruler
#												# also adds ruler_starting_age_add, an heir heir_starting_age_add.
#		)
#		× (
#			1
#			+ Σ Mult							# leader_starting_age_mult and <class>_starting_age_mult. A
#												# ruler also adds ruler_starting_age_mult, an heir
#												# heir_starting_age_mult.
#		)
#
# Σ Mult has no floor.
#
#
# ### AI leader assignment ###
#
# The AI runs the assignment weekly, with one assignment per run.
#
# 1. Collect the leaders that the empire owns, that are not the ruler, that are idle, and that
#    can change location.
# 2. Collect the locations: ships, colonies, galactic community seats, and federation seats.
#    Ideology advocate posts count only when the monthly increase of the ideology is ≤ 0.
# 3. For each leader and each location the leader can take, evaluate ai_location_weight.
# 4. Assign the pair with the highest weight. A weight ≤ 0 is never assigned.
#    On a tie, the leader with the lower skill wins. If the skill is also equal, the location
#    with the lower value in this table wins:
#
#	Fleet									# Define NAI.LOCATION_WEIGHT_FLEET_MULTIPLIER (1.0) × fleet size.
#	Ship without a fleet					# size_multiplier of the ship size.
#	Colony									# Define NAI.LOCATION_WEIGHT_PLANET_MULTIPLIER (1.0) × pops.
#	Federation								# Define NAI.LOCATION_WEIGHT_FEDERATION_MULTIPLIER (1.0) × members.
#	Galactic community						# Define NAI.LOCATION_WEIGHT_GALACTIC_COMMUNITY (100) for a member,
#											# else 0.
#
# 5. If no pair has a weight > 0, the AI tries these in order until one succeeds: hire an
#    ideology advocate, move a governor to an ideology advocate post, hire for a location,
#    hire a cultural envoy crew. Hiring sorts the recruitment pool by ai_location_weight.
# 6. For the council, the AI fills only empty positions. It sorts leaders by the ai_hiring_weight of
#    the councilor type, not by ai_location_weight, and assigns the first valid leader.
#    It then hires for the first position that is still empty, at most one hire per run.
#    The assignment is a queued command, so its position still counts as empty here.
#
# Envoy tasks do not use ai_location_weight.
#
#
# ### Deprecated ###
#
#	ai_weight_for_planet_assignment				# The parser reads and discards it. Remove it from new script.
#	default_category							# The parser reads and discards it. Remove it from new script.
