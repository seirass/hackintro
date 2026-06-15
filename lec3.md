What are buffer overflows?

A buffer overflow occurs when data is written outside of the space allocated for the buffer. 
C does not check that writes are in bounds. 

Can we return control to another function?

Q: What is an exploit?
An exploit is an input that violates the intended semantics of the target applications. 
Q: What is a system call?
The way user-space programs invoke kernel space functionalities. 

\x90: nop instruction: A no-operation instruction that does nothing, useful for exploit development, used to make the landing space bigger and then slide onto the shellcode.


\xcc: An interrupt to stop the normal flow of execution and usually how debuggers like gdb implement breakpoints.

Calling conventions -x86/32 bit.


