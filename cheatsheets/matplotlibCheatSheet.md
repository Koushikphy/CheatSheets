## Matplotlib Cheatsheet


- [Table of Contents](#matplotlib-cheatsheet)
  - [Basic plot with 2 lines](#basic-plot-with-2-lines)
    - [Plot configuration](#plot-configuration)
  - [Configuring with `rcParams`](#configuring-with-rcparams)
  - [Configuring font properties](#configuring-font-properties)
  - [Annotation](#annotation)
  - [Subplots](#subplots)
  - [Contours](#contours)
    - [Line Contour:](#line-contour)
    - [Filled Contour:](#filled-contour)


### Basic plot with 2 lines

```python
# note there are two types of style for plotting with matplotib
# one is object oriented and other is functional style, 
# the following codes uses object oriented style of ploting with matplotlib
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
ax.set_xlabel('y (\AA)$ ', fontsize=21, labelpad=10)
ax.set_ylabel('x', fontsize=21, labelpad=10)


# set axis tics properties
ax.tick_params(axis='both', which='major', labelsize=13)
ax.tick_params(axis='both', which='minor', labelsize=8)


ax.set_xticks(xTickArr)
ax.set_xticklabels(xLabelsArr)
ax.set_yticks(xTickArr)
ax.set_yticklabels(xLabelsArr)

plt.show()
```

#### Plot configuration
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



### Configuring with `rcParams`

Most of the appearance for matplotlib can be configured through the `rcParams`:

```python
import matplotlib.pyplot as plt
plt.rcParams.update({
    "text.usetex": True,
    # "font.family": "Helvetica",
    'text.latex.preamble':r'\usepackage{sfmath} \boldmath',
    "lines.linewidth":1,
    'ytick.labelsize': 13,
    'xtick.labelsize': 13,
    'ytick.right': True,
    'ytick.direction': 'in',
    'ytick.major.size':5,
    'xtick.major.size':5
})
```
<details>	
<summary>Here is the full list of available rcParams</summary>

```bash
    '_internal.classic_mode': False,
    'agg.path.chunksize': 0,
    'animation.bitrate': -1,
    'animation.codec': 'h264',
    'animation.convert_args': [],
    'animation.convert_path': 'convert',
    'animation.embed_limit': 20.0,
    'animation.ffmpeg_args': [],
    'animation.ffmpeg_path': 'ffmpeg',
    'animation.frame_format': 'png',
    'animation.html': 'none',
    'animation.writer': 'ffmpeg',
    'axes.autolimit_mode': 'data',
    'axes.axisbelow': 'line',
    'axes.edgecolor': 'black',
    'axes.facecolor': 'white',
    'axes.formatter.limits': [-5, 6],
    'axes.formatter.min_exponent': 0,
    'axes.formatter.offset_threshold': 4,
    'axes.formatter.use_locale': False,
    'axes.formatter.use_mathtext': False,
    'axes.formatter.useoffset': True,
    'axes.grid': False,
    'axes.grid.axis': 'both',
    'axes.grid.which': 'major',
    'axes.labelcolor': 'black',
    'axes.labelpad': 4.0,
    'axes.labelsize': 'medium',
    'axes.labelweight': 'normal',
    'axes.linewidth': 0.8,
    'axes.prop_cycle': cycler('color', ['#1f77b4', '#ff7f0e', '#2ca02c', '#d62728', '#9467bd', '#8c564b', '#e377c2', '#7f7f7f', '#bcbd22', '#17becf']),
    'axes.spines.bottom': True,
    'axes.spines.left': True,
    'axes.spines.right': True,
    'axes.spines.top': True,
    'axes.titlecolor': 'auto',
    'axes.titlelocation': 'center',
    'axes.titlepad': 6.0,
    'axes.titlesize': 'large',
    'axes.titleweight': 'normal',
    'axes.titley': None,
    'axes.unicode_minus': True,
    'axes.xmargin': 0.05,
    'axes.ymargin': 0.05,
    'axes.zmargin': 0.05,
    'axes3d.grid': True,
    'backend': 'QtAgg',
    'backend_fallback': True,
    'boxplot.bootstrap': None,
    'boxplot.boxprops.color': 'black',
    'boxplot.boxprops.linestyle': '-',
    'boxplot.boxprops.linewidth': 1.0,
    'boxplot.capprops.color': 'black',
    'boxplot.capprops.linestyle': '-',
    'boxplot.capprops.linewidth': 1.0,
    'boxplot.flierprops.color': 'black',
    'boxplot.flierprops.linestyle': 'none',
    'boxplot.flierprops.linewidth': 1.0,
    'boxplot.flierprops.marker': 'o',
    'boxplot.flierprops.markeredgecolor': 'black',
    'boxplot.flierprops.markeredgewidth': 1.0,
    'boxplot.flierprops.markerfacecolor': 'none',
    'boxplot.flierprops.markersize': 6.0,
    'boxplot.meanline': False,
    'boxplot.meanprops.color': 'C2',
    'boxplot.meanprops.linestyle': '--',
    'boxplot.meanprops.linewidth': 1.0,
    'boxplot.meanprops.marker': '^',
    'boxplot.meanprops.markeredgecolor': 'C2',
    'boxplot.meanprops.markerfacecolor': 'C2',
    'boxplot.meanprops.markersize': 6.0,
    'boxplot.medianprops.color': 'C1',
    'boxplot.medianprops.linestyle': '-',
    'boxplot.medianprops.linewidth': 1.0,
    'boxplot.notch': False,
    'boxplot.patchartist': False,
    'boxplot.showbox': True,
    'boxplot.showcaps': True,
    'boxplot.showfliers': True,
    'boxplot.showmeans': False,
    'boxplot.vertical': True,
    'boxplot.whiskerprops.color': 'black',
    'boxplot.whiskerprops.linestyle': '-',
    'boxplot.whiskerprops.linewidth': 1.0,
    'boxplot.whiskers': 1.5,
    'contour.corner_mask': True,
    'contour.linewidth': None,
    'contour.negative_linestyle': 'dashed',
    'date.autoformatter.day': '%Y-%m-%d',
    'date.autoformatter.hour': '%m-%d %H',
    'date.autoformatter.microsecond': '%M:%S.%f',
    'date.autoformatter.minute': '%d %H:%M',
    'date.autoformatter.month': '%Y-%m',
    'date.autoformatter.second': '%H:%M:%S',
    'date.autoformatter.year': '%Y',
    'date.converter': 'auto',
    'date.epoch': '1970-01-01T00:00:00',
    'date.interval_multiples': True,
    'docstring.hardcopy': False,
    'errorbar.capsize': 0.0,
    'figure.autolayout': False,
    'figure.constrained_layout.h_pad': 0.04167,
    'figure.constrained_layout.hspace': 0.02,
    'figure.constrained_layout.use': False,
    'figure.constrained_layout.w_pad': 0.04167,
    'figure.constrained_layout.wspace': 0.02,
    'figure.dpi': 100.0,
    'figure.edgecolor': 'white',
    'figure.facecolor': 'white',
    'figure.figsize': [6.4, 4.8],
    'figure.frameon': True,
    'figure.max_open_warning': 20,
    'figure.raise_window': True,
    'figure.subplot.bottom': 0.11,
    'figure.subplot.hspace': 0.2,
    'figure.subplot.left': 0.125,
    'figure.subplot.right': 0.9,
    'figure.subplot.top': 0.88,
    'figure.subplot.wspace': 0.2,
    'figure.titlesize': 'large',
    'figure.titleweight': 'normal',
    'font.cursive': ['Apple Chancery',
                    'Textile',
                    'Zapf Chancery',
                    'Sand',
                    'Script MT',
                    'Felipa',
                    'Comic Neue',
                    'Comic Sans MS',
                    'cursive'],
    'font.family': ['sans-serif'],
    'font.fantasy': ['Chicago',
                    'Charcoal',
                    'Impact',
                    'Western',
                    'Humor Sans',
                    'xkcd',
                    'fantasy'],
    'font.monospace': ['DejaVu Sans Mono',
                        'Bitstream Vera Sans Mono',
                        'Computer Modern Typewriter',
                        'Andale Mono',
                        'Nimbus Mono L',
                        'Courier New',
                        'Courier',
                        'Fixed',
                        'Terminal',
                        'monospace'],
    'font.sans-serif': ['DejaVu Sans',
                        'Bitstream Vera Sans',
                        'Computer Modern Sans Serif',
                        'Lucida Grande',
                        'Verdana',
                        'Geneva',
                        'Lucid',
                        'Arial',
                        'Helvetica',
                        'Avant Garde',
                        'sans-serif'],
    'font.serif': ['DejaVu Serif',
                    'Bitstream Vera Serif',
                    'Computer Modern Roman',
                    'New Century Schoolbook',
                    'Century Schoolbook L',
                    'Utopia',
                    'ITC Bookman',
                    'Bookman',
                    'Nimbus Roman No9 L',
                    'Times New Roman',
                    'Times',
                    'Palatino',
                    'Charter',
                    'serif'],
    'font.size': 10.0,
    'font.stretch': 'normal',
    'font.style': 'normal',
    'font.variant': 'normal',
    'font.weight': 'normal',
    'grid.alpha': 1.0,
    'grid.color': '#b0b0b0',
    'grid.linestyle': '-',
    'grid.linewidth': 0.8,
    'hatch.color': 'black',
    'hatch.linewidth': 1.0,
    'hist.bins': 10,
    'image.aspect': 'equal',
    'image.cmap': 'viridis',
    'image.composite_image': True,
    'image.interpolation': 'antialiased',
    'image.lut': 256,
    'image.origin': 'upper',
    'image.resample': True,
    'interactive': False,
    'keymap.back': ['left', 'c', 'backspace', 'MouseButton.BACK'],
    'keymap.copy': ['ctrl+c', 'cmd+c'],
    'keymap.forward': ['right', 'v', 'MouseButton.FORWARD'],
    'keymap.fullscreen': ['f', 'ctrl+f'],
    'keymap.grid': ['g'],
    'keymap.grid_minor': ['G'],
    'keymap.help': ['f1'],
    'keymap.home': ['h', 'r', 'home'],
    'keymap.pan': ['p'],
    'keymap.quit': ['ctrl+w', 'cmd+w', 'q'],
    'keymap.quit_all': [],
    'keymap.save': ['s', 'ctrl+s'],
    'keymap.xscale': ['k', 'L'],
    'keymap.yscale': ['l'],
    'keymap.zoom': ['o'],
    'legend.borderaxespad': 0.5,
    'legend.borderpad': 0.4,
    'legend.columnspacing': 2.0,
    'legend.edgecolor': '0.8',
    'legend.facecolor': 'inherit',
    'legend.fancybox': True,
    'legend.fontsize': 'medium',
    'legend.framealpha': 0.8,
    'legend.frameon': True,
    'legend.handleheight': 0.7,
    'legend.handlelength': 2.0,
    'legend.handletextpad': 0.8,
    'legend.labelcolor': 'None',
    'legend.labelspacing': 0.5,
    'legend.loc': 'best',
    'legend.markerscale': 1.0,
    'legend.numpoints': 1,
    'legend.scatterpoints': 1,
    'legend.shadow': False,
    'legend.title_fontsize': None,
    'lines.antialiased': True,
    'lines.color': 'C0',
    'lines.dash_capstyle': <CapStyle.butt: 'butt'>,
    'lines.dash_joinstyle': <JoinStyle.round: 'round'>,
    'lines.dashdot_pattern': [6.4, 1.6, 1.0, 1.6],
    'lines.dashed_pattern': [3.7, 1.6],
    'lines.dotted_pattern': [1.0, 1.65],
    'lines.linestyle': '-',
    'lines.linewidth': 1.5,
    'lines.marker': 'None',
    'lines.markeredgecolor': 'auto',
    'lines.markeredgewidth': 1.0,
    'lines.markerfacecolor': 'auto',
    'lines.markersize': 6.0,
    'lines.scale_dashes': True,
    'lines.solid_capstyle': <CapStyle.projecting: 'projecting'>,
    'lines.solid_joinstyle': <JoinStyle.round: 'round'>,
    'markers.fillstyle': 'full',
    'mathtext.bf': 'sans:bold',
    'mathtext.cal': 'cursive',
    'mathtext.default': 'it',
    'mathtext.fallback': 'cm',
    'mathtext.fontset': 'dejavusans',
    'mathtext.it': 'sans:italic',
    'mathtext.rm': 'sans',
    'mathtext.sf': 'sans',
    'mathtext.tt': 'monospace',
    'patch.antialiased': True,
    'patch.edgecolor': 'black',
    'patch.facecolor': 'C0',
    'patch.force_edgecolor': False,
    'patch.linewidth': 1.0,
    'path.effects': [],
    'path.simplify': True,
    'path.simplify_threshold': 0.111111111111,
    'path.sketch': None,
    'path.snap': True,
    'pcolor.shading': 'auto',
    'pcolormesh.snap': True,
    'pdf.compression': 6,
    'pdf.fonttype': 3,
    'pdf.inheritcolor': False,
    'pdf.use14corefonts': False,
    'pgf.preamble': '',
    'pgf.rcfonts': True,
    'pgf.texsystem': 'xelatex',
    'polaraxes.grid': True,
    'ps.distiller.res': 6000,
    'ps.fonttype': 3,
    'ps.papersize': 'letter',
    'ps.useafm': False,
    'ps.usedistiller': None,
    'savefig.bbox': None,
    'savefig.directory': '~',
    'savefig.dpi': 'figure',
    'savefig.edgecolor': 'auto',
    'savefig.facecolor': 'auto',
    'savefig.format': 'png',
    'savefig.orientation': 'portrait',
    'savefig.pad_inches': 0.1,
    'savefig.transparent': False,
    'scatter.edgecolors': 'face',
    'scatter.marker': 'o',
    'svg.fonttype': 'path',
    'svg.hashsalt': None,
    'svg.image_inline': True,
    'text.antialiased': True,
    'text.color': 'black',
    'text.hinting': 'force_autohint',
    'text.hinting_factor': 8,
    'text.kerning_factor': 0,
    'text.latex.preamble': '',
    'text.usetex': False,
    'timezone': 'UTC',
    'tk.window_focus': False,
    'toolbar': 'toolbar2',
    'webagg.address': '127.0.0.1',
    'webagg.open_in_browser': True,
    'webagg.port': 8988,
    'webagg.port_retries': 50,
    'xaxis.labellocation': 'center',
    'xtick.alignment': 'center',
    'xtick.bottom': True,
    'xtick.color': 'black',
    'xtick.direction': 'out',
    'xtick.labelbottom': True,
    'xtick.labelcolor': 'inherit',
    'xtick.labelsize': 'medium',
    'xtick.labeltop': False,
    'xtick.major.bottom': True,
    'xtick.major.pad': 3.5,
    'xtick.major.size': 3.5,
    'xtick.major.top': True,
    'xtick.major.width': 0.8,
    'xtick.minor.bottom': True,
    'xtick.minor.pad': 3.4,
    'xtick.minor.size': 2.0,
    'xtick.minor.top': True,
    'xtick.minor.visible': False,
    'xtick.minor.width': 0.6,
    'xtick.top': False,
    'yaxis.labellocation': 'center',
    'ytick.alignment': 'center_baseline',
    'ytick.color': 'black',
    'ytick.direction': 'out',
    'ytick.labelcolor': 'inherit',
    'ytick.labelleft': True,
    'ytick.labelright': False,
    'ytick.labelsize': 'medium',
    'ytick.left': True,
    'ytick.major.left': True,
    'ytick.major.pad': 3.5,
    'ytick.major.right': True,
    'ytick.major.size': 3.5,
    'ytick.major.width': 0.8,
    'ytick.minor.left': True,
    'ytick.minor.pad': 3.4,
    'ytick.minor.right': True,
    'ytick.minor.size': 2.0,
    'ytick.minor.visible': False,
    'ytick.minor.width': 0.6,
    'ytick.right': False
```

</details>

&nbsp;



### Configuring font properties
```python
# Label font properties

ax.set_xlabel('X', fontdict={'fontsize': 8, 'fontweight': 'medium','fontname':"Serif"})


# Legend font properties
import matplotlib.font_manager as font_manager
font = font_manager.FontProperties(family='Comic Sans MS',
                                   weight='bold',
                                   style='normal', 
                                   size=32)

ax.legend(title="My Title", prop=font, title_fontproperties=font,)
#^ legend text and title are configured seperately
```


### Annotation

```python
ax.annotate('Label', 
    xy=(x, y), 
    xytext=(x, y), 
    rotation=90, 
    fontsize=15, fontweight='bold', fontstyle='italic', family="Times New Roman"
    bbox=dict( boxstyle='round',facecolor='white'), 
    arrowprops=dict(facecolor='black', shrink=0.05, width=1,headwidth=10,arrowstyle="->")),
)
```

### Subplots

```python
import matplotlib.pyplot as plt
import numpy as np 

plt.rcParams.update({
    "text.usetex": True,
    "font.family": "Helvetica",
    'text.latex.preamble':r'\usepackage{sfmath} \boldmath',
    "lines.linewidth":1,
    'ytick.labelsize': 13,
    'xtick.labelsize': 13,
    'ytick.right': True,
    'ytick.direction': 'in',
    'ytick.major.size':5,
    'xtick.major.size':5
})

# Create the figure and axis objects for 6 plots with 3 row and 2 columns
fig, ax = plt.subplots(nrows=2, ncols=2, figsize=(10, 10))

# ticks position and labels
xTicksPosition = [...]
xTicksLabel = [...]
yTicksPosition = [...]
yTicksLabel = [...]

for (i,j),ax_ in np.ndenumerate(ax): # enumerate over the axes
    ax_.set_xlim([0,10])
    ax_.set_ylim([0,10])

    ax_.set_xticks(xTicksPosition)
    ax_.set_yticks(yTicksPosition)

    if i==1:#last row the xtikcs and xlable
        ax_.set_xticklabels(xTicksLabel)
        ax_.set_xlabel('y',fontsize=21)
    else:
        ax_.set_xticklabels(['' for _ in xTicksLabel])

    if j==0: # first column set y ticks
        ax_.set_yticklabels(yTicksLabel)
    else:
        ax_.set_yticklabels(["" for _ in yTicksLabel])


# a utility function that takes the axis and does the plot
def plotLine(axis,data,*args):
    x,y1,y2,y3,y4 = data # create or load the data for this axis
    # also annote the index if required
    axis.annotate(annot,xy=(1,9),fontsize=15, family="Times New Roman")
    return axis.plot(x,y1,x,y2,x,y3,x,y4) # returns the lines objects, here two lines


# plot the lines
plotLine(ax[0,0],data1,"(a)")
plotLine(ax[0,1],data2,"(b)")
plotLine(ax[1,0],data3,"(c)")
lines = plotLine(ax[1,1],data4,"(d)")  # capture any line object to draw the legend


fig.legend(
    handles=lines,   # using the line objects to get the plot properties
    labels=['$u_1$','$u_2$','$u_3$','$u_4$','$u_5$','$u_6$'],  # lables can also be given in the plot command itself
    ncol=6,  # 6 legends for 6 plots in a single line 
    fontsize=15,
    loc="lower center",
    shadow=True
)

# global y axis for all the plot
fig.text(0.04, 0.5, 'Adiabatic PES (eV)', va='center', rotation='vertical',fontsize=15)

fig.tight_layout()
plt.subplots_adjust(left=0.1,bottom=0.1,top=0.95, right= 0.95)
plt.savefig("plot.eps")
plt.show()
```



### Contours
#### Line Contour:
```python
fig, ax0 = plt.subplots(1)
levels = np.unique(np.percentile(z,np.linspace(0,100,20)))
# levels is any monotonically increasing array to specify the contour level, 
# the percentile is a quick way to calculate some proper levels for the data
# otherwise use a userdefined array for the contour labels

cp = ax0.contour(x, y, z, levels = levels, linewidths=1.3,colors='black')#, linestyles='solid')
# x,y,z are all 2D arrays for surface plot data
ax0.clabel(cp, inline=True,manual=True,inline_spacing=1,fontsize=13,fmt='%.3f',colors='black')
# manual True means you have to manually specify the contour label position by clicking on it
# `fmt` can be a function that returns the label string by taking the label value as input 

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



