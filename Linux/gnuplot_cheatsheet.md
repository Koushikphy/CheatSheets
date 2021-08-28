### Common gnuplot commands _Provided gnuplot version above 4.6_
1. Check available gnuplot plot styles
    ```bash 
    test   
    ```

1. plot 'data.dat' file with column 1 and 2 as x and y axis, with lines+points
    ```bash
    plot 'data.dat' using 1:2 with linespoints 
    p 'data.dat' u 1:2 w lp   #shorten version
    ```

1. Plot multiple lines
    ```bash
    p 'data.dat' u 1:2 w lp, 'data.dat' u 1:3 w lp
    p 'data.dat' u 1:2 w lp, '' u 1:3 w lp # can skip the 2nd file name if its the same as the first one
    ```


1. set line type , sets the color and styles of lines and points
    ```bash
    p 'data.dat' u 1:2 w lp linetype 1  
    p 'data.dat' u 1:2 w lp lt 1   # shorten version
    ```

1. sets color, width, dash of lines and size, type of points
    ```bash
    p 'data.dat' u 1:2 w lp linecolor 1 dashtype 1 linewidth 2 pointtype 2 pointsize 3 
    p 'data.dat' u 1:2 w lp lc 1 dt 1 lw 2 pt 2 ps 3   # shorten version
    ```

1. set legend for the plot
    ```bash
    p 'data.dat' u 1:2 w lp title "my data"
    p 'data.dat' u 1:2 w lp t "my data"     # shorten version
    ```

1. Set lables
    ```bash
    set xlabel/ylabel "My Axis" 
    set xlabel/ylabel "My Axis" font "Haveltica,20"  # set font as Haveltica, with size 20
    set xlabel/ylabel "My Axis" font "Haveltica,20" rotate by 90  # rotate the lable by 90 degree
    ```







## GnuPlot Cheatsheet
1. __multiple Data sets and data blocks__:
In multi data set file the data sets are seperated with _two_ blank lines. The data sets can be 1D or 2D data sets. Alternatevely, data blocks are seperated with just one blank lines. This makes a data set with multiple data blocks a 2D surface data or multiple 1D line data



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



1. Check available gnuplot plots/styles  
    Run `test` in gnuplot terminal



