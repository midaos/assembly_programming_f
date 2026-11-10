06.asm

This 32-bit Linux assembly program serves as the counterpart to example 05, utilizing ESP and 4-byte stack slots. 
Initial Setup: Initializing EAX to 0x11223344 and EBX to 0x1234 leaves the stack pointer unchanged.
Pushing Data: Executing push eax subtracts 4 from ESP and stores 0x11223344 at [S - 4]. Following this with push ebx subtracts another 4 and stores 0x1234 at [S - 8], making that the top item.
Popping Data: The instruction pop ebx restores 0x1234 and increments ESP by 4 to S - 4. Next, pop eax restores 0x11223344 and increments ESP by 4, fully restoring ESP to S.
Conclusion: Once the stack is balanced, the code sets the i386 exit syscall number and status, then terminates via int 0x80. The values return to their original registers in last-in, first-out order, and nothing is printed to the terminal.