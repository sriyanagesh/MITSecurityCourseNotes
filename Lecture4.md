Note: These notes are based on my understanding of the lecture and may not be completely and accurate.

Lecture 4
----------
#Privilege Separation
Instead of all of the application having access to all of the data, we should divide the app into modules which have access to parts of the data. Even if one of the modules gets compromised, not all of the data is compromised. This isolation is provided by virtual machines, UNIX/LINUX etc. We'll see how unix provides this

##Files
Read, write and execute operations can be performed on files by user (owner of the file), group (the group that owns the file) and others. 

  R(4)  W(2)  X(1)
U Y	Y	Y  --> 7

G Y	Y	N  --> 6

O Y	N	N  --> 4

Apart from rwx, another operation that only the user can perform in the chmod, changing the permissions on a file.

##Directories
Read, write and execute operations can be performed on directories by user (owner of the file), group (the group that owns the file) and others. 

Read in directories means you can list the contents of the directory (perform ls command)
Write in directories means you can rename, move, create, delete a file in that directory
Execute in directories means you can access the files and directories in that directory (perform cd operation)

###Example1:
open("/etc/password")
The process should have:
x perm on /
x perm on etc 
r perm on password 

###Example2:
Q: If there are two groups, Group1 is all students of course 658 and Group2 is all TAs, how would you provide access to the file /foo/bar/grades.txt to only 658 TAs?
A: Provide X perm on / and foo to Group1 and provide X perm on bar and r perm on grades.txt to Group2

##File descriptors
When a file is opened, the necessary permission checks are done and the file descriptor is returned which allows the process to read/write into the file. A process can gain access to this FD in one of two ways:
1. A child process inherits all the FDs from its parent. 
2. If process1 gets a FD (rightfully) and passes it to process2, maybe through a network socket. So when process2 (who should not have access to the file) starts writing to the file, no additional permission checks are done 

##Processes
Create, Kill and debug (ptrace) operations can be performed on processes. Any process can create another process and the child process will have the same uid as the parent. Only the parent process or root can kill a process. 

##Network sockets
Any process can try to connect to a socket, but not all process can listen on all ports. Typically, non-privileged processes are allowed to listen in on ports>1024. Beause the lower numbered ports such as HTTP (80,8080) are important.

##setuid - root, logon

##Two ways of Privilege Escalation

##chroot

##OKWS paper

### Typical web service architecture

### OKWS web service architecture
