---
layout: page
title:  generate_mode
description: Documentation for the main signal generation aspect of the code
---

`generate_mode` is a function that generates a gravitational wave mode based on the user-specified parameters. It first generates random white noise in the frequency domain and calculates the power spectral density `s1` using the provided `psd` function and input parameters. It then shapes the noise by the power spectral density and generates a pulse based on the specified polarization.

The math behind the function can be described as follows:

1. Generate random white noise `h1_white` in the frequency domain and calculate the frequency array `f`:
   h1_white = FFT(rng_generator.standard_normal(N))
   f = fftfreq(N, d=dt)[:N]

2. Calculate the power spectral density `s1` using the provided `psd` function and input parameters:
   s1 = psd(f, central_frequency, **psd_kwargs)

3. Normalize the power spectral density `s1`:
   s1 = s1 / sqrt(mean(s1^2))

4. Shape the noise by the power spectral density:
   h1_shaped = h1_white * s1

5. Generate a pulse based on the specified polarization:
   - If the polarization is 'unpolarised', generate another set of random white noise `h2_white`, shape it by the power spectral density `s1`, and perform an inverse Fourier transform on both `h1_shaped` and `h2_shaped` to obtain the time-domain waveforms `h_t1` and `h_t2`.
   - If the polarization is 'linear', generate a time-domain waveform `h_t1` using the inverse Fourier transform of `h1_shaped`, and set `h_t2` to be an array of zeros with the same length as `h_t1`.
   - If the polarization is 'elliptical', generate another set of random white noise `h2_white`, shape it by the power spectral density `s1` and the polarization value `polarisation_value`, and perform an inverse Fourier transform on both `h1_shaped` and `h2_shaped` to obtain the time-domain waveforms `h_t1` and `h_t2`.
   - For any other polarization, return two arrays of zeros with the same length as the input time array.

The output of the function is a tuple containing the time-domain waveforms `h_t1` and `h_t2`, which can be used to create the final gravitational wave signal.





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


### `gauss_psd(f, central_frequency, **kwargs)`

This function returns the Gaussian spectral density centered around a `central_frequency` with standard deviation `sigma`.

- Arguments:
  - `f`: numpy.array. The frequency values.
  - `central_frequency`: float. The central frequency.
  - `**kwargs`: dict. A dictionary containing additional keyword arguments, in this case `sigma` for the standard deviation.
- Returns: numpy.array. The Gaussian spectral density.

### `logistic_psd(f, central_frequency, **kwargs)`

This function returns the Logistic spectral density centered around a `central_frequency` with scale `s`.

- Arguments:
  - `f`: numpy.array. The frequency values.
  - `central_frequency`: float. The central frequency.
  - `**kwargs`: dict. A dictionary containing additional keyword arguments, in this case `s` for the scale parameter.
- Returns: numpy.array. The Logistic spectral density.

### `cauchy_psd(f, central_frequency, **kwargs)`

This function returns the Cauchy spectral density centered around a `central_frequency` with scale `gamma`.

- Arguments:
  - `f`: numpy.array. The frequency values.
  - `central_frequency`: float. The central frequency.
  - `**kwargs`: dict. A dictionary containing additional keyword arguments, in this case `gamma` for the scale parameter.
- Returns: numpy.array. The Cauchy spectral density.

### `constant_psd(f, central_frequency, **kwargs)`

This function returns a constant spectral density within a frequency band centered around a `central_frequency` and with a width of `delta_f`.

- Arguments:
  - `f`: numpy.array. The frequency values.
  - `central_frequency`: float. The central frequency.
  - `**kwargs`: dict. A dictionary containing additional keyword arguments, in this case `delta_f` for the width of the frequency band.
- Returns: numpy.array. The constant spectral density within the defined frequency band and zero outside.
---

