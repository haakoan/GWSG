---
layout: full
homepage: true
disable_anchors: true
description: Documentation for the GW-signal generator
---

A basic example can be found in the notebook example.ipyb

<div class="row">
<div class="col-lg-6" markdown="1">

## Installation
{:.mt-lg-0}

### git
   ```bash
  git clone https://github.com/haakoan/NAME
  ```

  ```python
  import NAME
  ```

### pip
  ```bash
  #To come 
  ```

### Basic usage

```python
import NAME

#Set up signal
s = NAME.Signal(time=t,modes=modes,
                polarisation=polarisation) 

#t, modes, and polarisation are user inputs

s.generate_signal() #Generate the signal
# The signal s will now contain the 
#time and the two modes, hp and hc, in
#s.time,s.signal[0],s.signal[1]

#Plot one part of the signal 
#(assuming pylab is imported as plt)
plt.plot(s.time,s.signal[0]) 
```

A fuller description of how to use NAME can be found in the notebook Getting_started.ipynb.

</div>
