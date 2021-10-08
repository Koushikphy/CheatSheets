### MPI Chetacheet for Fortran

#### Setup
```fortran 
    call MPI_INIT(ierr)

    !!!!!!!!!!!!!!
    ! Codes
    !!!!!!!!!!!!!!

    call MPI_FINALIZE(ierr)
    ! `ierr` is the return code for the call, of type integer. All MPI routines in Fortran has an error code as last argument 
```

#### Basic information
```fortran
    call MPI_COMM_RANK(MPI_COMM_WORLD, rank, ierr)      ! rank: rank/id of current process
    call MPI_COMM_SIZE(MPI_COMM_WORLD, num_procs, ierr) ! num_procs: total number of process
    call MPI_GET_PROCESSOR_NAME(pName, nresLen, ierr)   ! pName: name of the host for current process
```

#### Communication
Explicit Send and Receive data with one-to-one communication. `Send` is called only at source and `Recv` only at destination.
```fortran
    call MPI_Send(variable, length, MPI Datatype, destination, tag, MPI_COMM_WORLD,ierr) 
    call MPI_Recv(variable, length, MPI Datatype, source, tag,MPI_COMM_WORLD, status, ierr)

    !variable : data to send
    !length : length of the data
    !destination: rank of the process to send the data
    !source: rank of the process sending the data
    !tag : a unique integer, to communicate with different Send/Recv
```

Send data to all the available processes . `Bcast` is called in all processes, `source` sends the data and other process receives it. 
```fortran
    call MPI_Bcast(variable,length, MPI Datatype,source,MPI_COMM_WORLD,ierr)
```

Distribute chunks of array to different processes and collect it. `MPI_Scatter`, `MPI_Gather` can only distribute and collect equal length of chunks.
```fortran
    call MPI_Scatter(arrayMain, sendcnt, MPI Datatype, arrayChunks, recvcnt, MPI Datatype, source, MPI_COMM_WORLD, ierr)
    call MPI_Gather(arrayChunks, sendcnt, MPI Datatype, arrayMain, recvcnt, MPI Datatype,destination, MPI_COMM_WORLD, ierr)

    ! arrayMain : main array, chunks of which will be distributed
    ! arrayChunks: array to store the chunks
    ! source : rank of process, from where the array is distributed
    ! destination : rank of process, where to gather


```
Distribute chunks of array of unequal length to different processes and collect it.
```fortran
    call MPI_Scatterv(arrayMain,counts,displ,MPI Datatype,arrayChunks,mycounts,MPI Datatype,source,MPI_COMM_WORLD,ierr)
    call MPI_Gatherv(arrayChunks,mycounts,MPI Datatype,arrayMain,counts,displ,MPI Datatype,destination,MPI_COMM_WORLD,ierr)

    ! counts : array of chunksizes, that will be distibuted.
    ! mycounts : size of the received chunk of array in the current process
    ! displ : Start index of different chunks in the main array.
```
