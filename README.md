<img src="img/logo.svg" width=100 height=auto />

bccvm is a <del>procedural</del> two-dimensional stack-based esoteric programming language, inspired by Befunge98, ><> and Forth. All programs written in bccvm are stored on a 2D plane/grid, and they are navigated through using arrow operators.

For instance, this is a valid bccvm program, that loops ad infinitum:
```
#!/usr/bin/bccvm
>v
^<
```

...same for this, program that takes a number as input and prints its square to the screen:
```
#!/usr/bin/bccvm
vveeeeeeeeeeeeeeeeeeeeeeeee"Please enter an integer: "<
>                                                     ^
 >&:*$@
```
You can view more examples in the ```examples``` folder...

## Instruction-set
These are all the opcodes bccvm supports...

| **Instruction** | **Stack before**       | **Stack after**               | **Name**            | **Description**                                                                   |
|-----------------|------------------------|-------------------------------|---------------------|-----------------------------------------------------------------------------------|
| 0-F             |                        | x\|x∈{0,1,2,...,15}           | PUSH                | Pushes a hexadecimal digit onto the stack                                         |
|                 |                        |                               | NOP                 | Does nothing (moves the program counter/instruction pointer)                      |
| #               |                        |                               | TRAMPOLINE          | "Jumps" over one instruction                                                      |
| ~               | x                      | !x                            | NOT                 | Pushes 0 if x is true, or 1 if x is false                                         |
| !               |                        |                               | CRASH               | Crashes the program via abort()                                                   |
| ^ v > <         |                        |                               | PCDIR               | Changes the direction of the instruction pointer to N, S, E & W                   |
| ?               |                        |                               | PCRAND              | Changes the direction of the instruction pointer to something random              |
| t               | x y                    |                               | TELEPORT            | Teleports the instruction pointer to coordinates {x,y}                            |
| _ \|            | x                      |                               | HIF VIF             | Goes W if true or E if false / N if true or S if false                            |
| + - * / %       | x y                    | (x+y),(x-y),(x*y),(x/y),(x%y) | ADD SUB MUL DIV MOD | Calculates an operation between the first two elements of the stack               |
| i d             | x                      | (x+1),(x-1)                   | INC DEC             | Increments/Decrements the first value on the stack                                |
| \               | x y                    | y x                           | SWAP                | Swaps the first two variables on the stack                                        |
| ( = ) z         | x y                    | 1,0                           | LT EQ GT NEQ        | Compares 2 variables and pushes 1 if the condition is met or 0 if not             |
| e               | x                      |                               | EMITB               | Emits a byte to stdout                                                            |
| $               | x                      |                               | EMITN               | Emits an int to stdout                                                            |
| .               |                        | x                             | INPB                | Gets a byte from stdin                                                            |
| &               |                        | x                             | INPN                | Gets a number from stdin                                                          |
| w               | x                      |                               | PUT/INSERT          | Inserts a new instruction x at the next PC coordinates                            |
| [ ] n u         |                        |                               | CPC                 | Change instruction pointer position only if the top of the stack is equal to zero |
| "               |                        |                               | ASCII               | String mode                                                                       |
| p               | x                      |                               | POP                 | Pops the stack                                                                    |
| r               |                        |                               | REV                 | Reverses the stack                                                                |
| :               | x                      | x x                           | DUP                 | Duplicates the top stack element                                                  |
| ;               | x y                    | x x x x x.... (y times)       | DUPY                | Duplicates x y times                                                              |
| s               | x x x x x... (y times) | x x x x x... y                | SK                  | Pushes the stack element count                                                    |
| @               |                        |                               | HALT                | Terminates the program                                                            |

