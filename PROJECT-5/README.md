# Introduction to Shell Scripting and User Input

The shell is a program that provides the user with an interface to use the operating system’s functions through some commands.

A shell is a special user program that provides an interface for the user to use operating system services. Shell accepts human-readable commands from users and converts them into something which the kernel can understand. It is a command language interpreter that executes commands read from input devices such as keyboards or from files. The shell gets started when the user logs in or starts the terminal.

Shell scripts are mostly used to avoid repetitive work. You can write a script to automate a set of instructions to be executed one after the other, instead of typing in the commands one after the other n number of times.

## Shell Scripting Syntax Element

1. **Variables** : Bash allows you to define and work with variables. Variables can store data of all types such as numbers, strings and arrays. You can assign values to variables using == operator and access their values using the variable name preceded by a ```$``` sign.

Example: Assigning value to a variable:

```name=""Psalm```

![Alt text](images/variable.png)

```echo $name```

![Alt text](images/variable.png)

2. **Control flow** : Bash provides control flow statements like if-else, for loops, while loops ans case statements to control the flow of execution in your scripts. These statements allow you to make decisions, iterate over lists and, executes different commands based on conditions.

Example: Using if-else to execute scripts based on conditions :

```
#!/bin/bash

# Example script to check if a number is positive, negative, or zero

read -p "Enter a number: " num

if [ $num -gt 0 ]; then
    echo "The number is positive."
elif [ $num -lt 0 ]; then
    echo "The number is negative."
else
    echo "The number is zero."
fi

```
![Alt text](images/flow.png)

The code prompts you to type a number and prints a statement stating whether the number is positive, negative or zero.

![Alt text](<images/flow script.png>)

**Example**: Iterating through a list using a for loop :

```
#!/bin/bash

# Example script to print numbers from 1 to 5 using a for loop

for (( i=1; i<=5; i++ ))
do
    echo $i
done

```

![Alt text](images/loop.png)