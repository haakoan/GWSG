---
layout: page
title:  Mode generation
description: Documentation for the main signal generation function generate_mode
---
# Signal Generation
The function `generate_mode` generates a gravitational wave mode based on the user-specified parameters. 
It first generates random white noise in the frequency 
domain and calculates the power spectral density `s1` using the provided `psd` function and input parameters. 
It then shapes the noise by the power spectral density and generates a pulse based on the specified polarization.

The function is implemented as follows:

1. Generate random white noise `h1_white` in the frequency domain and calculate the frequency array `f`:
   
   `h1_white = FFT(rng_generator.standard_normal(N))`

   `f = fftfreq(N, d=dt)[:N]`
   
2. Calculate the power spectral density `s1` using the provided `psd` function and input parameters:

   `s1 = psd(f, central_frequency, **psd_kwargs)`

4. Normalize the power spectral density `s1`:

   `s1 = s1 / sqrt(mean(s1^2))`

6. Shape the noise by the power spectral density:

   `h1_shaped = h1_white * s1`

8. Generate a pulse based on the specified polarization:
   - If the polarization is 'unpolarised', generate another set of random white noise `h2_white`, shape it by the power spectral density `s1`, and perform an inverse Fourier transform on both `h1_shaped` and `h2_shaped` to obtain the time-domain waveforms `h_t1` and `h_t2`.
   - If the polarization is 'linear', generate a time-domain waveform `h_t1` using the inverse Fourier transform of `h1_shaped`, and set `h_t2` to be an array of zeros with the same length as `h_t1`.
   - If the polarization is 'elliptical', then `h2_white` is related to `h1_white` in the frequency domain as `h2_white = 1.0j*h1_white*polarisation_value`.

The output of the function is a tuple containing the time-domain waveforms `h_t1` and `h_t2`. The signal ends up in `Signal.signal[0]` and `Signal.signal[1]`, from which the user
can access them.


## `generate_mode(mode, *args, **kwargs)`

This is a template function for generating gravitational wave modes. It is overloaded to support both callables and sequences as input for the `mode`.

### `generate_mode(mode, time, dt, rng_generator, pulse_duration=0.05, polarisation='unpolarised', polarisation_value=0.0, mode_kwargs={}, psd=gauss_psd, psd_kwargs={'sigma': 10})`

This version of `generate_mode` accepts a user-defined or predefined function for the mode. It generates the signal component associated with a given mode as a series of pulses of colored noise.

- Arguments:
  - `mode`: function. Function describing the time evolution of the central frequency of the mode.
  - `time`: numpy.array. Array with the time coordinates at which to sample the mode.
  - `dt`: float. Time step size.
  - `rng_generator`: numpy.random.Generator. Random number generator for creating noise samples.
  - `pulse_duration`: float. Length of each of the individual pulses that make up the signal.
  - `polarisation`: str. Pulse polarisation type: 'unpolarised', 'linear', or 'elliptical'.
  - `polarisation_value`: float or numpy.array. Polarisation value(s) to use if `polarisation` is set.
  - `mode_kwargs`: dict. A dict containing keyword arguments that are to be passed to the mode function.
  - `psd`: function. PSD to use for the colored noise.
  - `psd_kwargs`: dict. A dict containing keyword arguments that are to be passed to the PSD function.
- Returns: tuple of numpy.array. The computed cross and plus components of the signal.

### `generate_mode(mode, time, dt, rng_generator, pulse_duration=0.05, polarisation='unpolarised', polarisation_value=0.0, psd=gauss_psd, psd_kwargs={'sigma': 10}, mode_kwargs={})`

This version of `generate_mode` accepts a sequence or ndarray for the mode. It generates the signal component associated with a given mode as a series of pulses of colored noise.

- Arguments:
  - `mode`: ndarray, list. Array describing the time evolution of the central frequency of the mode.
  - `time`: numpy.array. Array with the time coordinates at which to sample the mode.
  - `dt`: float. Time step size.
  - `rng_generator`: numpy.random.Generator. Random number generator for creating noise samples.
  - `pulse_duration`: float. Length of each of the individual pulses that make up the signal.
  - `polarisation`: str. Pulse polarisation type: 'unpolarised', 'linear', or 'elliptical'.
  - `polarisation_value`: float or numpy.array. Polarisation value(s) to use if `polarisation` is set.
  - `psd`: function. PSD to use for the colored noise.
  - `psd_kwargs`: dict. A dict containing keyword arguments that are to be passed to the PSD function.
  - `mode_kwargs`: dict. A dict containing keyword arguments that are to be passed to the mode function (if required).
- Returns: tuple of numpy.array. The computed cross and plus components of the signal.



## `add_noise`

This function adds random noise to the gravitational wave signal. It generates random noise using a specified random number generator and scales the noise by a given noise level.

### `add_noise(n, rng, noise_level=1.0)`

Generates random noise and scales it by the provided noise level.

- Arguments:
  - `n`: int. The number of time steps for which to generate noise.
  - `rng`: numpy.random.default_rng. An instance of the NumPy random number generator.
  - `noise_level`: float. The scaling factor for the generated noise. A higher value results in a higher level of noise. Default value is 1.0.
- Returns: numpy.array. The generated noise array.

## Power spectral density
The following PSDs are defined for colouring the noise that makes up the pulses. 
These are predefined, but the user can specify their own. Using the simple `gauss_psd` is recommended for most use cases.

### `gauss_psd(f, central_frequency, **kwargs)`

This function returns the Gaussian spectral density centered around a `central_frequency` with standard deviation `sigma`.

- Arguments:
  - `f`: numpy.array. The frequency values.
  - `central_frequency`: float. The central frequency.
  - `**kwargs`: dict. A dictionary containing additional keyword arguments, in this case `sigma` for the standard deviation.
- Returns: numpy.array. The Gaussian spectral density.

### `logistic_psd(f, central_frequency, **kwargs)`

This function returns the logistic spectral density centered around a `central_frequency` with scale `s`.

- Arguments:
  - `f`: numpy.array. The frequency values.
  - `central_frequency`: float. The central frequency.
  - `**kwargs`: dict. A dictionary containing additional keyword arguments, in this case `s` for the scale parameter.
- Returns: numpy.array. The logistic spectral density.

### `cauchy_psd(f, central_frequency, **kwargs)`

This function returns the Cauchy spectral density centered around a `central_frequency` with scale `gamma`.

- Arguments:
  - `f`: numpy.array. The frequency values.
  - `central_frequency`: float. The central frequency.
  - `**kwargs`: dict. A dictionary containing additional keyword arguments, in this case `gamma` for the scale parameter.
- Returns: numpy.array. The Cauchy spectral density.

### `constant_psd(f, central_frequency, **kwargs)`

This function returns a constant spectral density within a frequency band centered around a `central_frequency` with a width of `delta_f`.

- Arguments:
  - `f`: numpy.array. The frequency values.
  - `central_frequency`: float. The central frequency.
  - `**kwargs`: dict. A dictionary containing additional keyword arguments, in this case `delta_f` for the width of the frequency band.
- Returns: numpy.array. The constant spectral density within the defined frequency band and zero outside.


