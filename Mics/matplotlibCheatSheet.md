
### Basic plot with 2 lines

```python
import numpy as np
import matplotlib.pyplot as plt 


# setup figure
fig,ax = plt.subplots()

# `x`, `u1` and `u2` are 1D arrays

# plot lines
linu1,= ax.plot(x,u1,label='u$_1$', linewidth=2)
linu2,= ax.plot(x,u2,label='u$_2$', linewidth=2)
ax.legend( fontsize=13)

# set axes limites
ax.set_xlim([0,6])
ax.set_ylim([-.5,18])

# set axes labels
ax.set_xlabel('y (\AA)$ ', fontsize=21)
ax.set_ylabel('x', fontsize=21)


ax.tick_params(axis='both', which='major', labelsize=13)
ax.tick_params(axis='both', which='minor', labelsize=8)


plt.show()
```



### Figure configuration
```python
# set figure size and DPI
fig,ax = plt.subplots(figsize=(12,6),dpi=100)

# Plot two plot side by side
fig, axes = plt.subplots(nrows=1, ncols=2)
#^ `axes` now a list of two axis objects, each can be used like before to plot 

# save figure
fig.savefig("filename.png", dpi=200)
```


### Further configuration:
```python

ax.plot(x, x**2, 'b-') # blue line
ax.plot(x, x**2, 'b.-') # blue line with dots
ax.plot(x, x**3, 'g--') # green dashed line
ax.plot(x, x**3, 'g--',alpha=0.5) # half transperant

ax.plot(x, x**2, color="blue", linestyle='-', marker='.') # same as above second
ax.plot(x, x**2, color="blue", linestyle='-', marker='.' , linewidth=2) # thicker line

# possible linestype options ‘-‘, ‘–’, ‘-.’, ‘:’, ‘steps’
# possible marker symbols: marker = '+', 'o', '*', 's', ',', '.', '1', '2', '3', '4', ...

# `linewidth` or `lw` and `linestyle` or `ls` are same keyword

# all common options
ax.plot(x, x+16, 
    color="purple", 
    lw=1, 
    ls='-', 
    marker='s', 
    markersize=8,
    markerfacecolor="yellow", 
    markeredgewidth=3, 
    markeredgecolor="green")
```