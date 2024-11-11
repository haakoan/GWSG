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
#The signal s will now contain the 
#time and the two modes, hp and hc, in
#s.time,s.signal[0],s.signal[1]

#Plot one part of the signal 
#(assuming pylab is imported as plt)
plt.plot(s.time,s.signal[0]) 
```

## Tutorial
A description of how to use SynthGrav can be found in the tutorial the notebook
named Getting_started.ipynb, in the main repository <url>https://github.com/haakoan/SynthGrav</url>.
</div>
<div class="col-lg-6" markdown="1">

## Documentation
{:.mt-lg-0}
### Signal Class
This section documents the main Signal class, which is the primary object that end-users will interact with.
[Main Signal Class]({{ site.baseurl }}{% link signal.md %})

### Mode Generation
[Mode Generation]({{ site.baseurl }}{% link generate_mode.md %}) provides details on the underlying machinery that generates individual modes, and essentially forms the signal.

### Built-in Modes
Find details about the supernova-specific modes used to generate the signal in [Built-in Modes]({{ site.baseurl }}{% link modes.md %}).

</div>
</div>