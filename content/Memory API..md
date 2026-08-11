- Types of Memory:
	- In running a C program, there are two types of memory that are allocated. The first is called **stack** memory, and allocations and deallocations of it are managed *implicitly*  by the compiler for you, the programmer; for this reason it is sometimes called **automatic** memory. Declaring memory on the stack in C is easy, its just int x; The compiler does the rest, when you return from the function, the compiler deallocates the memory for you.
	
	- If is this need for long-lived memory that gets us to the second type of memory, the **heap** memory, where all allocations and deallocations are *explicitly* handled by you. A heavy responsibility, like [[Spider-Man]] of [[Spider-Man.svg]]. And certainly the cause of many bugs. 
	
- The *Malloc( )* Call:
	- The **malloc ()** call is quite simple: you pass it a size asking for some room on the heap, and it either succeeds and gives you back a pointer to the newly-allocated space, or fail and returns **NULL**..
	
- The *free( )* Call:
	- Allocating memory is the easy part of the equation; knowing when, how, and even if to free is the hard part. Some common errors tat arise in the use of malloc and free are:
		- **Forgetting to Allocate Memory**: Many routines expect memory to be allocated before you call them, this will likely lead to a **Segmentation fault**.
		- **Not Allocating Enough Memory**: A related error is not allocating enough memory, sometimes called a **buffer overflow**. Oddly enough, depending on how malloc is implemented and many other details, the program will often run seemingly correctly.
		- **Forgetting to Initialize Allocated Memory**: Whit this error, you call malloc( ) properly, but forget to fill some values into your newly-allocated data types. If this happens your program will eventually encounter an **uninitialized read** where it reads, where it reads from the heap some data.
		- **Forgetting to Free Memory**: Another common error is known as a **memory leak**, and if it occurs when you forget to free memory. In long-running applications or systems, this is a huge problem, as slowly leaking memory eventually leads one to run out of memory.
		- **Freeing Memory Before You Are Done With It**: Sometimes a program will free memory before it is finished using it; such a mistake is called a **dangling pointer**. 
		- **Freeing Memory Repeatedly**: Programs also sometimes dree memory more than once, this known as the **double free*.
		- **Calling free() Incorrectly**: One last problem we discuss is the call of *free ( )* incorrectly. After all, free() expects you only to pass to it one of the pointers you received from malloc.