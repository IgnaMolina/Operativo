- Interlude:
	- The problem of developing one of the most well-known approaches to scheduling, known as **Multi-Level Feedback Queue (MLFQ)**. The fundamental problems that MLFQ address is two-fold. It would try to optimize *turnaround time*, and will try to make a system feel responsive to interactive users.
	
- Basic rules:
	- The MLFQ has a number of distinct **queues** , each assigned a different **priority level**, to clarify a job that is ready to run is on a single queue. MLFQ uses priorities to decide witch job should run at a given time, a job whit higher priority is chosen to run. So, what happen when two jobs have the same priority? well, to solve this, we arrive to our first set of rules:
		1.  If a priority (A) > priority (B), A runs (B doesn´t).
		2.  If a priority (A) = priority (B), A & B run in RR.
	
	- But MLFQ not assign a priority and nothing more, no, MLFQ varies the priority of a job based on its *observed behavior*, for example, a job that repeatedly relinquishes the CPU while waiting for input from the keyboard will keep its priority high, in the other hand, if the job uses the CPU for intensively and long periods of time, it will reduce its priority. So MLFQ will *learn* about processes as they run, and try to predict its *future* behavior using the *history* of the job. The key now is to understand how MLFQ does this, how changes priority.
	
- **How to Change Priority**:
	- To do this, we must keep in mind our workload: a bunch of interactive jobs that are short-running and some longer-running "CPU-bound" jobs that uses a lot of the CPU time. For this, we need a new concept, **Allotment**. The allotment is the amount of time a job can spend at a given priority level before the scheduler reduces its priority. Lets set some more rules, it will be fun, i promise. 
		3. When a job enters the system, it is placed at the highest priority.
		4.  If a job uses up its allotment while running, its priority is reduced. 
		5.  After some time period **S**, move all the jobs in the system to the top most queue.
	- Check [[Figure 8.4]] for a visual help whit this rules. The addition of the time period S leads to the question: ¿What should **S** be set to? This could look as voo-doo magic, there is no correct answer, the truth is that if S is set too high, loon-running jobs could starve, too low and interactive jobs may not get a proper share of the CPU, of course there's some automatic methods based on machine learning.
	