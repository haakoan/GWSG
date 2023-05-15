---
layout: page
title:  Predefined modes
description: Here we document the signal modes
---
# Modes Sub-Library

The `modes` sub-library provides a collection of predefined modes and user-defined functions for generating gravitational wave signals. 
These modes can be used to construct custom gravitational wave signals using the `Signal` class.

## Predefined Modes

The predefined modes available in the `modes` sub-library are:

- `fmode`
- `p1mode`
- `p2mode`
- `p3mode`
- `g1mode`
- `g2mode`
- `g3mode`
- `gmode_default_func`

gmode_default_func is a test function and the other modes are based on 
Universal relations for gravitational-wave asteroseismology of proto-neutron stars, Alejandro Torres-Forné .et. al.
https://arxiv.org/abs/1902.10048

Each predefined mode is implemented as a function that generates a gravitational wave signal based on the given time array and mode-specific parameters.

## User-Defined Modes

To use a custom mode function with the Signal class, you can pass it as a dictionary value to the modes parameter when initializing the Signal instance:
Users can create their own custom mode functions to generate gravitational wave signals. A user-defined mode function must have the following signature:

```python
def custom_mode_function(mode_kwargs):
    '''
    Arguments:
      mode_kwargs: dict. A dictionary containing any additional mode-specific parameters required by the custom mode function.
    Returns:
      central_frequency: numpy.array. An array with the same length as Signal.time describing the time evolution of the mode's central
      frequency
      '''
    return central_frequency
 ```
 #### Example
```python
import numpy as np
def custom_mode_function(**kwargs):
    t = kwargs['time']
    a = kwargs['a']
    b = kwargs['b']
    return a*t+b
  
my_modes = {'custom_mode': custom_mode_function}
my_mode_kwargs = {'time' : np.linspace(0,1,100), 'a' : 150, 'b' : 130 }
signal = Signal(time, my_modes, mode_kwargs=my_mode_kwargs)
``` 

