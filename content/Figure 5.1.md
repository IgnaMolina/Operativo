1. int main(int argc, char *argv[]) {
2.      printf("hello (pid:%d)\n", (int) getpid()); int rc = fork(); 
3.      if (rc < 0) { 
4.           // fork failed 
5.           fprintf(stderr, "fork failed\n"); 
6.           exit(1); 
7.      } else if (rc == 0) { 
8.            // child (new process) 
9.            printf("child (pid:%d)\n", (int) getpid()); 
10.    } else {
11.          // parent goes down this path (main) 
12.          printf("parent of %d (pid:%d)\n", rc, (int) getpid()); 
13. }
14. return 0;}
15. Figure 5.1 Calling fork( ) (p1.c)

When you run this program you´ll see the following:
prompt> ./p1 
hello (pid:29146) 
parent of 29147 (pid:29146) 
child (pid:29147) 
prompt>