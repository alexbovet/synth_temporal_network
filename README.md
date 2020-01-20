Individual agent class.
    
Parameters:
-----------

ID: int
    ID of the individual

inter_distro_loc: float
    Location (mean) of the interactions (i.e. events) durations

inter_distro_scale: float
    Scale (standard-deviation) of the interactions (i.e. events) durations

inter_distro_type: string
    Type of distribution function of the interactions durations.
    Can be "exponential".

inter_distro_mod_func: function
    function that take an argument `time` and returns a tuple 
    `(loc, scale)` used as parameters for drawing time-dependent 
    interaction durations.

activ_distro_loc: float
    Location (mean) of the inter-activation (i.e. inter-events) durations

activ_distro_scale: float
    Scale (standard-deviation) of the inter-activation (i.e. inter-events) durations

activ_distro_type: string
    Type of distribution function of the inter-activation durations.
    Can be "exponential".

activ_distro_mod_func: function
    function that take an argument `time` and returns a tuple 
    `(loc, scale)` used as parameters for drawing time-dependent 
    inter-activation durations.

group: int
    ID of the group to which the individual belongs to.
    
    
    
SynthTempNetwork: a class for an agent based model generating a continuous time synthetic temporal network
        
Alexandre Bovet 2019

Parameters:
-----------

individuals: list
    List of Individual instances, i.e. the nodes of the network.
    Individual have a group id. There are N individuals and Ngroups group.

t_start: float
    Starting time of the simulation

t_end: float
    Ending time of the simulation

num_interactions_per_activation: int
    Number of interactions generated each time an individual is
    activated

next_event_method: float
    Method to choose the individual to interact with.
    Can be

    - 'random_uniform' (default): 
        uniform probability to choose any other individuals.
    - 'block_probs':
        probabilities given by a block matrix  `inter_group_probs`.
    - 'block_probs_mod': 
        probabilities given by a time-dependent function `block_prob_mod_func`.

inter_group_probs: Ngroups x Ngroups numpy array
    Contains the probabilities of inter-group interactions.

block_prob_mod_func: function
    Functions that depend on t such that `block_prob_mod_func(t)` returns
    an `inter_group_probs` matrix.

Usage:
------

The simulation is run by calling `self.run()`. All the events are stored
in 4 lists: `self.indiv_sources`, `self.indiv_targets`, 
`self.start_times` and `self.end_times`.    
