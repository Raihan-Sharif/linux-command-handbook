# Bash Scripting Basics

Bash (Bourne Again SHell) scripting allows you to automate tasks and create powerful workflows in Linux. This guide covers the fundamentals of bash scripting for beginners to intermediate users.

## Getting Started

### Creating Your First Script

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
#!/bin/bash

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
#!/bin/bash

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
#!/bin/bash

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
#!/bin/bash

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

```bash
#!/bin/bash

# Numeric comparisons
a=10
b=20

if [ $a -eq $b ]; then echo "a equals b"; fi
if [ $a -ne $b ]; then echo "a not equals b"; fi
if [ $a -lt $b ]; then echo "a less than b"; fi
if [ $a -le $b ]; then echo "a less than or equal to b"; fi
if [ $a -gt $b ]; then echo "a greater than b"; fi
if [ $a -ge $b ]; then echo "a greater than or equal to b"; fi

# String comparisons
str1="hello"
str2="world"

if [ "$str1" = "$str2" ]; then echo "Strings are equal"; fi
if [ "$str1" != "$str2" ]; then echo "Strings are not equal"; fi
if [ -z "$str1" ]; then echo "String is empty"; fi
if [ -n "$str1" ]; then echo "String is not empty"; fi
```

### File Test Operators

```bash
#!/bin/bash

file=$1

# File operations
if [ -e "$file" ]; then echo "File exists"; fi
if [ -f "$file" ]; then echo "Is a regular file"; fi
if [ -d "$file" ]; then echo "Is a directory"; fi
if [ -r "$file" ]; then echo "Is readable"; fi
if [ -w "$file" ]; then echo "Is writable"; fi
if [ -x "$file" ]; then echo "Is executable"; fi
if [ -s "$file" ]; then echo "File is not empty"; fi
if [ -L "$file" ]; then echo "Is a symbolic link"; fi
```

### Loops

#### For Loops

```bash
#!/bin/bash

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

#### While Loops

```bash
#!/bin/bash

# Basic while loop
count=1
echo "While loop counting to 5:"
while [ $count -le 5 ]; do
    echo "Count: $count"
    ((count++))
done

# Read lines from a file
echo "Reading lines from file:"
while read line; do
    echo "Line: $line"
done < input.txt

# Process output of a command
echo "Users on the system:"
who | while read user tty login_time; do
    echo "User: $user, Terminal: $tty"
done
```

#### Until Loops

```bash
#!/bin/bash

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
#!/bin/bash

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
#!/bin/bash

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
    # Or use return for small integers only (0-255)
    return $result
}

# Call functions
greet "World"

sum=$(add 5 3)
echo "Sum: $sum"

add 10 20
echo "Return status: $?"  # Gets the return value
```

## Working with Arrays

```bash
#!/bin/bash

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

# Iterate over keys
for key in "${!user_info[@]}"; do
    echo "$key: ${user_info[$key]}"
done
```

## String Operations

```bash
#!/bin/bash

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

# Strip prefix/suffix
echo "Strip prefix: ${string#Hello, }"  # "World!"
echo "Strip suffix: ${string%World!}"   # "Hello, "
```

## Error Handling

```bash
#!/bin/bash

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

# Check exit status
grep "pattern" file.txt
if [ $? -ne 0 ]; then
    echo "Pattern not found"
fi

# Set default values
filename=${1:-"default.txt"}
```

## Special Variables

```bash
#!/bin/bash

echo "Script name: $0"
echo "First argument: $1"
echo "Second argument: $2"
echo "All arguments: $@"
echo "Number of arguments: $#"
echo "Process ID: $$"
echo "Last command exit status: $?"
```

## Example Scripts

### System Information Script

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

### Backup Script

```bash
#!/bin/bash

# Configuration
backup_dir="/backup"
source_dir="/var/www"
date_format=$(date +%Y-%m-%d_%H-%M-%S)
backup_file="${backup_dir}/backup_${date_format}.tar.gz"

# Check backup directory
if [ ! -d "$backup_dir" ]; then
    mkdir -p "$backup_dir"
    if [ $? -ne 0 ]; then
        echo "Error: Could not create backup directory"
        exit 1
    fi
fi

# Create backup
echo "Creating backup of $source_dir..."
tar -czf "$backup_file" "$source_dir" 2>/dev/null

# Check if backup was successful
if [ $? -eq 0 ]; then
    echo "Backup created successfully: $backup_file"
    echo "Size: $(du -h "$backup_file" | cut -f1)"
else
    echo "Error: Backup failed"
    exit 1
fi

# Clean old backups (keep last 5)
cd "$backup_dir" || exit
ls -1t | grep "^backup_.*\.tar\.gz$" | tail -n +6 | xargs -r rm
echo "Old backups cleaned up"
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

- **Debug your script**: Add `set -x` to print commands and their arguments as they execute
- **Safer scripts**: Add `set -e` to exit on error, `set -u` to error on undefined variables
- **Temporary files**: Use `mktemp` to create secure temporary files
- **Check script syntax**: Use `bash -n script.sh`
- **Use || and && for conditional execution**: `mkdir dir || echo "Failed to create directory"`
