	1. int main(int argc, char *argv[]) {
	2.    int fd = open("/tmp/file", O_WRONLY|O_CREAT|O_TRUNC, S_IRWXU); 
	3.    assert(fd >-1); 
	4.    int rc = write(fd, "hello world\n", 12); 
	5.    assert(rc == 12); 
	6.    close(fd); 
	7.    return 0; 
	8. }