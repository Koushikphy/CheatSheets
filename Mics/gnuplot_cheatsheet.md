## GnuPlot Cheatsheet
_Provided gnuplot version above 4.6_



1. Check available gnuplot plot styles
    ```bash 
    test   
    ```

1. plot 'data.dat' file with column 1 and 2 as x and y axis, with lines+points
    ```bash
    plot 'data.dat' using 1:2 with linespoints 
    p 'data.dat' u 1:2 w lp   #shorten version
    ```

1. plot 2D data file 'data.dat' with column 1,2, and 3 as x,y,z axis. 2D data means the data is in blocks of the x axis
    ```bash
    splot 'data.dat' u 1:2:3 w lp  
    sp 'data.dat' u 1:2:3 w lp   #shorten version
    ```


1. Plot multiple lines
    ```bash
    p 'data.dat' u 1:2 w lp, 'data.dat' u 1:3 w lp
    p 'data.dat' u 1:2 w lp, '' u 1:3 w lp # can skip the 2nd file name if its the same as the first one
    ```


1. set line type, sets the color and styles of lines and points
    ```bash
    p 'data.dat' u 1:2 w lp linetype 1  
    p 'data.dat' u 1:2 w lp lt 1   # shorten version
    ```

1. sets color, dash, width of lines and type, size of points
    ```bash
    p 'data.dat' u 1:2 w lp linecolor 1 dashtype 1 linewidth 2 pointtype 2 pointsize 3 
    p 'data.dat' u 1:2 w lp lc 1 dt 1 lw 2 pt 2 ps 3   # shorten version
    ```

1. set legend for the plot
    ```bash
    p 'data.dat' u 1:2 w lp title "my data"
    p 'data.dat' u 1:2 w lp t "my data"     # shorten version
    ```

1. Set axis lables
    ```bash
    set xlabel/ylabel "My Axis" 
    set xlabel/ylabel "My Axis" font "Haveltica,20"  # set font as Haveltica, with size 20
    set xlabel/ylabel "My Axis" font "Haveltica,20" rotate by 90  # rotate the lable by 90 degree
    ```

1. Set Ranges
    ```bash
    set xrange/yrange [1:2] # set xrange or yrange from 1-2
    se xr/yr [1:2]          # shorten version
    se xr/yr [:2]           # set only maximum value of xrange or yrange
    pl [1:2][3:4] 'data.dat'# plot 'data.dat' with xrange 1-2 and yrange 3-4
    ```

1. Set ticks
    ```bash
    set xtics 5  # Set x-axis tics with interval of 5
    set xtics 0,.5,10  # Set x-axis tics between 0 to 10, with increment of 0.5
    set xtics ("low" 0, "medium" 50, "high" 100) # set xtics at xaxis position 0,50 and 100, with labels "low", "medium" and "high"
    set xtics ("average" 30 )  # set xtics at 30 with label "average" in addition to already existing tics
    set format x '%.2f'    # set xtics lable format as 2 decimal places
    set mxtics 5 # set minor 5 minor xtics (in between major each xtics)
    # same syntax applies to ytics, ztics, x2tics, y2tics and cbtics
    ```

1. Set texts/labels 
    ```bash
    set label 1 "A" at 1,1 "Haveltica,20" {pt <pointstyle>} {front|back}
    # use different tag (i.e. `1` after label) for different label
    # for 3D use 3 postion coordinates
    ```


1. Set legend
    ```bash
    pl "data.dat" u 1:2 w l title "my data" # plot "data.dat" with "my data" as legend
    set key    # show legned (defult)
    unset key  # hides legend
    set key inside  # set legend inside the plot (default)
    set key outside # set key outside the plot
    set key right top  # set key at top right corner (default)
    set key {left | right | center} {top | bottom | center} # set key at any of there combination only valide for `inside`  mode
    set key {above | below} # set key above of below the plot, valid only for `outside` mode.
    set key at 5,5  # set key at coordinate at 5,5
    set key box 3   # Put a box around legend with line type 3
    set key reverse # Put legend text after the line symbol
    set key width 5  # set legend column width as 5
    ```



1. Multiple y-axis
    ```bash
    plot "data1.dat" u 1:2 w l axes x1y1, "data2.dat" u 1:2 w l axes x1y2 
    # plot "data1.dat" on x axes 1 and y axes 1 i.e. use bottom and left axes for x and y respectevely, and use "data.dat" with right axes as y axes. All the ranges, labels etc for the 2nd y axes can be controlled with y2range and y2label
    ```




1. __multiple Data sets and data blocks__:
In multi data set file the data sets are seperated with _two_ blank lines. The data sets can be 1D or 2D data sets. Alternatevely, data blocks are seperated with just one blank lines. This makes a data set with multiple data blocks a 2D surface data or multiple 1D line data  

    **Data Sets** : *Data seperated by two blank lines*.  
    **Data Blocks**: *Data seperated by one blank lines*.  


1. __Plot part of a file__ :  
    __index command__:
    Plot part of a mulit data set file using index command.To plot the 3rd index of a multi-dataset file use, (index starts from 0)
    ```
    plot 'file' index 2
    ```

    __every command__: A Very powerful gnuplot commnad where you can specify differnt part of a single data sets,

    `every I:J:K:L:M:N`	  
    *    `I`	Line increment  
    *    `J`	Data block increment  
    *    `K`	The first line  
    *    `L`	The first data block  
    *    `M`	The last line  
    *    `N`	The last data block  

    __Samples:__  
    *   `every 2`	plot every 2 line  
    *   `every ::3`	plot from the 3-rd lines  
    *   `every ::3::5`	plot from the 3-rd to 5-th lines  
    *   `every ::0::0`	plot the first line only  
    *   `every 2::::6`	plot the 1,3,5,7-th lines  
    *   `every :2`	plot every 2 data block  
    *   `every :::5::8`	plot from 5-th to 8-th data blocks  
    *   `every :::5::5` plot 5-th data block


    __with bash command__
    Bash commands can be used inside the gnuplot plot function to modify/fiter data directly. e.g. to plot using only first n rows of the data file.
    ```
    pl '< head -n file'
    ```


1. loops
    * Inlined `for` loop (gnuplot 4.4+)
    ```bash
    plot for [i=1:1000] 'data'.i.'.txt' using 1:2 title 'Data='.i
    ```


    * Explicit `do-for` loop (gnuplot 4.6+)
    ```bash
    do for [i=0:4] {
        plot 'data'.i.'.txt' using 1:2 title 'Data='.i
    }
    ```

    * looping over a string of words
    ```bash
    ll='0 1 2 3 4'
    do for [i in ll] {
        plot 'data'.i.'.txt' using 1:2 title 'Data='.i
    }
    ```


1. Call system commands:  
    Use `system` command to call any terminal/system commands, e.g. to list all `.txt` file in directory
    ```bash
    system('ls *.txt')
    ```
    This is useful when working with loop to loop through/plot all related files in a directory.



1. Curve Fitting

```bash
f(x) = a*exp(-b*x**2)   # define the curve you want to fit
a=1;b=1                 # set initial values of the parameter
fit f(x) 'data.dat' u 1:2 via a,b  # fit 1,2 column, as x and f(x), of the file `data.dat` by varying the parameter `a`, `b`
pl 'data.dat' u 1:2 w l, f(x)      # plot the fitted function for comparison, note `a`, `b` will be used as fitted paramter set
```


### Reference
1. Gnuplot website : http://www.gnuplot.info/