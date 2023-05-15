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
