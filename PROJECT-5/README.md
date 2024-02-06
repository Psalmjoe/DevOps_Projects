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

3. **Command substitution** : Command substitution allows you to capture the output of a command and use it as a value within your script. You can use the backtick or the syntax ```$()``` for it.

**Example** : Using backtick for command substitution

```current_date=`date +%Y-%m-%d` ```

**Example** : Using ```$()``` syntax for command substitution

```current_date=$(date +%Y-%m-%d) ```

4. **Input and Output** : Bash provides various ways to handle inputs and outputs. You can use the read command to accept user input, and output text to the console using the echo command. Additionally, you can redirect input and output using operators like > (output to a file), < (input from a file), and | (pipe the output of one command as input to the other).

Example : Accept user input

```
echo "Enter your name:"
read name

```

**Example** : Output text to the terminal

``` echo "Hello World" ```

**Example**: Output the result of a command into a file

``` echo "Hello World"  > index.txt```

**Example** : Pass the content of a file as input to a command

```grep "pattern" < input.txt```

**Example** : Pass the result of a command as input to another command

```echo "hello world" | grep "pattern"```

5. **Functions** : Bash allows you to define and use functions to group related commands together. Functions provide a way to modularize your code and make it more reusable. You can define function by using the function keyword or simply by declaring the function name followed by parentheses.

```
#!/bin/bash

# Define a function to greet the user
greet() {
    echo "Hello, $1! Nice to meet you."
}

# Call the greet function and pass the name as an argument
greet "John"

```
![Alt text](images/hello.png)


## Let's write our first shell script

**Step 1** : On your terminal, open a terminal called shell scripting using the command ```mkdir shell-scripting```. This will hold all the scripts that we will write in this project.

![Alt text](images/mkdir.png)

**Step 2** : Create a file called user-input.sh using the command ```touch user-input.sh```

![Alt text](images/touch.png)

Step 3 : Inside the file, copy and paste the block of code below:

```
#!/bin/bash

# Prompt the user for their name
echo "Enter your name:"
read name

# Display a greeting with the entered name
echo "Hello, $name! Nice to meet you."

```
![Alt text](<images/user script.png>)

The above script prompts for your name. After typing your name, it dispalys the text hello! Nice to meet you. Also #!/bin/bash specifies the type of interpreter to be used to execute the script.

**Step 4** : Save your file

![Alt text](<images/save file.png>)

**Step 5** : Run the command using ```sudo chmod +x user-input.sh```

![Alt text](<images/chmod user.png>)

**Step 6** : Run the script using the command ```./user-input.sh```

![Alt text](<images/user run script.png>)


## Directory Manipulation and Navigation

We will write a simple script that will display the current directory, create a new directory called "my_directory", change to that directory, create two files inside it, list the files, move back one level up, remove the "my_directory" and its contents and finally list the files in the current directory again.

Follow the steps below to do that :

**Step 1** : Open a file named *navigating-linux-filesystem.sh*