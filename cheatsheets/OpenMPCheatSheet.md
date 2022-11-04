## OpenMP Cheat Sheet for Fortran
---
OpenMP: (i) Thread Level Parallelism; (ii) Shared Memory Parallelism

- [Table of Contents](#-openmp-cheat-sheet-for-fortran)
  - [Compiling OpenMP code](#compiling-openmp-code)
  - [OpenMP directive](#openmp-directive)
  - [OpenMP parallel region](#openmp-parallel-region)
  - [Setting number of threads.](#setting-number-of-threads)
  - [Parallelizing `do` loops](#parallelizing-do-loops)
    - [OpenMP do loop directive.](#openmp-do-loop-directive)
    - [Scoping variable inside an parallel do loop: `private`/`shared` variable.](#scoping-variable-inside-an-parallel-do-loop-privateshared-variable)
    - [Parallelize multiple do loops: `collapse` clause.](#parallelize-multiple-do-loops-collapse-clause)
    - [Perform reduction operation across threads: `reduction` clause.](#perform-reduction-operation-across-threads-reduction-clause)
    - [Behavior of parallelization: `schedule` clause:](#behavior-of-parallelization-schedule-clause)
  - [Conditional parallelization: `if` clause.](#conditional-parallelization-if-clause)
  - [Noniterative workshare: `sections` clause.](#noniterative-workshare-sections-clause)
  - [Nested parallelism](#nested-parallelism)
  - [Mutual exclusion synchronization: `critical` clause.](#mutual-exclusion-synchronization-critical-clause)
  - [Coarse grain vs fine grain parallelisation](#coarse-grain-vs-fine-grain-parallelisation)
    - [Coarse grain parallelisation](#coarse-grain-parallelisation)
    - [Fine grain parallelisation](#fine-grain-parallelisation)




### Compiling OpenMP code
It depends on the compiler, check the compiler manual for details. For `gfortran` and `ifort`, its `-fopenmp` and `-qopenmp` respectively
```bash
# for gfortran
gfortran code.f90 -fopenmp
# for ifort
ifort code.f90 -qopenmp
```
&nbsp;


### OpenMP directive
In free form of Fortran a line that begins with `!$omp` is a OpenMP directive
```fortran
!$omp parallel
!---code---
!$omp end parallel
```
If the directive needs to be continued to next line put an `&` at the end. Any part of the code that starts with `!$` will only be compiled when OpenMP is enabled
```fortran
! will only print when OpenMP is enabled
!$ print *, 'Hello'
```
&nbsp;


### OpenMP parallel region
A parallel region is declared by the `parallel` directive. Code inside the parallel region (by default) will be executed by all the threads
```fortran
!$omp parallel
!code to be executed in parallel
!$omp end parallel
```
&nbsp;


### Setting number of threads.
1. Using environment variable.
```bash
export OMP_NUM_THREADS=10
```

1. Using OpenMP function/subroutine
```fortran 
call omp_set_num_threads(10)
```

1. Using OpenMP directive
```fortran
!$omp parallel num_threads(10)
!code to be executed in parallel
!$omp end parallel
```

Each one of the above option to set number of threads has greater affinity than the before i.e. if all the option is set, the last one will take effect. Note, only the first option doesn't modify the code itself, so it may be more useful/portable.  </br>

&nbsp;


### Parallelizing `do` loops
#### OpenMP do loop directive.
```fortran
!$omp parallel do
do i=1,n
!code inside this do loop will be executed in parallel
enddo
!$omp end parallel do
```  


#### Scoping variable inside an parallel do loop: `private`/`shared` variable.
The `default` keyword define the default scope of the variable inside the do loop. In absence of any default scope,  
    - all loop index variable are private  
    - all other variables are shared  
    - all automatic variable inside a procedure call from the parallel region are private  
Also check `firstprivate` and `lastprivate` for more about scoping
```fortran
!$omp parallel do default(shared) private(x)
do i=1,n
    x = i**2
enddo
!$omp end parallel do
```
    


#### Parallelize multiple do loops: `collapse` clause.
The following parallelize 2 do loops. Note: The loops have to be in a canonical form
```fortran
!$omp parallel do default(shared) private(x) collapse(2)
do i=1,n
    do j = 1,n
        x = i**2 + j**2
    enddo
enddo
!$omp end parallel do
```
    

#### Perform reduction operation across threads: `reduction` clause.
The format for reduction is `reduction(<operator>:<variable>)`Variable inside the reduction clause stays private and after exiting the parallel region they are reduced using the specified operator. Following performs a sum over an array element in parallel using reduction
```fortran
total = 0 
!$omp parallel do default(shared) reduction(+:total)
do i=1,n
    total = total + array(i)
enddo
!$omp end parallel do
```
 

#### Behavior of parallelization: `schedule` clause: 
The OpenMP loop schedule clause determines how the corresponding loop iterations will be assigned to different execution threads. 
```fortran
!$omp parallel do schedule(<type>,<chunksize>)
do i=1,n
    !codes
enddo
!$omp end parallel do
```

<details>	
    <summary>There are 5 types of schedule in total:</summary>


1. `static`: If no chunksize is not provided, OpenMP will divide the whole iteration into equal (if possible) size of chunks and distribute them to the threads, otherwise it will be divided into number of iteration given by the chunksize. In `static` scheduling both the chunksize and their mapping to threads are constant, resulting in minimum overhead during parallelization, but may create a load imbalance if iterations are not equally distributed in threads. `static` scheduling is preferable when each iteration have almost equal computation requirement and the loop can be divided into approximately equal number of chunks as that of the threads. This is the default behavior, in case of no explicit scheduling is provided.


2. `dynamic`: Here OpenMP will split the whole loop into iteration-size/chunk-size, but they will be distributed to threads dynamically without any specific order. In dynamic scheduling the chunksize is constant but their mapping is dynamic. Due to this behavior this approach has the minimum load imbalance but at the same time it also introduce significant overhead during the parallelization. When different iteration of the loop require different computaion time, `dynamic` scheduling is preferable.

3. `guided`: Here both the chunk size and the mapping of the chunks are dynamic. The size of the chunk is proportional to the number of unassigned iterations divided by the number of threads and the size will decreased to chunksize.

4. `runtime`: Scheduling is set from the outside of the code through the `OMP_SCHEDULE` environment variable

5. `auto`: Here the comiler/machine will decide and/or runtime the best scheduling to apply to the corresponding loop.
</details>


&nbsp;
    


### Conditional parallelization: `if` clause.
If the parallel directive has an `if` clause then the directive only take effect only if the `if` clause satisfies    
```fortran
!$omp parallel do if(n>10)
do i=1,n
    ! This loop is parallelized only if n is greater than 10
enddo
!$omp end parallel do
```


&nbsp;


### Noniterative workshare: `sections` clause.
The OpenMP parallel sections parallelize blocks of code, separated by `section` clause, in threads. Here, all the 3 subroutine calls will be made in parallel.
```fortran
!$omp parallel sections
call sub1()
!$omp section
call sub2()
!$omp section
call sub3()
!$omp end parallel sections
```



&nbsp;



### Nested parallelism
Multiple OpenMP parallel regions can be nested inside each other. 
```fortran

!$ call omp_set_max_active_levels(2)   ! Allows 2 level of nested parallelization

!$omp parallel do default(shared) 
do i=1,n
    ! codes
    !$omp parallel do default(shared) 
    do j=1,m
        ! codes
    enddo
    !$omp end parallel do
enddo
!$omp end parallel do
```
The above code will be parallelized in 2 nested parallel regions i.e. if number of OpenMP threads is set to 4 then the innermost code will be executed by 4x4=16 threads. If one need to flexibly change the number of OpenMP threads in separate nested level then the following code have to be called 
```fortran
!$ call omp_set_dynamic(.true.)
```



&nbsp;


### Mutual exclusion synchronization: `critical` clause.
Block of code inside this clause can be run only by one thread at a time, i.e. their execution is mutually exclusive. 
```fortran
!$omp parallel 
!$omp critical
call sub1()
!$omp end critical
!$omp end parallel 
```



&nbsp;


### Coarse grain vs fine grain parallelisation
__Tl;dr__ Coarse grain means explicitly sharing of task in each threads and fine grain means let OpenMP handle how to share task in each thread.  


#### Coarse grain parallelisation 
Here a task is split in small number of large tasks and they are explicitly assigned to threads. In this case OpenMP only opertes each thread on disjoint part of the large task. Not always prefered. Imporper load balancing may occur
```fortran
points_per_thread = (n + nthreads - 1) / nthreads
!$omp parallel private(thread_num, istart, iend, i)
thread_num = 0  ! for  serial mode
!$ thread_num = omp_get_thread_num()
istart = thread_num * points_per_thread + 1
iend = min((thread_num+1) * points_per_thread, n)
!manually/explicitly split the do loops in each thread
do i=istart,iend
! work on thread’s part of array
enddo
...
!$omp end parallel
```


#### Fine grain parallelisation 
Here a task is split into large number of small task and they are implicitly shared in available threads. Preferable in most of the cases.
```fortran
!$omp parallel do  private(i)
do i=1,n
    ! codes !
enddo
!$omp end parallel do 
```
