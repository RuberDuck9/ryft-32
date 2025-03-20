# ryft-32   
A fully custom 32 bit cpu - also built on a custom architecture - capable of complex instructions throught the cisc architecture design model.     

# Architecture Style: CISC    

## Bit Allocation / Instruction Format   
   
1x32bit bus   
[000000000][000000000][000000000][00000]     
[Opcode][Argument 1][Argument 2][Argument 3]     

Arguments are used as a way of subdividing the bus to make more complex instructions possible. Although arguments can still be combined in some cases - such as the imm instruction which treats all 3 arguments as one - they are generally used as ways to pass multiple different values to the cpu.

## Instructions

NOP [00000] : no instruction
IMM [00001] : store the value typed out across arguments 1 and 2 at the register address specified in argument 3
CPY [00010] : copy the value from the register address specified in argument 1 to the register address specified in argument 2, argument 3's value is ignored for this
