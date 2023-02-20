## GnuPlot Cheatsheet
_Provided gnuplot version above 4.6_


- [Table of Contents](#gnuplot-cheatsheet)
  - [Basic Plot](#basic-plot)
  - [Configuring plot styles](#configuring-plot-styles)
  - [Multiple Data sets and data blocks](#multiple-data-sets-and-data-blocks)
  - [Loops](#loops)
  - [system call](#system-call)
  - [Curve Fitting](#curve-fitting)
  - [Multiplot](#multiplot)
  - [Script for saving figure as eps/pdf](#script-for-saving-figure-as-epspdf)
  - [Markups \& Symbols](#markups--symbols)
  - [Data processing:](#data-processing)
  - [Miscellaneous](#miscellaneous)
    - [Remove margins from gnuplot saved eps](#remove-margins-from-gnuplot-saved-eps)
    - [Positioning things](#positioning-things)
    - [Inline Data](#inline-data)
    - [Pseudo columns](#pseudo-columns)
  - [Reference](#reference)

---

### Basic Plot

1. Check available gnuplot plot styles
    ```bash 
    test   
    ```

2. Plot 'data.dat' file with column 1 and 2 as x and y axis, with lines+points
    ```bash
    plot 'data.dat' using 1:2 with linespoints 
    p 'data.dat' u 1:2 w lp  #shorten version
    p 'data.dat' u 1:2 w l   # plot only with line
    p 'data.dat' u 1:2 w p   # plot only with points
    ```

3. Plot 2D data file 'data.dat' with column 1,2, and 3 as x,y,z axis. 2D data means the data is in blocks of the x axis
    ```bash
    splot 'data.dat' u 1:2:3 w lp  
    sp 'data.dat' u 1:2:3 w lp   #shorten version
    ```

4. Plot multiple lines
    ```bash
    p 'data.dat' u 1:2 w lp, 'data.dat' u 1:3 w lp
    p 'data.dat' u 1:2 w lp, '' u 1:3 w lp # can skip the 2nd file name if its the same as the first one
    ```

5. Multiple y-axis
    ```bash
    plot "data1.dat" u 1:2 w l axes x1y1, "data2.dat" u 1:2 w l axes x1y2 
    # plot "data1.dat" on x axes 1 and y axes 1 i.e. use bottom and left axes for x and y respectively, and use "data.dat" with right axes as y axes. All the ranges, labels etc for the 2nd y axes can be controlled with y2range and y2label
    ```


### Configuring plot styles

5. Set line type, sets the color and styles of lines and points
    ```bash
    p 'data.dat' u 1:2 w lp linetype 1  
    p 'data.dat' u 1:2 w lp lt 1   # shorten version
    ```

6. Sets color, dash, width of lines and type, size of points
    ```bash
    p 'data.dat' u 1:2 w lp linecolor 1 dashtype 1 linewidth 2 pointtype 2 pointsize 3 
    p 'data.dat' u 1:2 w lp lc 1 dt 1 lw 2 pt 2 ps 3   # shorten version
    ```

7. Set legend for the plot
    ```bash
    p 'data.dat' u 1:2 w lp title "my data"
    p 'data.dat' u 1:2 w lp t "my data"     # shorten version
    ```

8. Set axis lables
    ```bash
    set xlabel/ylabel "My Axis" 
    set xlabel/ylabel "My Axis" font "Haveltica,20"  # set font as Haveltica, with size 20
    set xlabel/ylabel "My Axis" font "Haveltica,20" rotate by 90  # rotate the label by 90 degree
    ```

9. Set Ranges
    ```bash
    set xrange/yrange [1:2] # set xrange or yrange from 1-2
    se xr/yr [1:2]          # shorten version
    se xr/yr [:2]           # set only maximum value of xrange or yrange
    pl [1:2][3:4] 'data.dat'# plot 'data.dat' with xrange 1-2 and yrange 3-4
    ```

10. Set ticks
    ```bash
    set xtics 5  # Set x-axis tics with interval of 5
    set xtics 0,.5,10  # Set x-axis tics between 0 to 10, with increment of 0.5
    set xtics ("low" 0, "medium" 50, "high" 100) # set xtics at xaxis position 0,50 and 100, with labels "low", "medium" and "high"
    set xtics ("average" 30 )  # set xtics at 30 with label "average" in addition to already existing tics
    set format x '%.2f'    # set xtics lable format as 2 decimal places
    set mxtics 5 # set minor 5 minor xtics (in between major each xtics)
    # same syntax applies to ytics, ztics, x2tics, y2tics and cbtics
    ```

11. Set texts/labels 
    ```bash
    set label 1 "A" {at <position>} {font "Haveltica,20"} {front|back} 
    # use different tag (i.e. `1` after label) for different label
    # position can be a coordinate for 2 or 3 numbers
    # for easily figuring out the position check below
    ```


12. Set legend
    ```bash
    pl "data.dat" u 1:2 w l title "my data" # plot "data.dat" with "my data" as legend
    pl "data.dat" u 1:2 w l # if `title` missing then the file name with columns will be used as legend
    pl "data.dat" u 1:2 w l notitle # Ignore this plot in legend
    set key    # show legend (default)
    unset key  # hides legend
    set key {left | right | center} {top | bottom | center} # set key at any of there combination only valid for `inside`  mode
    set key {inside | outside} # set legend inside/outside the plot (default: inside)
    set key {above | below} # set key above of below the plot, valid only for `outside` mode.
    set key {Left | Right} # Justify legend text left or right
    set key at 1,1  # set key at 1,1 position ( see below)
    set key box 3   # Put a box around legend with line type 3
    set key reverse # Put legend text after the line symbol
    set key width 5  # set legend column width as 5
    set key invert  # reverse the order of keys
    set key spacing 2 # set spacing between the keys
    ```

---

### Multiple Data sets and data blocks  
In multi data set file the data sets are separated with _two_ blank lines. The data sets can be 1D or 2D data sets. Alternatively, data blocks are separated with just one blank lines. This makes a data set with multiple data blocks a 2D surface data or multiple 1D line data  

**Data Sets** : *Data separated by two blank lines*.  
**Data Blocks**: *Data separated by one blank lines*.  


-  __Plot part of a file__ :  
    __index command__:
    Plot part of a multi data set file using index command.To plot the 3rd index of a multi-dataset file use, (index starts from 0)
    ```
    plot 'file' index 2
    ```

    __every command__: A Very powerful gnuplot command where you can specify different part of a single data sets,


    `every I:J:K:L:M:N`	  
    *    `I`	Line increment  
    *    `J`	Data block increment  
    *    `K`	The first line  
    *    `L`	The first data block  
    *    `M`	The last line  
    *    `N`	The last data block  
    &nbsp;
    <details>	
    <summary> Examples of every command </summary> 

    *   `every 2`	plot every 2 line  
    *   `every ::3`	plot from the 3-rd lines  
    *   `every ::3::5`	plot from the 3-rd to 5-th lines  
    *   `every ::0::0`	plot the first line only  
    *   `every 2::::6`	plot the 1,3,5,7-th lines  
    *   `every :2`	plot every 2 data block  
    *   `every :::5::8`	plot from 5-th to 8-th data blocks  
    *   `every :::5::5` plot 5-th data block
     </details>   



    __with bash command__
    Bash commands can be used inside the gnuplot plot function to modify/filter data directly. e.g. to plot using only first n rows of the data file.
    ```
    pl '< head -n file'
    ```

---

### Loops
* __Inlined__ `for` loop (all plots will be drawn in a single graph/window) (gnuplot 4.4+)
```bash
plot for [i=1:1000] 'data'.i.'.txt' using 1:2 title 'Data='.i
```


* __Explicit__ `do-for` loop (plots will be done one after another) (gnuplot 4.6+)
```bash
do for [i=0:4] {
    plot 'data'.i.'.txt' using 1:2 title 'Data='.i
    pause -1
}
```
`pause -1` means to wait for the enter key. Use `pause n` to wait for n sec.

* looping over a string of words
```bash
ll='0 1 2 3 4'
do for [i in ll] {
    plot 'data'.i.'.txt' using 1:2 title 'Data='.i
    pause -1
}
```

---

### system call  
Use `system` command to call any terminal/system commands, e.g. to list all `.txt` file in directory
```bash
system('ls *.txt')
```
This is useful when working with loop to loop through/plot all related files in a directory. For example, the following command plots all the `*.dat` files in the current directory
```bash
plot for [i in system("ls *.dat")] i u 1:2 w l title i
```

---


### Curve Fitting

```bash
f(x) = a*exp(-b*x**2)   # define the curve you want to fit
a=1;b=1                 # set initial values of the parameter
fit f(x) 'data.dat' u 1:2 via a,b  # fit 1,2 column, as x and f(x), of the file `data.dat` by varying the parameter `a`, `b`
pl 'data.dat' u 1:2 w l, f(x)      # plot the fitted function for comparison, note `a`, `b` will be used as fitted parameter set
```

---



### Multiplot
In multiplot mode several plots can be placed in one page/window. This is very use ful in showing multiplot plots in gridded view in a single page or showing plots in inset.
```bash

set multiplot layout 3,2  #  to plot 6 graph in 3 rows and 2 column
#-- 6 Plots commands ---

```
---

### Script for saving figure as eps/pdf  

Save the following script as `test.plt` and run `gnuplot test.plt` it will generate a `output.eps` file. You can easily convert the eps file to pdf with `epspdf`.


<details>	
<summary>Sample script</summary>

```bash
set term postscript enhanced color eps
set encoding iso_8859_1

set size 1.0,1.0
set view 55,60 # orientation, only for 3d
# set hidden3d

set xtic ("0"0,"{/Symbol p}/6"0.52,"{/Symbol p}/3"1.05,"{/Symbol p}/2"1.57) offset 0,-0.3 font ",20"
set ytic ("0"0.0,"{/Symbol p}/2"1.57 , "{/Symbol p}"3.14, "3{/Symbol p}/2"4.71, "2{/Symbol p}"6.28) offset 0,-0.3 font ",20"
set ztic 3 offset 1,0 font ",20"

set xlabel "{/Symbol q}" offset 1,-1 font ",20"
set ylabel "{/Symbol p}" offset -1,-1 font ",20"
set zlabel "u (eV) "rotate parallel offset 1,0 font ",20"

set key font ",19" spacing 2 at screen 0.9,0.9


set out "output.eps"
sp [][][:20] 'data.dat' u 1:2:3 every 2 w l title "u_1"
```

</details>


---


### Markups & Symbols
Set the terminal type as `set encoding iso_8859_1` to use symbols and markups.  

- Useful Gnuplot Symbols

| Symbol      | GnuPlot symbol |Symbol  |GnuPlot symbol | 
| ----------- | ----------- |---| ---| 
| `Å` (angstrom)     | {\305}      |`°` (degree)   | {\260}       |
| `′` (prime)     | {/Verdana '}      |`≠` (not equal)   | {/Symbol \271}       |
|`α` (alpha)         |  {/Symbol a}    |`β` (beta)          |  {/Symbol b}    |
|`χ` (chi)       |  {/Symbol c}|`δ`/`Δ` (delta)       |  {/Symbol d/D}    |
|`ε` (epsilon)       |  {/Symbol e}   |`φ`/`Φ` (phi)         |  {/Symbol f/j/F}    |
|`γ`/`Γ` (gamma)       |  {/Symbol g}  |`η` (eta)       |  {/Symbol h}|
|`ι` (iota)          |  {/Symbol i}|`κ` (kappa)         |  {/Symbol k}|
|`λ`/`Λ` (lambda)          |  {/Symbol l/L}|`μ` (mu)        |  {/Symbol m}    |
|`ν` (nu)        |  {/Symbol n}|`π`/`Π` (pi)          |  {/Symbol p/P}    |
|`θ`/`Θ` (theta)       |  {/Symbol q/Q}  |`ρ` (rho)       |  {/Symbol r}|
|`σ`/`Σ` (sigma)       |  {/Symbol s/S}    |`τ` (tau)       |  {/Symbol t}    |
|`υ` (upsilon)       |  {/Symbol u}|`ω`/`Ω` (omega)       |  {/Symbol w/W}|
|`ξ`/`Ξ` (xi)          |  {/Symbol x/X}|`ψ`/`Ψ` (psi)         |  {/Symbol y}|
|`ζ` (zeta)          |  {/Symbol z}|

- Useful Gnuplot Markups  

| Markup      | GnuPlot command | Description|
| ----------- | ----------- |-------|
|    $a^x$    | a^x  |Superscript |
|    $a_x$    | a_x  | Subscript|
|    _abc_    | {/Times:Italic abc}  |Italic |
|     __abc__    | {/Times:Bold=20 abc}  |Bold |
|    $a^b_c$    | a@^b_c  |Align super and subscript |



* Markups can be turned off (if its already on for the terminal) with `noenhanced` keyword

&nbsp;

### Data processing:
Functions or operators can be used inside the gnuplot to modify data from files. Data from a particular column can be referneced with the `$` macro.

```bash
pl 'data.dat' u 1:(3*$2) w l # plot column 1 and 2 with column 2 multiplied with 3
pl 'data.dat' u 1:(abs($2)) w l # plot column 1 and 2 with absolute value of column 2

torad(x)=x*3.14159265/180   # a function that converts degree to radian
pl 'data.dat' u (torad($1)):2  # plot column 1 with 2, but convert the degree values to radian

pl 'data.dat' u 1:($2<0?0:$2) w l # `ternary operator`, plot column 2 but put 0 in place of negetive number.
```


---


### Miscellaneous

#### Remove margins from gnuplot saved eps
Configuring margins inside gnuplot is tricky, instead use `eps2eps` removes margins from eps files saved from gnuplot. Save the figure in eps using gnuplot, use `eps2eps` to convert to a temporary `eps` and then convert the eps to pdf to generate a pdf with no unnecessary margins. Here's a simple bash function to do that easily. Just run this `topdf test.eps`.

<details>	
<summary>Bash function</summary>

```bash
topdf(){
    for file in $@; do
        echo $file   # should be eps
        tmpFile=tmp_$file   # convert to temporary eps
        eps2eps $file $tmpFile
        epspdf $tmpFile "${file%.*}".pdf
        rm $tmpFile
    done
}
```
</details>


&nbsp;


#### Positioning things
Gnuplot uses a coordinate style positioning to position different thing like `label`, `key` etc. This can get confusing sometimes and the best way is to use `graph` and `screen` positioning.   
The `screen` positioning uses the whole page of the plot to position things where `0,0` is the bottom left corner and `1,1` is the top right corner of the page. e.g.

```bash
set label 1 "Hi there" at screen 0,0  # will put a label at the bottom left corner of the page
```

The `graph` positioning sets the graph within the axes as a box (or rectangle) of unit 1. Here the `0,0` means the bottom left corner of the graph and `1,1` means the top right corner of the graph. A z coordinate can also be given for surface plots.
```bash
set label 1 "Hi there" at screen 0,0,1  
# set the label at the 0,0 (or the minimum) position of the x,y axis and highest position of the z axis
```



&nbsp;

#### Inline Data
Gnuplot can draw from inline data directly specified during plot, without the need of any explicit data file.
```bash
pl '-' u 1:2 w lp
1 2
2 3
4 5
e
```
This will plot the data [(1,2),(2,3),(4,5)] as if it were given in a file. The `-` means inline data and `e` at the end specifies the end of data input.



&nbsp;

#### Pseudo columns
Gnuplot actual column number starts from 1, but there are three pseudo columns (0,-1,-2) that can be used during plot.   
- 0     Contains the record number (starting from zero) in the current data set.
- -1    Contains the line number (starting from zero). Reset by a single blank line.
- -2    Contains the index (starting from zero) of the current data set. Reset by a double blank line.



### Reference
1. Gnuplot website : http://www.gnuplot.info/
