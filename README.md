# ryft-32   
A fully custom 32 bit cpu - also built on a custom architecture - capable of complex instructions throught the cisc architecture design model.     

# CISC Architecture Style:     

## Bit Allocation / Instruction Format   
   
1x32bit bus   
[00000][000000000][000000000][000000000]    
[Opcode][Argument 1][Argument 2][Argument 3]     

Arguments are used as a way of subdividing the bus to make more complex instructions possible. Although arguments can still be combined in some cases - such as the imm instruction which treats arguments 1 and 2 as one - they are generally used as ways to pass multiple different values to the cpu.
       
## Components     
      
Instruction Pointer: increases by one each tick unless modified by an instruction, controls read address of    
Instruction Register: stored instructions for the cpu to carry out once turned on, stores data as binary hex values, reads from address specified by instruction pointer     
Instruction Decoder: reads the opcode bits (0-4) from the instruction register and determines which instruction to execute    
Registers: hold temporary values that the cpu needs in the very short term      
RAM: holds more long-term data for the cpu      
The Stack: stores data sequentially for the cpu, cannot be accessed out of outer         

## Instructions    

NOP [00000] : no instruction    
IMM [00001] : store the value typed out across arguments 1 and 2 at the register address specified in argument 3     
CPY [00010] : copy the value from the register address specified in argument 1 to the register address specified in argument 2, argument 3's value is ignored for this    
ADD [00011] : add the value held at the register address specified in argument 1 and the value held at the register address specified in argument 2, and store it at the register address specified in argument 3    
AD1 [00100] : add the value specified in argument 1 and the value held at the register address specified in argument 2, and store it at the register address specified in argument 3    
AD2 [00101] : add the value held at the register address specified in argument 1 and the value specified in argument 2, and store it at the register address specified in argument 3    
CKJ [00111] : check if adding the values held at the addresses specified in arguments 1 and 2 would have a carry, if so, set the instruction pointer to the value typed in argument 3   
