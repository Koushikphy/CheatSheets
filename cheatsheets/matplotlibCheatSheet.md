
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

# set axes labels, labelpad is offset of the label from the axis
ax.set_xlabel('y (\AA)$ ', fontsize=21, labelsize=10)
ax.set_ylabel('x', fontsize=21, labelsize=10)


# set axis tics properties
ax.tick_params(axis='both', which='major', labelsize=13)
ax.tick_params(axis='both', which='minor', labelsize=8)


ax.set_xticks(xTickArr)
ax.set_xticklabels(xLabelsArr)
ax.set_yticks(xTickArr)
ax.set_yticklabels(xLabelsArr)

plt.show()
```



### Figure configuration
```python
# set figure size and DPI
fig,ax = plt.subplots(figsize=(12,6),dpi=100)

# Plot two plot side by side
fig, axes = plt.subplots(nrows=1, ncols=2)
#^ `axes` now a list of two axis objects, each can be used like before to plot 

# remove unwanted margins, after plotting everything
fig.tight_layout()


# save figure
fig.savefig("filename.png", dpi=200)
```


### Further configuration:
```python

ax.plot(x, x**2, 'b-') # blue line
ax.plot(x, x**2, 'b.-') # blue line with dots
ax.plot(x, x**3, 'g--') # green dashed line
ax.plot(x, x**3, 'g--',alpha=0.5) # half transparent

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


### Contours
#### Line Contour:
```python
fig, ax0 = plt.subplots(1)
levels = np.unique(np.percentile(z,np.linspace(0,100,20)))
# levels is any monotonically increasing array to specify the contour level, 
# the percentile is a quick way to calculate some proper levels for the data
cp = ax0.contour(x, y, z, levels = levels, linewidths=1.3,colors='black')#, linestyles='solid')
# x,y,z are all 2D arrays for surface plot data
ax0.clabel(cp, inline=True,manual=True,inline_spacing=1,fontsize=13,fmt='%.3f')
# manual True means you have to manually specify the contour label position by clicking on it

# if you want to use legend with the contour plot, useful for multiple surface contour 
lines = [ cp.collections[0]]
labels = ['sample data']
plt.legend(lines, labels, fontsize=15 )
```

#### Filled Contour:
<!--  -->
```python
cp = ax0.contourf(x, y, z,levels = levels, cmap='RdYlGn_r', norm=matplotlib.colors.BoundaryNorm(levels,256))
# x,y,z are 2D array for surface data
# levels is a monotonically increasing array
# choose any of the available `cmap`s
# Chose a `norm` type for proper color normalization appropriate for the current data https://matplotlib.org/stable/tutorials/colors/colormapnorms.html

# put a color bar for the filled contour
cbar = plt.colorbar(cp,ticks=levels, orientation='verticle')
cbar.ax.set_yticklabels([ '{:.2f}'.format(i) for i in levels]) 
# use xtickslables for horaizontal colorbar
cbar.ax.tick_params(labelsize=15)
cbar.ax.get_yaxis().labelpad = 30
cbar.ax.set_ylabel('Energy (eV)', rotation=270,fontsize=25)
```



### Annotation/Text:

#### Text with arrow

```python
ax.annotate('Label', 
    xy=(x, y), 
    xytext=(x, y), 
    rotation=90, 
    fontsize=15, fontweight='bold', fontstyle='italic', family="Times New Roman"
    bbox=dict( boxstyle='round',facecolor='white'), 
    arrowprops=dict(facecolor='black', shrink=0.05, width=1,headwidth=10),
)
```

#### Matplotlib arrow
```python
# Arrow goes from (x,y) to (x+dx,y+dy)
plt.arrow(x,y,dx,dy,head_width=.8, head_length=2, length_includes_head=True,color='black')
```