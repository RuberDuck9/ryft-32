# ryft-32   
A fully custom 32 bit cpu - also built on a custom architecture - capable of complex cisc-like instructions.        

## Bit Allocation / Instruction Format   
   
1x32bit bus   
[00000][00000000000][00000000000][00000]    
[Opcode][Argument 1][Argument 2][Argument 3]     

Arguments are used as a way of subdividing the bus to make more complex instructions possible. Although arguments can still be combined in some cases - such as the imm instruction which treats arguments 1 and 2 as one - they are generally used as ways to pass multiple different values to the cpu.
       
## Components     

- System Clock: toggles between an on and off state at a given rate, which other components use to synchronize themselves    
- Instruction Pointer: increases by one each clock cycle unless modified by an instruction, controls read address of the instruction register   
- Instruction Register: stored instructions for the cpu to carry out once turned on, stores data as binary hex values, reads from address specified by instruction pointer    
- Instruction Decoder: reads the opcode bits (0-4) from the instruction register and determines which instruction to execute    
- Registers: hold temporary values that the cpu needs in the very short term      
- RAM: holds more long-term data for the cpu      
- The Stack: stores data sequentially for the cpu, cannot be accessed out of outer           
- ALU: performs all math operations for the cpu, operation to be performed is controlled by the instruction decoder     

## Instructions    

- NOP [00000] : no instruction    
- IMM [00001] : store the value typed out across arguments 1 and 2 to the register address specified in argument 3     
- CPY [00010] : copy the value from the register address specified in argument 1 to the register address specified in argument 3, argument 2's value is ignored for this    
- ADD [00011] : add the value held at the register address specified in argument 1 and the value held at the register address specified in argument 2, and store it at the register address specified in argument 3    
- AD1 [00100] : add the value specified in argument 1 and the value held at the register address specified in argument 2, and store it at the register address specified in argument 3    
- AD2 [00101] : add the value held at the register address specified in argument 1 and the value specified in argument 2, and store it at the register address specified in argument 3    
- CKJ [00111] : check if adding the values held at the register addresses specified in arguments 2 and 3 would have a carry, if so, set the instruction pointer to the value typed in argument 1        
- SUB [01000] : subtract the value held at the register address specified in argument 2 from the value held at the register address specified in argument 1, and store it at the register address specified in argument 3    
- MLT [01001] : multiply the value held at the register address specified in argument 1 and the value held at the register address specified in argument 2, and store it at the register address specified in argument 3     
- AND [01010] : and each bit of the values held at the addresses specified in arguments 1 and 2 and save it to the address specified in argument 3   
- ORR [01011] : or each bit of the values held at the addresses specified in arguments 1 and 2 and save it to the address specified in argument 3   
- NOR [01100] : nor each bit of the values held at the addresses specified in arguments 1 and 2 and save it to the address specified in argument 3   
- STR [01101] : store the value held at the address specified in argument 1 to the address specified in argument 2 in ram, argument 3's value is ignored for this   
- LOR [01110] : load the value held at the address specified in argument 1 from ram and save it at the register address specified in argument 3, argument 2's value is ignored for this  
- PSH [01111] : push the value stored at the address in either argument 1 to the stack, the values of argument 2 and 3 value are ignored for this    
- POP [10000] : pop the top value from the stack and save it to the address specified in argument 3, the values of argument 2 and 3 value are ignored for this   
- RST [10001] : set the value of the instruction pointer to zero, all argument values are ignored for this      
- GTO [10010] : set the value of the instruction pointer to the value specified in argument 1, the values of argument 2 and 3 value are ignored for this      
- EQL [10011] : compare the values stored at the addresses specified by arguments 1 and 2, if they are equal, set the instruction pointer value to the one specified in argument 3     
- EQL [10100] : compare the values stored at the addresses specified by arguments 1 and 2, if they are not equal, set the instruction pointer value to the one specified in argument 3     
- GRT [10101] : compare the values stored at the addresses specified by arguments 1 and 2, if the value held at the address specified argument 1 is greater than that of argument 2, set the instruction pointer value to the one specified in argument 3     
- LES [10101] : compare the values stored at the addresses specified by arguments 1 and 2, if the value held at the address specified argument 1 is less than that of argument 2, set the instruction pointer value to the one specified in argument 3      
- CAL [10110] : push the current instruction pointer value + 4 to the stack (to prevent infinite loops) and then jump to the address specified in argument 1, the values of argument 2 and 3 value are ignored for this     
- RET [10111] : pop the top value off the stack and set the instruction pointer equal to that value, all argument values are ignored for this   
- HLT [11111] : stop the system clock, all other arguments are null for this instruction

## Registers

Due to the bit size of argument 3 - which is used primarily for specifying register address - there are 2^5 possible register addresses. Still, memory shouldn't be a problem for most reasonable programs, since the amount of ram is much more generous. Register addresses are numbered 0 to 31, HOWEVER, register 0 has no write access and is always a permanent 0.
