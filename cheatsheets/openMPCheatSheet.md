### OpenMP cheat sheet for Fortran
---
1. Thread Level Parallelism 
1. Shared Memory Parallelism

---
1. **Compiling OpenMP code**
    It depends on the compiler, check the compiler manual for details. For `gfortran` and `ifort`, its `-fopenmp` and `-qopenmp` respectively
    ```bash
    # for gfortran
    gfortran code.f90 -fopenmp
    # for ifort
    ifort code.f90 -qopenmp
    ```

1. **OpenMP directive**
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

1. **OpenMP parallel region**
    A parallel region is declared by the `parallel` directive. Code inside the parallel region (by default) will be executed by all the threads
    ```fortran
    !$omp parallel
    !code to be executed in parallel
    !$omp end parallel
    ```

1. **Setting number of threads.**
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

    Each one of the above option to set number of threads has greater affinity than the before i.e. if all the option is set, the last one will take effect. Note, only the first option doesn't modify the code itself, so it may be more useful/portable.

1. **Parallelizing `do` loops**
    * OpenMP do loop directive.
    ```fortran
    !$omp parallel do
    do i=1,n
    !code inside this do loop will be executed in parallel
    enddo
    !$omp end parallel do
    ```

    * Scoping variable inside an parallel do loop: `private`/`shared` variable. The `default` keyword define the default scope of the variable inside the do loop. In absence of any default scope,  
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

 
    * Parallelize multiple do loops: `collapse` clause.   
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

    * Perform reduction operation across threads: `reduction` clause.  
    The format for reduction is `reduction(<operator>:<variable>)`Variable inside the reduction clause stays private and after exiting the parallel region they are reduced using the specified operator. Following performs a sum over an array element in parallel using reduction
    ```fortran
    total = 0 
    !$omp parallel do default(shared) reduction(+:total)
    do i=1,n
        total = total + array(i)
    enddo
    !$omp end parallel do
    ```
    * Learn more: Scheduling


1. Conditional parallelization: `if` clause.   
If the parallel directive has an `if` clause then the directive only take effect only if the `if` clause satisfies    
```fortran
!$omp parallel do if(n>10)
do i=1,n
    ! This loop is parallelized only if n is greater than 10
enddo
!$omp end parallel do
```



1. Noniterative workshare: `sections` clause.
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




1. Mutual exclusion synchronization: `critical` clause.  
Block of code inside this clause can be run only by one thread at a time, i.e. their execution is mutually exclusive. 
```fortran
!$omp parallel 
!$omp critical
call sub1()
!$omp end critical
!$omp end parallel 
```