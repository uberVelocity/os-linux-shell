## OS - Assignment 2
### Exercise 1 - Writing a shell
#### Set of special characters: {<, >, |, &, ", \*?}
Need a parser for the input.
There are certain inputs which are possible.
#### Parser construction
Initial idea is to go through the input and create two buffers,
one for special characters and one for strings of characters.
Create two buffers of sizes that correspond to the number of special
characters / character strings and store the special characters and
strings into the buffer. An abstract structure may be created in order
to deal efficiently with the input.
The character '"' should parse everything as a string until the next '"'.
##### getopt() built-in function in C - might be useful
##### Chain of operations
1. Parse the input to check for valid expression.
2. Parse buffers to execute the expression.
3. Terminate processes that 

#### Possible inputs
1. After a "<" or a ">" you expect an input / output file. 
- This creates a pipe between the two files.
- \< redirects information into the lhs from the rhs.
- \> redirects information from the lhs into the rhs.
So, A > B should create a file descriptor that is used to communicate
between A and B. > will mean that A will write information to B.
This can be done by opening the file B and writing on B whatever output
A provides.
A \< B will mean that A will read information from B. This implies that
B should be opened and read until the eof. The information taken from
B should then be provided as input into A.
If no filename is provided: "Invalid syntax!".
2. [commandA] | [commandB] should create a new pipe between commandA
and commandB. 
If no command name is provided: ~something~.
Pipes and input/output redirection [example #1](http://www.cs.loyola.edu/~jglenn/702/S2005/Examples/dup2.html), [example #2](https://www.unix.com/programming/122360-c-piping-redirect-operator.html), [example 3] (https://www.geeksforgeeks.org/making-linux-shell-c/)

#### TODO:
- [ ] Parse special characters
- [x] Execute regular commands
- [x] Execute regular commands with multiple flags
- [ ] Execute composed commands
- [ ] Execute commands with special characters
- [x] Implement cd/exit/help (extension)
- [x] Auto-complete path names with tab (extension - GNU Readline)

#### Remaining Extensions:
- tab twice to show possibilities
- provide [emacs shortcuts](https://en.wikipedia.org/wiki/GNU_Readline)
- change environmental variables using export (can be used to implement [colors](https://www.cyberciti.biz/faq/bash-shell-change-the-color-of-my-shell-prompt-under-linux-or-unix/))
#### Notes
- A potential function that deals with the creation of a file descriptor
between two processes might be useful since one does not know how many
file descriptors shall be needed in advance. As such, each operation
that needs a file descriptor shall create its own dynamically.
- dup() used for handling the output / input from a file to a file
- redirection of input output happens before execute (and after fork?)
- separate logic of parser from executions of functions
- struct that represents input line; as soon as it hits newLine, execute that line
it could have multiple commands and these commands could have multiple executions.
- flex file?
- useful tutorial https://brennan.io/2015/01/16/write-a-shell-in-c/
#### NMAP used in Assignment 2
- producer and consumer
