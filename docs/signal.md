---
layout: page
title:  Signal Class
description: Here we document the main signal class
---

# Signal Class

The Signal class represents a gravitational wave signal generated from a set of modes. For each mode and at each time step, the signal is created by randomly sampling from a window centered on the mode frequency at that time. Randomly sampled noise is then added to the signal. The relative strength of each mode can be adjusted by user-specified mode weights.

## Attributes

- `time`: numpy.array
  - An array containing the time coordinates. Assumed to be equidistant.

- `signal`: numpy.array
  - The gravitational wave signal sampled at the times in the `time` array.

- `modes`: dict
  - A dictionary listing the modes of the signal.

- `mode_weight`: dict
  - A dictionary containing weights corresponding to any one mode. The keys of `mode_weight` should correspond to the keys in `modes`. If a key in `modes` exists in `mode_weight`, then the mode's contribution to the total signal is taken to be `contribution_of_mode * mode_weight[mode]`.

- `signal_weight`: numpy.array
  - Time-dependent weights applied to the signal so that the total signal is given by `signal(t) * signal_weight`

- `rng_seed`: int
  - Seed used for the random number generator.

- `rng`: numpy.random.default_rng
  - An instance of the numpy random number generator, using the `rng_seed`.

- `dt`: float
  - Spacing between time steps.


## Methods

### `generate_signal()`

This function generates the gravitational wave signal based on the input provided by the user when the Signal was initiated. The user does not need to provide any input since this has already been provided when initializing the Signal instance.

- Arguments: None
- Returns: None

### `__init__(self, time, modes, mode_kwargs={}, mode_weight = {}, polarisation=False, signal_weight = None, rng_seed = -1, noise_level=1.0)`

This method sets up the Signal instance based on the input provided by the user. The user can specify the desired modes either as a string (for a single mode), as a tuple of strings, or as a dictionary of user-defined modes. 

- Arguments:
  - `time`: numpy.array. Array with the time coordinates at which to sample the signal.
  - `modes`: str, tuple(str), dict. Modes to be included in the signal.
  - `mode_kwargs`: dict. A dict containing keyword arguments that are to be passed to the mode functions.
  - `mode_weight`: dict. A dict containing weights to adjust each individual mode's contribution to the total signal.
  - `signal_weight`: numpy.array. Array to weight the total signal, time dependent.
  - `rng_seed`: int. Seed used in random number generation.
  - `noise_level`: float. Level of noise to be added to the signal.
- Returns: None

---
