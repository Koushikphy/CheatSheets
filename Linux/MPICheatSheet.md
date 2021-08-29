### MPI Chetacheet for Fortran

#### Setup
```fortran 
    call MPI_INIT(ierr)
    call MPI_FINALIZE(ierr)
    ! `ierr` is the return code for the call, of type integer. All MPI routines in Fortran has an error code as last argument 
```

#### Basic information
```fortran
    call MPI_COMM_RANK(MPI_COMM_WORLD, rank, ierr) ! rank: rank/id of current process
    call MPI_COMM_SIZE(MPI_COMM_WORLD, num_procs, ierr) !num_procs: total number of process
    call MPI_GET_PROCESSOR_NAME(pName, nresLen, ierr)   ! get name of the host for current process
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

Distribute chunks of array to different processes and collect it
```fortran
    call MPI_Scatter(arrayMain, sendcnt, MPI Datatype, arrayChunks, recvcnt, MPI Datatype, source, MPI_COMM_WORLD, ierr)
    call MPI_GATHER(arrayChunks, sendcnt, MPI Datatype, arrayMain, recvcnt, MPI Datatype,destination, MPI_COMM_WORLD, ierr)
```


#### MPI data types:

