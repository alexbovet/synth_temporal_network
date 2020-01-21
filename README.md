# Simulation of temporal networks.

Alexandre Bovet, 2019

This program consists of two main Classes : **Individual**, the class of individual agents (i.e. nodes of the network), and **SynthTempNetwork**, the class used for running the simulations and generating a continuous time synthetic temporal network where an event `(v_1,v_2,t_s,t_e)` represents an interaction between nodes (agents) v_1 and v_2 that started at t_s and ended at t_e.

The nodes are activated at different times drawn from a prescribe distribution that can be time-dependent and can be different for each node. When a node is activated it starts a new event with a given number of other nodes drawn according to probabilities given by a block model that can also be time-dependent. The duration of the events are also drawn from distributions that can be time-dependent and different for each node.


## **Individual** class parameters:

    ID: int
ID of the individual

    inter_distro_loc: float
Location (mean) of the interactions (i.e. events) durations

    inter_distro_scale: float
Scale (standard-deviation) of the interactions (i.e. events) durations

    inter_distro_type: string
Type of distribution function of the interactions durations. Can be "exponential".

    inter_distro_mod_func: function
Function that take an argument `time` and returns a tuple `(loc, scale)` used as parameters for drawing time-dependent interaction durations.

    activ_distro_loc: float
Location (mean) of the inter-activation (i.e. inter-events) durations

    activ_distro_scale: float
Scale (standard-deviation) of the inter-activation (i.e. inter-events) durations

    activ_distro_type: string
Type of distribution function of the inter-activation durations. Can be "exponential".

    activ_distro_mod_func: function
function that take an argument `time` and returns a tuple `(loc, scale)` used as parameters for drawing time-dependent inter-activation durations.

    group: int
ID of the group to which the individual belongs to.
    
## **SynthTempNetwork** class parameters:

    individuals: list
List of Individual instances, i.e. the nodes of the network.Individual have a group id. There are N individuals and Ngroups group.

    t_start: float
Starting time of the simulation

    t_end: float
Ending time of the simulation

    num_interactions_per_activation: int
Number of interactions generated each time an individual is activated

    next_event_method: string
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
Functions that depend on t such that `block_prob_mod_func(t)` returns an `inter_group_probs` matrix.

## Usage:

The simulation is run by calling `SynthTempNetwork.run()`. All the events are stored in 4 lists: `SynthTempNetwork.indiv_sources`, `SynthTempNetwork.indiv_targets`, `SynthTempNetwork.start_times` and `SynthTempNetwork.end_times`.
