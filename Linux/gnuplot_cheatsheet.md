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