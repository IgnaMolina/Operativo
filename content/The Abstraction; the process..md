   - In this part, we discuss one of the most fundamental abstractions that the OS provides to user: the **process**. We can say that the process it is a **running program**, this last thing its a lifeless thing, it just sits in there on the disk, waiting to spring into action. It is the **Operating System** that take these bytes and gets them running.

   - When you want to run more than one program in your  PC, the pc takes care and run the millions of process that are necessary for an easy use. The **OS** creates this illusion by virtualizing the CPU. By running one process, then stopping it and running another, and so forth, it can promote the illusion that many virtual CPUs exist when in fact there is only one CPU. This basic technique, known as **time sharing** of the CPU. The **OS** will need both some low-level machinery and somo high-level intelligence. We call the low-level machinery mechanisms, are low-level methods or protocols that implement a needed piece of functionality, for example, to implement a **context switch**, gives te **OS** the ability to stop running one program and start running another; this **time-sharing** mechanism is employed by all modern **OSes**. As we already say in the previous chapter, **polices** are algorithms for making some kind of decision within te **os**. For example, given a number of possible programs to run, how to decide which program run first? well, a **scheduling policy** is the solution.
   
- The Abstraction: A Process:
	- The abstraction provided by the OS of a running program is something we will call a **process**, remember that a process it´s just a running program. Before jumping deeper into the definition of a process, first we have to understand its **machine state**: what a program can read or update when it is running. One obvious component of machine state that comprises a process is its *memory*. Instructions lie in memory, thus the memory that the process can address (called its **address space**) is part of the process.
	- Note that there are some particularly special registers that form part of this machine state, for example the **program counter (PC)** tells us which instruction of the program will execute next.
	
- Process API: There some processes thar are available in any modern operating system. 
	- **Create**: An operating system must include some method to create new processes.
	- **Destroy**: As there is an interface for process creation, also provide an interface to destroy processes forcefully. Many processes will run and just exit by themselves when complete. 
	- **Wait**: Sometimes it is useful to wait for a process to stop running.
	- **Miscellaneous Control**:  Other than killing or waiting for a process, most operating systems provide some kind of method to suspend a process, and then resume it.
	- **Status**: there are usually interfaces to get some status information about a process as well. 
	- Consult [[Figure 4.1.svg]] or [[Figure 4.1]]: Loading: From Program to Process.
	
- Process Creation: A Little More Detail.
	- You may be asking ¿How programs are transformed into processes?  Or mor specifically, how does the OS get a program up an running? Well, the first thing is to **load** its code and any static data, like initialized variables, into memory. Programs initially reside on **disk** in some kind of executable format. The process of loading a program and static data into memory requieres the OS to read those bytes from disk and place them in memory somewhere.
	
	- Once the code and static data are loaded into memory, the OS needs to do some things before running the process. Some memory must be allocated for the program´s **run-time stack** (or just **stack**). C programs use the stack for local variables, function parameters, and return addresses; The OS allocates this memory and gives it to the process. The OS may also allocate some memory for the program´s **heap**. The OS will also do some other initialization task, particularly as related to input/output.
	
- Process States:
	- Lets talk about the different **states** a process can be in at a given time:
		- **Running**: In the running state, a process is running on a processor. This means it is executing instructions.
		
		- **Ready**: In the ready state, a process is ready to run but for some reason the OS has chosen not to run it at this given moment
		
		- **Blocked**: In the blocked state, a process has performed some kind of operation that makes it not ready to run until some other event takes place. For example, when a process initiates an I/O requestto a disk, it becomes blocked and thus some other process can use the processor.
		
		- Please check [[Figure 4.2]] or [[Figure 4.2]] for a visual healp.
		
	- Being moved from ready to running means the process has been **scheduled**; Being moved from running to ready means the process has been **descheduled**. Once a process has become blocker, the OS will keep it as such until some event occurs, at that point, the process moves to the ready state again.
	
- Data Structures:
	- The  Os is a program, it has some key data structures that track various relevant pieces of information. To track the state of each process, the OS will keep some kind of **process list** for all processes that are ready. The OS must also track, in some wat, blocked processes.