### Buffer overflows and x86 fundamentals. 

3 categories of memeory:
stack 
heap
global/static


stack: The stack is a continuous memory segment where elements are added and removed in a last in first out order.
So the last element to be added is also the first one to be removed.

char a = 61, char b = 62 char c = 63 -> byte 32000 : 61, byte 31999: 62, byte 31998 : 63 

char d = 64 => byte 31997 : 64

What is frequently saved on the stack:

int equalIgnoreCase(char char1, char char2){ : the variables that are passes in the function 
  char lowerChar1 = tolower(char1); ----|---> the local variables initialized inside the function
  char lowerChar2 = tolower(char2); ----|
  return lowerChar 1 == lowerchar2;
} -> some temporary data that are saved by the compiler (most likely a few bytes)

[/insert stack_1 photo/]

The part shown in the "stack" is the memory allocated to EACH call of the function equalIgnoreCase. This part is called activation record or stack frame. 

What will happen when tolower(char) is called the first time? 
The tolower() stack frame will be pushed into the stack like any other function!

[/insert tolower_stack photo/]

Endianess: Endianess is the way integers are stored in memory. Integers are represented by many bytes thus a need to figure out a way how to store them into memory arose.

Suppose the following example:

#include <stdio.h>
int main() {
 int x = 0x42434445;
 char * bytes = (char*)&x;
 int i;
 for(i = 0; i < sizeof(int) / sizeof(char); i++)
printf("%02x\n", bytes[i]);
 return 0;
}

output: 45 44 43 42

Little endian is when the Least Significant Bit (LSB) is saved in the highest memory adress. (example above)
Big endian is when the Most Significant Bit (MSB) is saved in the highest memory adress. (how you would normally read a number)
Bi-endian is when the endianness can switch dynamically according to some prerequisites.


Compilation Workflow & Execution semantics. 

To answer whether a program is safe or not we must first know what will executing it do. 

[/insert compilation_pipeline photo/]

The execution workflow is as follows:

[/insert execution_workflow photo/]


The stack Grows DOWNWARD!

CALL - RET SEMANTICS. 

The cpu keeps track of the currenly executing instruction using a register called the instruction pointer (ip,eip, rip) depending on architecture.
When the cpu encounters a call <function_address> instruction, it performs two distinct actions automatically in a single step.
1) Push the return address: Takes the memory adress of the very nexty instruction and pushes it on to the top of the stack. This is the return adress.

suppose this pseudofunction:
main {
  n = n + 1
  func()
  n = n + 2
}

when func() is invoked, the address of n = n + 2 will be pushed into the stack, making it the return address of the function.
3) Jump to target: it updates the instruction pointer with the address of the target function. 

RET:
1) poip the return address
2) jump back to the memory address it pointed to
3) cleans up.


BUFFER OVERFLOWS
A buffer overflow occurs when data is written outside of the space allocated for the buffer.
C does not inherently check that writes are in bnoundss.
1) stack based
2) heap based. 











