- Prelude:
	- In this chapter we will have to understand the higg-level **policies** that the OS scheduler employs.
	
- Workload Assumptions: 
	- We understand that **workload** is the amount of processes running in te system; determining the workload is a critical part of building policies.
	
- Scheduling Metrics:
	- If we want to compare different scheduling policies we nee a **scheduling metric**, for now lets us a **turnaround time** metric, this metric is:
				*Turnaround*= *completion* - *arrival*.
	- We could say that the **turnaround** metric is actually a **performance** metric, we also have a **fairness** metric; performance and fairness are often at odds in scheduling, we may optimize performance but at the cost of preventing a few jobs from running, thus decreasing fairness, life isn´t perfect bro.
	
- **First In, First Out (FIFO).**
	- The most basic algorithm we can implement is **FIFO**, its pretty obvios, the first program that arrives is te first being process. Lets take for example three jobs: A, B and C, and lets assume that each job takes 10 seconds to complete, considering that arrival is 0, and because FIFO needs to process the first to arrive, lets say A arrive first, then B and lastly C, FIFO would lock something like the [[Figure 7.1]] or [[Figure 7.1.svg]]. A finished at 10, B at 20 and C at 30, and the computing turnaround time is as easy as that; now lets say that each job takes different times, lets say A takes 100 seconds, B takes 10 and C also 10, and they arrive in that order, first A, then b and lastly C, the FIFO would lock something like [[Figure 7.2]] or [[Figure 7.2.svg]], as you can see, this time, FIFO returns a **timearound** of 110, that's horrible, this is because until A is complete, B and C can not start processing, this is generally re refer to as the **convoy effect**.
	
- **Shortest Job First (SJF)**:
	- It turns out that a very simple approach solves the convoy effect, lets see what happen if we prioritize the shortest process, remember, they all arrive at the exact same moment, A  takes 100 seconds to complete, B takes 10 and C also 10,  you can see in [[Figure 7.3]] or [[Figure 7.3.svg]]that the turnaround time is 50, a lot lees than te 110 of te FIFO. But, what happen if the jobs arrive at different times, like A arrive at 0 and need 100 seconds to finish, B and C arrive at 10 and need 10 seconds each to complete, lest take a look at [[Excalidraw/Figure 7.4|Figure 7.4]] or [[Figure 7.4.svg]], as you can see, 103.33 seconds is wild.
	
- **Shortest TIme-to-Completition First (STCF):
	- Now, lets say that jobs don´t need to run till completion, if we follow the last example, the **Schedule** can do something wen B and C arrives, it can **preempt** job A and decide to run another job, lets take a look at [[Figure 7.5]] or [[Figure 7.5.svg]], as you can see, the OS prioritize the shortest job wen arrives.
	
- A New Metric: Response Time:
	- Lets asume now users would sit at a terminal and demand interactive performance from the system as well, and thus, a new metric was born: **Response Time**. We define response time as the time from when the job arrives in a system to te **FIRST** time it is scheduled:
					*Response* = *firstrun* - *arrival* 
	
- **Round Robin (RR)**
	- Round Robin instead of running jobs to competition, it runs a job for a time slice and then switches to the next job in te run queue, it does repeatedly until the jobs are finished. Lets take the schedule of [[Figure 7.5]] and the response time of each job is as follo: 0 for job A, 0 for B, and 10 for C, now lets take a look to [[Figure 7.6-7.7]] or [[Figure 7.6-7.7.svg]], as you can see, RR does something strange, you could say its cheating, but time response mesures the tima it takes each job to process for the first time, RR processes each job almos instant and clock the beast time. 
	