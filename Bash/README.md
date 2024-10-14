<h1 style="color:#4b04c7">Bash</h1>

<h3 style="color:#4b04c7">Intro</h3>

> - <a style="color:#000000">Everyday computer tasks can be done using the concise scripts that Bash can produce</a>

```bash
#!/bin/bash

echo "Hello, World!"
```

> - <a style="color:#000000">Variables</a>

```bash
#!/bin/bash

AGE=25
echo $AGE
readonly AGE
AGE=26
echo $AGE

# Output
# 25
# line 6: AGE: is read-only
```

```bash
#!/bin/bash

AGE=25
echo $AGE
unset AGE
echo "empty":$AGE

# Output
# 25
# empty:
```

> - <a style="color:#000000">Global vs Local Scope</a>

```bash
#!/bin/bash

setAge() {
    echo "Inside Function Age: $AGE"
}
AGE=40
setAge
echo "Script Age: $tmp"

# Output
# Inside Function Age: 40
# Script Age: 40
```

```bash
#!/bin/bash

setAge() {
    local AGE=25
    echo "Local Variable Age: $AGE"
}
AGE=40
setAge
echo "Global Age: $tmp"

# Output
# Local Variable Age: 25
# Global Age: 40
```

> - <a style="color:#000000">Displaying Environment Variables</a>

> <strong>printenv</strong> and <strong>env</strong> Both of these commands list all the environment variables of the terminal


> - <a style="color:#000000">Reading Input</a>

```bash
#!/bin/bash

# Prompt the user to enter their name
echo "Input your name:"

# Read user input and store it in a variable named 'name'
read name

# Greet the user with their name
echo "Hello, $name!"
```

> - <a style="color:#000000">Array Declaration</a>

```bash
#!/bin/bash

# Declare an array named "colors" containing favorite colors
colors=("Red", "Blue" "Green" "Purple" "Yellow")

# Print the entire array
echo "My favorite colors are: ${colors[@]}"

# Output
# My favorite colors are: Red, Blue Green Purple Yellow
```

> - <a style="color:#000000">Special Variables</a>

```bash
#!/bin/bash

# Print the name of the script
echo "Name of the script: $0"

# Print the number of arguments passed to the script
echo "Number of arguments passed: $#"

# Print all the arguments passed to the script
echo "All arguments passed: $@"

# Check the exit status of the last command
echo "Exit status of the last command: $?"
```

<h3 style="color:#4b04c7">I/O Redirection</h3>

```bash
#!/bin/bash

# Using input redirection to read the contents of "exec_stderr.txt" and echoing them to the terminal
cat < exec_stderr.txt

# Using input redirection to read the contents of "input.txt" and output redirection to write them to "output.txt"
cat < input.txt > output.txt

# Redirecting the standard error (stderr) of a command to a file named "error.log"
command_that_might_generate_errors 2> error.log
# 2>' symbol is used for stderr redirection,
# which redirects the standard error (stderr) output of the command to the file "error.log"

# Appending the output of the date command to "log.txt" without overwriting its existing contents
date >> log.txt

# Redirecting the output of the ls command to grep as input, to list only files with a ".txt" extension
ls | grep '\.txt$'

# Using input redirection to read a number from "nums.txt"
# Performing arithmetic operation on the read number
read number < nums.txt
result=$((number * 2))

# Printing the result of the arithmetic operation
echo "The result of doubling the number from nums.txt is: $result"

# Redirecting the output of the command to both the terminal and a file using tee
ls -l | tee output.txt
# The | symbol (pipe) is used to redirect the output of the ls -l command as input to the tee command.
# tee output.txt redirects the output to both the terminal and a file named "output.txt".
# The "tee" command reads from standard input and writes to both standard output (the terminal) and the specified file.
```

<h3 style="color:#4b04c7">Conditionals</h3>

```bash
#!/bin/bash

# Prompt the user to enter a number
echo "Input a number:"
read n

# Check if the number is greater than 100
if [ "$n" -gt 100 ]; then
    echo "The number is greater than 100."
else
    echo "The number is not greater than 100."
fi

# Check if the file "test.txt" exists in the current directory
if [ -f "test.txt" ]; then
    echo "File exists"
else
    echo "File does not exist"
fi

# Define a string
input_str=""

# Check if the string is empty
if [ -z "$input_str" ]; then
    echo "The string is empty"
else
    echo "The string is not empty"
fi

# Predefined password
my_password="Pass0123$"

# Prompting the user to input a password
printf "Please input your password: "
# This command disables echoing of characters, so the password input is not displayed on the screen.
stty -echo
read user_password
# This command re-enables echoing of characters after the password has been entered.
stty echo
printf "\n"

# Checking if the entered password matches the predefined value
if [ "$user_password" = "$my_password" ]; then
    echo "Access granted"
else
    echo "Access denied"
fi

# Prompting the user to input a number
echo "Please input a number:"
read number

# Checking if the input is a valid number
if [[ ! "$number" =~ ^[0-9]+$ ]]; then
    echo "Invalid input. Please enter a valid number."
    exit 1
fi

# The ! operator negates the condition, so it checks if the input does not match the pattern ^[0-9]+$,
# which means one or more digits from 0 to 9

# Checking if the number is even or odd
if (( number % 2 == 0 )); then
    echo "$number is even."
else
    echo "$number is odd."
fi

# [[...]] is for conditional expressions and ((...)) is for arithmetic expressions

# Check if the file "abc.sh" exists
if [ -e "abc.sh" ]; then
    # Check if the file is executable
    if [ -x "abc.sh" ]; then
        # If executable, run the script
        ./abc.sh
    else
        # If not executable, print message
        echo "Script is not executable"
    fi
else
    # If the file does not exist, print message
    echo "File 'abc.sh' does not exist"
fi

# Prompting the user to enter a number
echo "Input a number:"
read n

# Checking if the number is positive, negative, or zero
if (( n > 0 )); then
    echo "The number is positive."
elif (( n < 0 )); then
    echo "The number is negative."
else
    echo "The number is zero."
fi

# Getting the username of the logged-in user
logged_in_user=$(whoami)

# Checking if the user is logged in
if [ -n "$logged_in_user" ]; then
    echo "The logged-in user is: $logged_in_user"
else
    echo "User is not logged in"
fi
```
