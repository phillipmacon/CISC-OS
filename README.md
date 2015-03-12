# CISC-OS
Operating system based on CISC.

## Abstract
The main goal of the project was to design resident monitor software similar to the monitor program utilized by the SANPER-1 lab unit. This software program is meant to provide the user with a variety of commands that run on the MC68000. This will provide the user with a suitable method of testing, debugging and for implementing some hardware designs.

### Objective
Design monitor program with a variety of commands namely<br />
  * Command Interpreter<br />
  * Command programs<br />
  * Debugger programs<br />
  * Help

### Problem
The main problem is to create a way to allow users to operate hardware designs which utilize the MC68K software functionalities for operation. This problem is address by implementing the commands for the monitor program mentioned above.

### Design Methodology
Firstly, the command interpreter code is written which allows for the software program to check if a valid command has been entered. If a valid command was not entered, an error is displayed to the screen together with information requesting the user to use the HELP command allowing the user to understand how to use the instructions.<br /><br />
Next, once a valid command is entered, the program jumps to the code used to execute that command and if any errors were present in the syntax, an error is displayed on the screen.<br /><br />
Consider a case when the user attempts to divide a number by zero. Since there is no definite result for this operation, an exception handling mechanism is utilized to provide better security. When such an error occurs, the program jumps to the exception handler and displays the contents of all registers to the screen before returning back to the program. The same idea is utilized for other debugger errors mentioned above.

###  Technology Used
  * EASY68K software tool<br />
  * ASM<br />
  * SIM

## Monitor Program
The monitor program provides the user a variety of software commands for changing memory, testing memory, debugger commands and even a help command used to provide the user with information on how to execute a certain function.

### Command Interpreter
The command interpreter is a routine or section of the code used to check if the command entered was a valid command or not. If the command was valid, program flow proceeds to appropriate routine but if the command was not valid, an error message is displayed

#### Algorithm and flowchart for command interpreter
  * Display prompt<br />
  * Get text from command line<br />
  * Compare first character with space or zero<br />
  * If space save pointer to on stack else get next character<br />
  * Loop back to compare character<br />
  * Compare characters between beginning of buff and first space with commands in command table<br />
  * If found go to subroutine, else increment command-list pointer<br />
  * If at end of command list, display error, else loop back to compare

### Debugger Commands
    1. Help
    2. MDSP (Memory Display)
    3. BKFL (Block Fill)
    4. GOTO (Go to Memory Address)
    5. MCHG (Modify contentents of memory)
    6. SRTW (Sort memory block)
    7. BKSH (Block Search)
    8. HXDC (Convert hexadecimal number to decimal)
    9. EXIT (Exit program)
    10. BKMV (Block move)
    11. BSET (Block set)
    
### Exception Handlers
   1. Address Error (ADR_ERR)
   2. Bus Error (BUS_ERR)
   3. Divide by zero error (DVZ_ERR)
   4. Illegal Instruction Error (ILS_ERR)
   5. Line A Error (LNA_ERR)
   6. Line F Error (LNF_ERR)
   7. Privilege Violation Error (PRV_ERR)
   
## Instruction Manual
Here is a quick guide on how to use the monitor program.
  * Open Easy68K and locate the assembly file.
  * Compile the source code by pushing the F9 key
  * If the code compiles without errors, a pop up window will show
  * Click on the button that says "Execute" to open up the simulator
  * Once the simulator is open, click F9 to start running the monitior program
  * A prompt should display in the I/O window
  * Type "HELP" to see a list of available commands and their usage
  * Choose a command to execute and type in your parameters
  * Note: All commands entered must be upper case
  * To exit the program, type "EXIT"
  
## Discussion
The major design challenge was to take into consideration all the errors which could occur while running the program and write codes for better protection. The extra protection prevents the program from breaking when wrong commands are entered by the user. As such, this ensures not only a fully working program but a robust program.

## Feature Suggestion
Though the resident monitor program designed worked properly, it provides the user with very limited functionality. The resident monitor can only be improved by increasing the number of debugger commands and protection through exception handlers. It would also be nice to have many of the helper subroutines such as ASCII to BCD, DECIMAL TO BCD included in the user menu.<br /><br />
The program code is generally modular and relies heavily on subroutines calls to perform much of the heavy lifting. However, reliance on subroutines makes the program vulnerable in such a way that if one register that is used elsewhere is modified or gets corrupted, the entire program may fail. It would be a good idea to convert all subroutines into MACROS that will reduce the need to use specific registers for particular subroutines.

## Conclusion
The overall outcome of the project was a fairly robust monitor program with a lot of time having been spent on developing it. Many other useful functions and subroutines exist in the program code but because of time did not make it to the user menu.<br /><br />
I have learned of key considerations that are needed while developing an operating system for 68K family of microprocessors and could use these ideas if I were to develop a similar programs for other microprocessor architectures
