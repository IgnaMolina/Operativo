		1. Int
		2. main (int argc, char * argv[])
		3. {
		4.     int *p = malloc(sizeof(int))         // a1;
		5.     assert(p != NULL);
		6.     printf("(%d) address pointed to by p: %p\n", getpid(), p);
		7.     * p = 0;
		8.     while (1) { 
		9.           Spin(1);
		10.          *p = *p + 1; // a3 
		11.           printf("(%d) p: %d\n", getpid(), *p);        / / a4 }
		12. }
		13. return 0;
		14. }