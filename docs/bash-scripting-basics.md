# Bash Scripting Basics

Bash (Bourne Again SHell) scripting is a powerful way to automate tasks on Linux systems. This guide covers the fundamentals to help you get started with creating effective bash scripts.

## Creating Your First Script

1. Create a new file with a `.sh` extension:

   ```bash
   touch myscript.sh
   ```

2. Make it executable:

   ```bash
   chmod +x myscript.sh
   ```

3. Add the shebang line at the top:

   ```bash
   #!/bin/bash
   ```

4. Add commands and save:

   ```bash
   #!/bin/bash
   echo "Hello, World!"
   ```

5. Execute the script:
   ```bash
   ./myscript.sh
   ```

## Basic Syntax

### Variables

```bash
# Variable assignment (no spaces around =)
name="John"
age=30
current_date=$(date +%Y-%m-%d)

# Using variables (with $ prefix)
echo "Hello, $name!"
echo "You are $age years old."
echo "Today is $current_date"

# Variables with curly braces (recommended for clarity)
echo "Hello, ${name}!"
```

### User Input

```bash
# Read input with prompt
echo -n "Enter your name: "
read name

# Read input with prompt in one line
read -p "Enter your age: " age

# Read secret input (passwords)
read -sp "Enter password: " password
echo  # Add newline after password input

echo "Hello, $name! You are $age years old."
```

### Command Substitution

```bash
# Old syntax
kernel_version=`uname -r`

# Preferred syntax
user_count=$(who | wc -l)
current_dir=$(pwd)

echo "Kernel version: $kernel_version"
echo "Users logged in: $user_count"
echo "Current directory: $current_dir"
```

## Control Structures

### Conditionals (if-else)

```bash
# Basic if-else
if [ "$1" == "hello" ]; then
    echo "Hello to you too!"
elif [ "$1" == "bye" ]; then
    echo "Goodbye!"
else
    echo "I don't understand '$1'"
fi

# File tests
if [ -f "$1" ]; then
    echo "$1 is a regular file"
elif [ -d "$1" ]; then
    echo "$1 is a directory"
else
    echo "$1 does not exist"
fi
```

### Comparison Operators

For numeric comparisons:

- `-eq`: equal to
- `-ne`: not equal to
- `-lt`: less than
- `-le`: less than or equal to
- `-gt`: greater than
- `-ge`: greater than or equal to

For string comparisons:

- `=`: equal to
- `!=`: not equal to
- `-z`: string is empty
- `-n`: string is not empty

### File Test Operators

- `-e`: file exists
- `-f`: is a regular file
- `-d`: is a directory
- `-r`: is readable
- `-w`: is writable
- `-x`: is executable
- `-s`: file is not empty
- `-L`: is a symbolic link

## Loops

### For Loops

```bash
# Basic for loop
echo "Counting from 1 to 5:"
for i in 1 2 3 4 5; do
    echo "Number: $i"
done

# Range-based for loop
echo "Counting from 1 to 5 (using sequence):"
for i in $(seq 1 5); do
    echo "Number: $i"
done

# C-style for loop
echo "Counting from 0 to 4 (C-style):"
for ((i=0; i<5; i++)); do
    echo "Number: $i"
done

# Iterate over files
echo "Files in current directory:"
for file in *.sh; do
    echo "Script: $file"
done
```

### While Loops

```bash
# Basic while loop
count=1
echo "While loop counting to 5:"
while [ $count -le 5 ]; do
    echo "Count: $count"
    ((count++))
done

# Reading lines from a file
echo "Reading lines from file:"
while read line; do
    echo "Line: $line"
done < input.txt
```

### Until Loops

```bash
# Until loop (runs until condition becomes true)
count=1
echo "Until loop counting to 5:"
until [ $count -gt 5 ]; do
    echo "Count: $count"
    ((count++))
done
```

### Case Statements

```bash
echo -n "Enter a fruit name: "
read fruit

case "$fruit" in
    "apple")
        echo "Apple is red or green"
        ;;
    "banana")
        echo "Banana is yellow"
        ;;
    "orange")
        echo "Orange is orange"
        ;;
    *)
        echo "Unknown fruit"
        ;;
esac
```

