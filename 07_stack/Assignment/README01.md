01.asm

This 64-bit Linux assembly program demonstrates how the hardware stack operates using push and pop instructions. 
Assuming S represents the initial stack pointer (RSP) provided by the kernel upon startup:
Initial Setup: Moving values into rax (100) and rbx (200) occurs entirely within registers without altering the stack.
Pushing Data: Executing push rax decreases the stack pointer by 8 and places 100 at memory location
 [S - 8]. Following this with push rbx decreases the pointer by another 8 and places 200 at [S - 16], making it the new top of the stack.
 Popping Data: The instruction pop rcx retrieves the 200 value into RCX and increases the stack pointer back to S - 8. 
 Next, pop rdx retrieves the 100 value into RDX and further increases the pointer, fully restoring RSP to its original value S.
 Conclusion: Interspersed nop instructions leave the stack untouched, and because _start functions as the entry point rather than a standard subroutine, the program uses an explicit exit syscall instead of a ret instruction.Ultimately, the LIFO nature of the stack reverses the order during the pop phase.