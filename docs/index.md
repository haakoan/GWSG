---
layout: full
homepage: true
disable_anchors: true
description: Documentation for the GW-signal generator SynthGrav

---

<div class="row">
<div class="col-lg-6" markdown="1">

## Installation
{:.mt-lg-0}

### git
   ```bash
  git clone https://github.com/haakoan/SynthGrav
  ```

  ```python
  import synthgrav
  ```

### pip
  ```bash
  #To come 
  ```

## Basic usage

```python
import synthgrav

#Set up signal
s = synthgrav.Signal(time=t,modes=modes,
                polarisation=polarisation) 

#t, modes, and polarisation are user inputs

s.generate_signal() #Generate the signal
#In this example, the signal s will contain the 
#time and the two modes, hp and hc, in
#s.time,s.signal[0],s.signal[1]

#Plot one signal component 
#(assuming pylab is imported as plt)
plt.plot(s.time,s.signal[0]) 
```

## Tutorial
The notebook Getting_started.ipynb provides a SynthGrav tutorial.
</div>
<div class="col-lg-6" markdown="1">

## Documentation
{:.mt-lg-0}
### Signal Class
This section documents the Signal class, through which users can generate a gravitational wave signal from a set of modes.
[Main Signal Class]({{ site.baseurl }}{% link signal.md %})

### Mode Generation
[Mode Generation]({{ site.baseurl }}{% link generate_mode.md %}) provides details on the underlying machinery that generates individual modes to form the signal.

### Built-in Modes
SynthGrav includes built-in modes for supernovae. 
Find details in [Built-in Modes]({{ site.baseurl }}{% link modes.md %}).

## Contact
Haakon Andresen: haakon.andresen (at) astro.su.se \
Bella Finkel: blfinkel (at) wisc.edu

</div>
</div>
