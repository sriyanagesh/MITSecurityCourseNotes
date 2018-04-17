Note: These notes are based on my understanding of the lecture and may not be completely and accurate.

Lecture 3
----------

Stack vs. Heap

Stack

	- Stack grows down and is used to store non-dynamic variables such as local function variables
	- The most recently inserted stack frame is the first to be removed/popped. For example, the most recently called function will be the first to return

Heap
	- Heap grows up and is used to store dynamic memory - memory allocated via new, malloc, calloc etc
	- Freeing memory in heap has nothing to do with the order of insertion

Note: Code is stored in a separate segment called as Code Segment

Other ways of handling/detecting buffer overflow attacks:

1. Non-executable memory - Attacker can overflow the buffer to insert code in the stack and then point the return address to that code. However, by making the stack/heap non-executable, this can be prevented. 

2. Randomized address space 

Real life buffer overflow attacks detection/handling techniques - GCC uses stack canaries, whereas LINUX uses non-executable memory and randomization of addresses


Defeating Canaries - Canaries can be defeated by guessing the bytes of the canary. This technique assumes that the program crashes when a canary is compromised and that after the system recovers from the crash, it maintains the address of the canary. In the technique, the attacker first guesses the fist byte of the canary. If the program does not crash, then he knows the value is right and then moves on to guessing the next byte.

Return Oriented Programming (ROP)

Because of the non-executable memory implementation, the attacker is unable to point the return address to his own malicious code. But he can use the existing program code to implement his evil plan. For example, if the existing program for some God forsaken reason has a function fun1() calling /bin/sh, the attacker could determine the address of that function by disassembling the program binary and can perform buffer overflow attack to replace the return address with address of fun1()

What if the programmer was not dumb enough to call /bin/sh in his program? What if he called system with ls and there is another string containing /bin/sh. In this case, the attacker needs to trick the system call into using /bin/sh and not ls as its argument. This can be done by buffer overflow as well.

What if the attacker wanted to call multiple system calls? He will use the pop ret gadget. 

What is the pop ret gadget?
The pop ret gadget contains two functions, pop and ret. pop pops the top of the stack into a register. ret executes whatever the stack pointer is pointing to and then pops the stack

Watch the video to understand how pop ret works. It is too complicated to explain here.
