04.asm

This 32-bit Linux assembly program demonstrated how stack frames and 4-byte values operate using ESP. 
Function Call: Executing call work pushes the 4-byte return address onto the stack, changing ESP to S - 4 before entering the subroutine.
Frame Setup: Executing push ebp saves the old frame pointer at the top of the stack and changes ESP to S - 8, while mov ebp, esp sets the frame base to S - 8.
Local Storage: Subtracting 8 from ESP reserves local space, setting ESP to S - 16. The dwords at [ebp - 4] and [ebp - 8] are set to 100 and 200, respectively, and copied into EAX and EBX without modifying ESP.
Teardown and Return: Releasing the local dwords via mov esp, ebp restores ESP to S - 8, and pop ebp restores the saved frame pointer and moves ESP to S - 4. Finally, ret removes the return address and returns to \_start, restoring ESP to S before the exit syscall.
Conclusion: Built successfully in 32-bit mode using ld -m elf_i386, the program discards its local storage, rebalances the stack pointer, and terminates cleanly with status 0 without producing any terminal output.