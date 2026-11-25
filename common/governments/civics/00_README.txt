# Civics
# Updated: 2026-10-06
#
# One entry defines one civic. All fields are optional unless marked Required.
# Defines named below are in common/defines/00_defines.txt.
#
# A civic is one part of the government of an empire, with the authority and the origin. Civics
# are selected in the empire designer and changed with a government reform.
# Origins use this database and these fields, with is_origin = yes.
# A field marked ORIGIN ONLY has no effect unless is_origin = yes.
#
# civic_test_01 = {
#
#	### Identity ###
#
#	icon = <icon_key>
#	picture = <sprite_key>						# ORIGIN ONLY. Sprite of the origin entry in the origin selection
#												# of the empire designer.
#	portrait = <portrait_key>					# ORIGIN ONLY. Selecting the origin in the empire designer sets
#												# the founder species portrait to this portrait, if a selectable
#												# portrait category contains it.
#	room = <room_key>							# ORIGIN ONLY. Selecting the origin in the empire designer sets
#												# the room background of the design.
#	city_graphical_culture = <key>				# ORIGIN ONLY. Selecting the origin in the empire designer sets
#												# the city graphical culture of the design.
#	description = <loc_key>						# Custom text under "Effects".
#	negative_description = <loc_key>			# Custom text under "Penalties".
#
#	### Availability ###
#
#	cost = 1									# Default 1. Civic points the civic uses. The total cost of the
#												# civics of an empire cannot exceed its civic points: define
#												# NGameplay.GOVERNMENT_CIVIC_POINTS_BASE (2) + max(0,
#												# country_government_civic_points_add). The modifier is truncated
#												# to an integer, and a negative total adds nothing. A cost ≤ 0
#												# logs an error and becomes 1. No effect when is_origin = yes.
#	playable = {}								# Trigger, scope: no check. If false, the civic is not listed in
#												# the empire designer or the reform window, a design that holds it
#												# is invalid, random generation and the AI never pick it, and an
#												# empire that holds it cannot be selected on hotjoin. An origin
#												# that fails is listed only when it is missing a DLC.
#	ai_playable = {}							# Trigger, scope: no check. Only for governments the AI
#												# randomizes or reforms. If false, the AI never picks the civic
#												# and removes it from its government on revalidation.
#	potential = {}								# Requirements list. See ../99_README_GOVERNMENT.txt.
#	possible = {}								# Requirements list. See ../99_README_GOVERNMENT.txt.
#	pickable_at_start = no						# Default yes. If yes, the civic is available in the empire designer.
#	modification = {}							# Default yes. If yes, the player can add or remove the civic
#												# after empire creation.
#												# Values: yes, no, trigger block. See "Modification".
#	alternate_civic_version = <key>				# Replacement civic when a reform locks this one.
#	max_once_global = yes						# ORIGIN ONLY. Maximum one empire in the galaxy.
#	advanced_start = yes						# ORIGIN ONLY. Available to advanced start empires.
#	flags = {}									# Country flags set at country creation. Reforms do not change them.
#
#	### Species ###
#
#	traits = {}									# Forced traits for the primary species. The player cannot remove them.
#	soft_traits = {}							# ORIGIN ONLY. As traits, but the government restrictions solver
#												# does not check them.
#	has_secondary_species = {}					# Title and traits for a secondary species. Galaxy generation
#												# creates the species with no pops. Script creates its pops: the
#												# vanilla origins and civics do it in generate_start_pops, in
#												# common/scripted_effects/01_start_of_game_effects.txt.
#
#	### Origin start ###
#
#	is_origin = yes								# Default no. If yes, the entry is an origin.
#	homeworld = pc_volcanic						# Planet class key. Sets both starting_colony and
#												# habitability_preference. A later starting_colony or
#												# habitability_preference in the same entry overrides one of them.
#	starting_colony = pc_volcanic				# Planet class key. Planet class of the starting colony. Galaxy
#												# generation gives it to the planet the system initializer places
#												# with ideal_planet_class. Creates no colony.
#	habitability_preference = pc_volcanic		# Planet class key. Planet class preference of the founder
#												# species. The empire designer also checks species traits against
#												# it.
#												# These three are read from the origin, then from the first civic
#												# that sets them. If none sets them, the empire uses the planet
#												# class picked in the empire designer. A nomadic empire ignores
#												# all three.
#	initializers = {}							# ORIGIN ONLY. Solar system initializer keys. If set, the empire
#												# designer offers only these initializers, and fixes the choice
#												# when there is one. Galaxy generation uses the first valid key,
#												# skipping nomad initializers for a non-nomadic empire.
#	blocks_random_machine_empire_generation = yes
#												# ORIGIN ONLY. Default no. If yes, a randomized species class for
#												# the empire is never a machine class. This covers the founder
#												# species of a random empire and a secondary species.
#	non_colonizable_planet_class_neighbor = yes	# Default no. If yes, the planets the system initializer places
#												# with ideal_design_class get a random non-colonizable starting
#												# planet class. One origin or civic with yes is sufficient. Checked
#												# before preferred_planet_class_neighbor.
#	preferred_planet_class_neighbor = yes		# Default yes. Applies to the planets the system initializer
#												# places with ideal_design_class. If yes, they get the
#												# habitability_preference class. If no, they get a random home
#												# planet class. Read from the origin or civic that supplies
#												# habitability_preference.
#	removed_planet_types = {}					# Planet class keys removed from the homeworld choices.
#	added_planet_types = {}						# Planet class keys added to the homeworld choices.
#	removed_climate_labels = {}					# Interface element names hidden in the homeworld picker.
#	added_climate_labels = {}					# Interface element names shown in the homeworld picker. Declare
#												# the element in the interface first.
#												# The homeworld choices start from define
#												# NGameplay.DEFAULT_HOME_PLANETS. Each of these four lists, when
#												# not empty, replaces the list of the species class. The sources
#												# are the origin and the civic with the most added_planet_types
#												# and removed_planet_types entries. The picker shows the origin
#												# list over the civic list. Design validation uses the civic list
#												# over the origin list, and climate labels only affect the picker.
#
#	### Modifiers ###
#
#	modifier = {}								# Country modifier applied when the empire has this civic and
#												# the civic is valid.
#	triggered_country_modifier = {}				# Repeatable. Country modifier applied when the empire has this
#												# civic and the potential trigger is true. Scope: country.
#	triggered_planet_modifier = {}				# Repeatable. Planet modifier applied to each colony of the empire,
#												# on any colony carrier, when the empire owns and controls the
#												# carrier and the potential trigger is true. Scope: colony. The
#												# civic tooltip always shows it.
#	swap_type = {}								# Repeatable. Name, flavor text, and modifier that apply while a
#												# trigger is true. See "Swap types".
#	hide_modifiers = yes						# Default no. If yes, the civic tooltip does not show the modifiers.
#	custom_tooltip_with_modifiers = <key>		# Loc key after the generated modifier text.
#	can_build_ruler_ship = yes					# Default no. No effect. The parser reads it, and nothing checks
#												# it. Not used in vanilla.
#
#	### Weights ###
#
#	random_weight = {}							# Scriptable weight for random civic selection, scope: country
#												# when an empire exists. Default 1.
#	ai_weight = {}								# Scriptable weight for AI civic selection when a new civic slot
#												# unlocks after game start, scope: country when an empire exists.
#												# Default 1. Not needed with modification = no.
#
#	### Leader generation ###
#
#	leader_background_job_weight = {}			# Avoid. Use the job fields. See "Leader generation" in
#												# ../../leader_classes/00_README.txt.
#
# }
#
#
# ### Swap types ###
#
#	Condition								# The swap applies while its trigger is true.
#	Name									# The swap name replaces the civic name, only when the swap name
#											# has a loc key.
#	Flavor text								# The loc key <name>_desc of the swap, if it exists.
#	Multiple true swaps						# The first true swap in file order applies. Each other true swap
#											# logs an overlapping type_swaps error. Make the triggers mutually
#											# exclusive.
#	No true swap							# The civic name, description, and modifier apply.
#
#		swap_type = {
#			name = ...
#			description = ...
#			negative_description = ...
#			trigger = {
#				...
#			}
#			modifier = {
#				...
#			}
#		}
#
#
# ### Modification ###
#
# Values: yes, no, or a block with two triggers.
#
#		modification = {
#			moddable_conditions_custom_tooltip = <loc_key>
#												# Loc key for the tooltip of a side with no trigger,
#												# when the civic is not fully moddable. Also used for
#												# modification = no. Default CIVIC_NOT_MODDABLE.
#			add = {}							# Trigger. The player can add the civic after empire creation.
#			remove = {}							# Trigger. The player can remove the civic after empire creation.
#		}
#
# When the empire reforms to an authority that forbids this civic:
#
#	Alternate possible						# The alternate_civic_version replaces this civic when the player
#											# selects the authority. A civic that is not removable does not
#											# block the reform. For example, civic_anglers sets
#											# alternate_civic_version = civic_corporate_anglers, which replaces
#											# it on a reform to auth_corporate.
#	No alternate							# The civic stays and blocks the reform. The player must remove it.
#											# modification = no prevents removal.