## Functions

```bash
# Function definition
greet() {
    echo "Hello, $1!"
    local local_var="I'm local"  # Local variable
    echo "$local_var"
}

# Function with return value
add() {
    local result=$(($1 + $2))
    echo $result  # Output becomes the return value
}

# Call functions
greet "World"

sum=$(add 5 3)
echo "Sum: $sum"
```

## Working with Arrays

```bash
# Declare array
fruits=("apple" "banana" "orange" "grape")

# Access elements
echo "First fruit: ${fruits[0]}"
echo "All fruits: ${fruits[@]}"
echo "Number of fruits: ${#fruits[@]}"

# Iterate over array
for fruit in "${fruits[@]}"; do
    echo "Fruit: $fruit"
done

# Add element to array
fruits+=("mango")

# Delete element
unset fruits[1]

# Associative arrays (dictionaries)
declare -A user_info
user_info[name]="John"
user_info[age]=30
user_info[city]="New York"

echo "Name: ${user_info[name]}"
```

## String Operations

```bash
string="Hello, World!"

# Length
echo "Length: ${#string}"

# Substring (position, length)
echo "Substring: ${string:7:5}"  # "World"

# Replace
echo "Replace: ${string/World/Bash}"  # "Hello, Bash!"

# Replace all occurrences
echo "Replace all: ${string//l/L}"  # "HeLLo, World!"

# Uppercase/Lowercase
echo "Uppercase: ${string^^}"
echo "Lowercase: ${string,,}"
```

## Error Handling

```bash
# Exit on error
set -e  # Script will exit if any command fails

# Custom error handling
error_handler() {
    echo "Error occurred at line $1"
    exit 1
}

# Set trap for errors
trap 'error_handler $LINENO' ERR

# Check command success
if ! command -v git &> /dev/null; then
    echo "Git is not installed"
    exit 1
fi
```

## Special Variables

- `$0`: Script name
- `$1`, `$2`, etc.: Command-line arguments
- `$@`: All arguments
- `$#`: Number of arguments
- `$$`: Process ID
- `$?`: Exit status of last command

## Example: System Information Script

```bash
#!/bin/bash

echo "=============== System Information ==============="
echo "Hostname: $(hostname)"
echo "Kernel: $(uname -r)"
echo "Uptime: $(uptime -p)"
echo "CPU: $(grep 'model name' /proc/cpuinfo | head -1 | cut -d ':' -f2 | sed 's/^[ \t]*//')"
echo "Memory: $(free -h | grep Mem | awk '{print $2}')"
echo "Disk usage: $(df -h / | tail -1 | awk '{print $3 "/" $2 " (" $5 ")"}')"
echo "IP address: $(hostname -I | awk '{print $1}')"
echo "=================================================="
```

## Best Practices

1. **Always use the shebang line**: `#!/bin/bash`
2. **Use double quotes around variables**: `echo "$variable"`
3. **Use meaningful variable names**: `user_count` instead of `uc`
4. **Comment your code**
5. **Handle errors**
6. **Check command existence**: `command -v program >/dev/null 2>&1 || { echo "Program not found"; exit 1; }`
7. **Validate input parameters**
8. **Use functions for reusable code**
9. **Use consistent indentation**
10. **Use `-x` flag for debugging**: `bash -x script.sh`

## Tips and Tricks

- **Debug your script**: Add `set -x` to print commands as they execute
- **Safer scripts**: Add `set -e` to exit on error, `set -u` to error on undefined variables
- **Temporary files**: Use `mktemp` to create secure temporary files
- **Use || and && for conditional execution**: `mkdir dir || echo "Failed to create directory"`

## Further Reading

For more advanced bash scripting techniques, check out:

- The Bash man page: `man bash`
- [Advanced Bash-Scripting Guide](https://tldp.org/LDP/abs/html/)
- [Bash Hackers Wiki](https://wiki.bash-hackers.org/)
