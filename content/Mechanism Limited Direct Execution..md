- Interlude:
	- In order to virtualize the CPU, the OS needs to share the physical CPU among many jobs running, the basic idea is: run a process for a  little while, then run another one, and so forth. By **time** **sharing** the CPU, virtualization is achieved. There are a few challenges, the first is performance: how can we implement  virtualization  without adding excessive overhead to the system? Te second is control: How can we run a processes efficiently while retaining control over the CPU?
	
	- To solve this problems, we have to understand first a basic technique: *Limited Direct Execution*; To make a program run as fast as one expect, whit this technique, just run the program directly on the CPU, when the OS wishes to start a program running, it creates a process entry for it in a process list, allocates some memory for it, loads the program code into the memory, locates its entry point (main), jumps to it and starts running the user´s code. However, this approach rise a few problems, for example, if we just run a program, how can the OS make sure the program doesn´t do anything that we don´t want it to do. Or how can the OS stop it from running and switch to another process, for this to succeed we need a **time sharing**.
	
- Problem #1: Restricted Operations: 
	- For this problem, the approach we take is to introduce a new processor mode, know as **user mode**; code that runs in **user mode** is restricted in what it can do, for example, a process can´t issue a I/O request; doing so would result in the processor raising an exception, the OS would then likely kill the process.
	
	- In contrast to **user mode** is **kernal mode**, which the OS run on, code that run on this mode can do what it likes, including privileged operations.
	
	- However, theres another challenge, what should a user process do when it wants to perform a privileged operation; to enable this, hardware provides the ability for users programs to perform a **system call**, this special calls allow the kernal to carefully expose certain keys of functionality to user programs, such as accessing the file system, creating and destroying processes, communicating whit other processes, and more.
	
	- To execute a **system call** a program must execute a special **trap** instruction. This instruction simultaneously jumps into the kernal and raises the privilege level to **kernal mode**; once in this mode, te system can now perform whatever privileged operations are needed. When finished, te Os calls a special **return-from-trap** instruction, this instruction returns into the calling user program while simultaneously reducing the privilege level back to **user mode**. The hardware needs to save enough of the caller´s registers in order to be able to return correctly.
	
	- Now, how does the trap know which code to run inside the OS? The kernal does so by setting up a **trap table** at boot time. When the machine boots up, it does so in privileged mode. One of the first thing the OS thus does is to tell the hardware what code to run when certain exceptional events occur. To specify the exact system call, a **system-call number** is usually assigned to each system call; the OS make sure that this number is valid, and, if it is, executes the corresponding code.
	
- Problem #2: Switching Between Processes:
	- This should be simple, right? The OS just decide to stop one process and star another, but if a process is running in the CPU, this means that the OS is **not** running, if the OS is not running, then how can it do anything at all?
	
- **Cooperative Approach**: Wait for System Calls: 
	- In this approach, the OS **trust** the processes of the system to  behave reasonably; processes that run for too long are assumed to eventually give up the CPU, they use a **system call** to doit so, it could be any, asking to open a file an subsequently read it, or communicate whit other machine, in this utopian world, the OS includes an explicit **yield** system call, which does nothing except handle back the CPU. It´s also important to mention that process handle back te control when they try to do something illegal like access memory that they shouldn't.
	
	- In this systems, the OS regains control waiting for system calls or an illegal operation.
	
- **A Non-Cooperative Approach: The OS Takes Control:**
	- In this more realistic world, a **timer interrupt** is set up, a timer device can be programmed to raise an interrupt event every so many milliseconds; when this happens, the currently running process is halted, and a pre-configure **interrupt handler** in the OS runs. As you would expect, the OS must tell de hardware which code run when the timer interrupt occurs, thus, at boot time, also at boot time, the OS needs to start the timer, which of course its a privileged operation.
	
	- As te previous approach, the hardware needs to save enough of the state of the program that was running hen the interrupt occurred, this to eventually start back te process.
- Saving and Restoring Context:
	- Now that the OS has regained control, a decision has to be made: whether continue running the currently-running process, or switch to a different one. This decision is made following the **scheduler**. If the decision is to switch, the OS then executes a low-level piece of code which we refer to as a **context switch**. All the Os has to do is save a few registers values for the currently-executing process and restore a few for te soon-to-be-executing process. The OS thus ensures that when the retunr-from-trap instruction is finally executed, instead of returning to the process that was running, the system resumes execution of another process.
	
- Worried About Concurrency? 
	- You could ask ¿What happens when you´re handling one interrupt and another one happens?¿Does this break the kernal? Well, kinda, the OS does indeed need to be concerned as to what happens if, during interrupt or trap handling, another interrupt occurs. On simple thing the OS might do is **disable interrupts** during interrupt processing, although the OS has to be careful in doing so; disabling interrupts for too long could lead to los interrupts, which its bad.