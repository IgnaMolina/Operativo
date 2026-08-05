
- The *fork( )* System Call:
	- The *fork( )* system call is used to create a new process: it is certainly the strangest routine you will ever call. You have a running program whose code looks like what you see in [[Figure 5.1]].
	- When it first started running, the process print hello, included in that message is its **process identifier**, also know as a **PID**, the PID is used to name the process if one wants to do something with the process, such as, for example, stop if from running. so far, so good.
	- The process calls the *fork( )* system call, so the Os provides as a way to create a new process, the odd part: the process that is created is an exact copy of the calling process. That means that to the OS, it now looks like there two copies of the program in [[Figure 5.1]] running, and both are about to return from the *fork( )* system call. The newly-created process, lets call it a **child** and the original **parent**, doesn´t start running at *main( )*, it just comes into life as if it had calle *fork( )* itself. Check te [[Figure 5.2]]
	- The child, or Figure 5.2, it now has its own copy of the address space, its own registers, its own PC, and so forth, the value it returns to the caller of **forck()** is different. This differentiation is useful, because it is simple then to write the code that handles the two different cases.
	- The output (of p1.c) is not deterministic. When the child process is created, there are now two active process, the parent and the child, either the child or the parent might run at that point. The CPU **scheduler** determines which process runs at a given moment in time.
   
- The *wait( )* System Call:
	- Sometimes it  is quite useful for a parent to wait for a child process to finish what it has been doing. This task is accomplished with the *wait( )* system call. In this example, [[Figure 5.2]] the parent process calls *wait( )* to block until the child finishes executing. Adding a *wait( )* call to the code above majes the output deterministic. If you run the code, you will notice that the child will print first, even though the parent runs first, it will call *wait( )*, this system call will not return until the child has run and exited. So the chill always runs first.
	
- The *exec( )* System Call:
	- This system call is useful when you want to run a program that is different from the calling program. Calling *forck( )* in p2.c is only useful if you want to keep running copies of the same program, often you want to run a different program; *exec( )* does just that. Check [[Figure 5.3]]
	
	- In this example the child process calls *execvp( )* in order to run the program wc, which is the word counting program. The *fork( )* system call is strange, its partner in crime, *exec( )* is not so normal either.
	
- Why? Motivating The API:
	- FALTA RESUMIR:
	