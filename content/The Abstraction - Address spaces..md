- Early Systems:
	- From the perspective of memory, early machines didn´t provide much of an abstraction to users. But, after a time, because machines were expensive, people began to share machines more effectively. The era or **multiprogramming** was born, in which multiple processes were ready to run at a given time ande the OS would switch between them.
	
	- We had to solve how to give memory to each program, at first the OS will gave full access to memory, then stop it, this approach has a big problem, it is way to slow, particularly when memory grows. What we´d rather do is leave processes in memory while switching between them, allowing the OS to implement time sharing efficiently, as you can see in [[Figure 13.2]] or [[Figure 13.2.svg]].
	
- The Address Space:
	- We requiere the OS to create an **easy-to-use** abstraction of physical memory, we call this abstraction the **address space**. The address space of a process contains all of the memory state of the running program, lets sat the code for example. The program, while it is running, uses a **stack** to keep track of where it is in the function call chain as well as to allocate local variables and pass parameters and return values to and from routines. The **heap** is used for dynamically-allocated, user-managed memory, such as *malloc( )* in C. For now let us just assume those three components: code, stack, and heap. Check [[Figure 13.3]] or [[Figure 13.3.svg]]for a visual help. Because code is static, we can place it at the top of the address space and know that it won´t need any more space, after that we have two regions of the address space that may grow or shrink while the program runs. We place them like this because each wishes to be able to grow, and putting them at opposite ends of the address space, we can allow such growth. This placement is just a convention not a rule. 
	
	- To clarify, the memory that we describe is in reality the **abstraction** that the OS is providing to the running program, the program isn´t in memory physical addresses 0 through 16KB. This is **virtualizing memory**.
	
- Memory goals:
	- To make sure our OS is the best, we need some goals to guide us, such as:
		- **Transparency**: The OS should implement virtual memory in a way that is invisible to the running program, the program shouldn't be aware of the fact that memory is virtualized.
		- **Efficiency**: The OS should strive to make virtualization as **efficient** as possible, both in terms of time and space.
		- **Protection**: The OS should make sure to **protect** processes from one another as well as te OS itself from processes.