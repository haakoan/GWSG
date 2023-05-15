---
layout: page
title:  generate_mode
description: Documentation for the main signal generation aspect of the code
---
## `generate_mode`

This function generates a single mode of a gravitational wave signal. It takes a user-defined function or a predefined function from the modes sub-library, computes the mode, and returns it.

### `generate_mode_v1(func, time, dt, rng_seed, mode_kwargs={}, polarisation=False, polarisation_value=None)`

This version generates the gravitational wave mode using a single user-defined or predefined function. 

- Arguments:
  - `func`: function. The function to compute the mode.
  - `time`: numpy.array. Array with the time coordinates at which to sample the mode.
  - `dt`: float. Time step size.
  - `rng_seed`: int. Seed used in random number generation.
  - `mode_kwargs`: dict. A dict containing keyword arguments that are to be passed to the mode function.
  - `polarisation`: bool. Whether or not to include polarisation effects.
  - `polarisation_value`: float or numpy.array. Polarisation value(s) to use if `polarisation` is set to True.
- Returns: numpy.array. The computed mode.

### `generate_mode_v2(func, time, dt, rng_seed, mode_kwargs={}, polarisation=False, polarisation_value=None)`

This version generates the gravitational wave mode using a single user-defined or predefined function and adds the effect of polarisation using the polarisation value(s).

- Arguments:
  - `func`: function. The function to compute the mode.
  - `time`: numpy.array. Array with the time coordinates at which to sample the mode.
  - `dt`: float. Time step size.
  - `rng_seed`: int. Seed used in random number generation.
  - `mode_kwargs`: dict. A dict containing keyword arguments that are to be passed to the mode function.
  - `polarisation`: bool. Whether or not to include polarisation effects.
  - `polarisation_value`: float or numpy.array. Polarisation value(s) to use if `polarisation` is set to True.
- Returns: numpy.array. The computed mode.

## `add_noise`

This function adds random noise to the gravitational wave signal. It generates random noise using a specified random number generator and scales the noise by a given noise level.

### `add_noise(n, rng, noise_level=1.0)`

Generates random noise and scales it by the provided noise level.

- Arguments:
  - `n`: int. The number of time steps for which to generate noise.
  - `rng`: numpy.random.default_rng. An instance of the NumPy random number generator.
  - `noise_level`: float. The scaling factor for the generated noise. A higher value results in a higher level of noise. Default value is 1.0.
- Returns: numpy.array. The generated noise array.

---

