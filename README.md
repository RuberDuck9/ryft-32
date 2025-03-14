# ryft-32   
A fully custom 32 bit cpu - also built on a custom architecture - capable of complex instructions throught the cisc architecture design model.     

# Architecture Style: CISC    

## Bit Allocation / Instruction Format   
   
1x32bit bus   
[000000000][000000000][000000000][00000]   
[Argument 3][Argument 2][Argument 1][Opcode]   

Arguments are used as a way of subdividing the bus to make more complex instructions possible. Although arguments can still be combined in some cases - such as the imm instruction which treats all 3 arguments as one - they are generally used as ways to pass multiple different values to the cpu.
