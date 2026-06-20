## INTRODUCTION

### Bourne Again Shell

[Bash](https://en.wikipedia.org/wiki/Bash_\(Unix_shell\)) is the scripting language we use to communicate with Unix-based OS and give commands to the system.

Like a programming language, a scripting language has almost the same structure, which can be divided into:

- `Input` & `Output`
- `Arguments`, `Variables` & `Arrays`
- `Conditional execution`
- `Arithmetic`
- `Loops`
- `Comparison operators`
- `Functions`

## WORKING WITH COMPONENTS

### Conditional Execution

Conditional execution allows us to control the flow of our script by reaching different conditions. If we reach a specific condition, only the code for that condition is executed, and the others are skipped.

#### Shebang
The shebang line is always at the top of each script and always starts with "`#!`". This line contains the path to the specified interpreter (`/bin/bash`) with which the script is executed.

- if
- elif
- else

### Arguments, Variables, and Arrays

#### Arguments

The advantage of bash scripts is that we can always pass up to 9 arguments (`$0`-`$9`) to the script without assigning them to variables or setting the corresponding requirements for these.

![[Pasted image 20260616172638.png]]

#### Special Variables


| COMANDA | EXPLICACIÓ                                                                                                                    |
| ------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `$#`    | This variable holds the number of arguments passed to the script.                                                             |
| `$@`    | This variable can be used to retrieve the list of command-line arguments.                                                     |
| `$n`    | Each command-line argument can be selectively retrieved using its position. For example, the first argument is found at `$1`. |
| `$$`    | The process ID of the currently executing process.                                                                            |
| `$?`    | The exit status of the script. This variable is useful to determine a command's success.                                      |
| `$0`    | This special variable is assigned the name of the executed script.                                                            |

#### Arrays
There is also the possibility of assigning several values to a single variable in Bash. This can be beneficial if we want to scan multiple domains or IP addresses. These variables are called `arrays` that we can use to store and process an ordered sequence of specific type values.
![[Pasted image 20260616173145.png]]

### Comparison Operators

The `comparison operators` are used to determine how the defined values will be compared. For these operators, we differentiate between:

- `string` operators
- `integer` operators
- `file` operators
- `boolean` operators

#### String Operators

| OPERATOR | DESCRIPTION                                 |
| -------- | ------------------------------------------- |
| `==`     | is equal to                                 |
| `!=`     | is not equal to                             |
| `<`      | is less than in ASCII alphabetical order    |
| `>`      | is greater than in ASCII alphabetical order |
| `-z`     | if the string is empty (null)               |
| `-n`     | if the string is not null                   |

#### Integer Operators

| OPERATOR | DESCRIPTION                 |
| -------- | --------------------------- |
| `-eq`    | is equal to                 |
| `-ne`    | is not equal to             |
| `-lt`    | is less than                |
| `-le`    | is less than or equal to    |
| `-gt`    | is greater than             |
| `-ge`    | is greater than or equal to |

#### File Operators

| OPERATOR | DESCRIPTION                                            |
| -------- | ------------------------------------------------------ |
| `-e`     | if the file exist                                      |
| `-f`     | tests if it is a file                                  |
| `-d`     | tests if it is a directory                             |
| `-L`     | tests if it is if a symbolic link                      |
| `-N`     | checks if the file was modified after it was last read |
| `-O`     | if the current user owns the file                      |
| `-G`     | if the file’s group id matches the current user’s      |
| `-s`     | tests if the file has a size greater than 0            |
| `-r`     | tests if the file has read permission                  |
| `-w`     | tests if the file has write permission                 |
| `-x`     | tests if the file has execute permission               |

#### Logical Operators

| OPERATOR | DESCRIPTION            |
| -------- | ---------------------- |
| `!`      | logical negotation NOT |
| `&&`     | logical AND            |
| \| \|    | logical OR             |

### Arithmetic

In Bash, we have seven different `arithmetic operators` we can work with. These are used to perform different mathematical operations or to modify certain integers.



| OPERATOR     | DESCRIPTION                             |
| ------------ | --------------------------------------- |
| +            | Addition                                |
| -            | Subtraction                             |
| *            | Multiplication                          |
| /            | Division                                |
| %            | Modulus                                 |
| `variable++` | Increase the value of the variable by 1 |
| `variable--` | Decrease the value of the variable by 1 |


## SCRIPT CONTROL

### Input and Output

### Flow Control - Loops

Logical expressions of boolean values usually control the execution of a control structure. These control structures include:

- Branches:
    - `If-Else` Conditions
    - `Case` Statements
- Loops:
    - `For` Loops
    - `While` Loops
    - `Until` Loops

#### For Loops

![[Pasted image 20260616174944.png]]

#### While Loops
![[Pasted image 20260616175109.png]]


### Flow Control - Branches
#### Case Statements

![[Pasted image 20260616175255.png]]


## EXECUTION FLOW
### Functions
`Functions` are an essential part of scripts and programs, as they are used to execute recurring commands for different values and phases of the script or program. Therefore, we do not have to repeat the whole section of code repeatedly but can create a single function.
![[Pasted image 20260616175413.png]]

#### Parameter Parsing
An important difference between bash scripts and other programming languages is that all defined variables are always processed `globally` unless otherwise declared by "[local](https://www.tldp.org/LDP/abs/html/localvar.html)."
![[Pasted image 20260616175616.png]]

### Debugging

Bash allows us to debug our code by using the "`-x`" (`xtrace`) and "`-v`" options.

This process is also used to find vulnerabilities in programs.

















































