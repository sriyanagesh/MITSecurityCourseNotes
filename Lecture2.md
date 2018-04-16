Note: These notes are based on my understanding of the lecture and may not be completely and accurate.

Lecture2: Buffer Overflow Attacks
---------------------------------

Introduction:
Buffer overflow is when a process writes into more memory than what's allocated to it.                                        C is more vulnerable to buffer overflows attacks that Java
and C# because, in Java and C#, arrays are treated as objects and there are
functions associated with the array object which check whether a buffer
overflow is occurring. In C, arrays are data structures and no such check
happens. This makes C more vulnerable as well as faster. Functions like gets,
malloc etc. can be dangerous in this aspect.

3 ways to detect buffer overflow attacks:
Buffer overflow attacks can go undetected for a long time and the following
methods can help detect these attacks

1. Canaries 
Canaries are memory blocks containing a value that is pre-known. The canary is
usually placed after the buffer (in the way of the buffer growth) and whenever
a buffer operation occurrs, the canary's
value is checked. If the canary value has changed, then a buffer overflow has
occurred which has replaced the canary's original value. 

2. Guard pages
A guard page is a chunk of memory (at least a page) placed between memory
chunks. If an attempt is made to write into a guard page, a segmentation fault
occurs.

3. Fat Pointers
A regular pointer is 4 bytes long to hold the address of the memory. A fat
pointer is typically 4x3=12 bytes long and stores the start, end and current memory
address of the allocated buffer. Instrumented code of the compiler
checks if the address of the pointer lies between the start and end points
before performing any pointer operation. The disadvantage of a fat pointer is
that it is not always backward compatible. Legacy code does not expect a
pointer to be 12 bytes long.

Baggy bounds algorithm
-----------------------

Buddy allocation:
Baggy bounds algorithm depends on the buddy memory allocation technique. In
this technique, memory is divided in powers of 2. 
Example1: 64 bytes is requested
A 128 byte block is divided into two and one of the two blocks is allocated
Example2: 65 bytes is requested
A 128 byte block is allocated. If half of the block is more than the
requested size, then that block is allocated
Example 3: 40 bytes is requested
A 64 byte block is allocated because 64/2=32 < 40

There are 4 rules to this algorithm:

Rule 1: Memory is rounded to power of 2
Rule 2: The size information is stored in log 2 value
Rule 3: A linear table called the bounds table is used to store the bounds
information
Rule 4: Memory is allocated in terms of slot size which is a power of 2
Example1:int ``*p = malloc(32)
Here, a 32 byte block is assigned to p. Assume slot_size=16
In t[p/slot_size]=5, t[(p/slot_size)+1]=5
During pointer operation, the size and the range of p can be determine
arithmetically.

Example of alogorith in work:
int *p = malloc (40)
int *q = p + 20 // No error since p has 64 bytes of memory
int *r = q + 16 // results in an error since r is at a position great than
half slot size
int *s = p + 30 // No error since s is at 70 which is 64 + 6 (6 is less than
half slot_size). If you dereference s, it will result in an error
int *t = s - 32 // s is brought back in bounds``
 
##Cons

*Space*
	Extra space to store the bounds table
*CPU*
	Extra processing time for the arithmetic operations
*False alarms*
 	The algorithm might throw an error when out of bounds memory address is assigned and not dereferenced yet

