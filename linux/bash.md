# Bash Scripting Notes

## **Basics**

### Shebang
```bash
#!/bin/bash
```

### Running Scripts
```bash
bash script.sh          # Run with bash
./script.sh             # Run directly (needs execute permission)
chmod +x script.sh      # Make executable
```

### Comments
```bash
# This is a comment
: ' This is a multi-line comment
   that spans multiple lines
'
```

---

## **Variables**

### Declaring Variables
```bash
name="John"
age=25
```

### Using Variables
```bash
echo $name
echo ${name}         # Preferred for clarity
echo "Hello $name"   # Double quotes allow variable expansion
echo 'Hello $name'   # Single quotes treat literally
```

### Special Variables
```bash
$0      # Script name
$1-$9   # Arguments passed to script
$#      # Number of arguments
$@      # All arguments as separate words
$*      # All arguments as single word
$?      # Exit status of last command
$$      # Process ID of current script
$!      # Process ID of last background command
```

### Environment Variables
```bash
export PATH="/usr/local/bin:$PATH"
echo $HOME
echo $USER
echo $PATH
```

---

## **Strings**

### String Operations
```bash
str="Hello World"

# Length
echo ${#str}              # 11

# Substring
echo ${str:0:5}           # Hello
echo ${str:6}             # World

# Replace
echo ${str/World/Bash}    # Hello Bash
echo ${str//l/L}          # HeLLo WorLd

# Check if string contains substring
if [[ $str == *"World"* ]]; then
    echo "Contains World"
fi
```

### String Concatenation
```bash
str1="Hello"
str2="World"
combined="$str1 $str2"    # Hello World
length=${#str1} # to get length of str1
```

---

## **Arrays**

### Indexed Arrays
```bash
# Declare
arr=("apple" "banana" "cherry")

# Access
echo ${arr[0]}            # apple
echo ${arr[@]}            # All elements
echo ${#arr[@]}           # Length

# Add element
arr[3]="date"
arr+=("elderberry")

# Loop through
for item in "${arr[@]}"; do
    echo $item
done
```

### Associative Arrays (Key-Value)
```bash
declare -A fruits
fruits=(["apple"]="red" ["banana"]="yellow")

echo ${fruits[apple]}     # red
echo ${!fruits[@]}        # All keys
echo ${fruits[@]}         # All values
```

---

## **Conditionals**

### If Statements
```bash
if [ condition ]; then
    # code
elif [ condition ]; then
    # code
else
    # code
fi
```

### Comparison Operators
```bash
# Numbers
-eq  # Equal
-ne  # Not equal
-gt  # Greater than
-ge  # Greater or equal
-lt  # Less than
-le  # Less or equal

# Strings
=   # Equal
!=  # Not equal
<   # Less than (lexicographic)
>   # Greater than (lexicographic)
-z  # Empty string
-n  # Not empty

# Files
-f  # Regular file
-d  # Directory
-e  # Exists
-r  # Readable
-w  # Writable
-x  # Executable
```

### Examples
```bash
# Number comparison
if [ $age -gt 18 ]; then
    echo "Adult"
fi

# String comparison
if [ "$name" = "John" ]; then
    echo "Hello John"
fi

# File check
if [ -f "file.txt" ]; then
    echo "File exists"
fi

# AND/OR
if [ $age -gt 18 ] && [ $age -lt 65 ]; then
    echo "Working age"
fi
```

---

## **Loops**

### For Loop
```bash
# Range
for i in {1..10}; do
    echo $i
done

# Array
for item in "${arr[@]}"; do
    echo $item
done

# Files
for file in *.txt; do
    echo $file
done

# C-style
for ((i=0; i<10; i++)); do
    echo $i
done
```

### While Loop
```bash
count=0
while [ $count -lt 5 ]; do
    echo $count
    ((count++))
done
```

### Until Loop
```bash
count=0
until [ $count -ge 5 ]; do
    echo $count
    ((count++))
done
```

### Break & Continue
```bash
for i in {1..10}; do
    if [ $i -eq 5 ]; then
        continue    # Skip 5
    fi
    if [ $i -eq 8 ]; then
        break       # Stop at 8
    fi
    echo $i
done
```

---

## **Functions**

### Defining Functions
```bash
function greet() {
    echo "Hello, $1!"
}

# Alternative syntax
greet() {
    echo "Hello, $1!"
}
```

### Calling Functions
```bash
greet "John"        # Hello, John!
greet $name
```

### Return Values
```bash
add() {
    echo $(($1 + $2))
}

result=$(add 5 3)
echo $result        # 8
```

### Return Status
```bash
check_file() {
    if [ -f "$1" ]; then
        return 0     # Success
    else
        return 1     # Failure
    fi
}

if check_file "file.txt"; then
    echo "File exists"
fi
```

---

## **Input/Output**

### Reading Input
```bash
echo "Enter your name:"
read name
echo "Hello, $name"

# Silent input (passwords)
read -s -p "Enter password: " password

# Read multiple values
read -p "Enter name age: " name age
```

### Command Line Arguments
```bash
#!/bin/bash
echo "Script name: $0"
echo "First arg: $1"
echo "Second arg: $2"
echo "All args: $@"
echo "Number of args: $#"
```

### Output
```bash
echo "Hello"              # Print to stdout
echo "Error" >&2          # Print to stderr
printf "Name: %s\n" "John" # Formatted output
```

---

## **Command Substitution**

### Backticks (Old style)
```bash
result=`command`
```

### $() (Preferred)
```bash
result=$(command)
files=$(ls *.txt)
count=$(wc -l < file.txt)
```

---

## **Arithmetic Operations**

### Basic Math
```bash
echo $((5 + 3))           # 8
echo $((10 - 4))          # 6
echo $((6 * 7))           # 42
echo $((20 / 4))          # 5
echo $((10 % 3))          # 1
```

### Variables
```bash
a=5
b=3
echo $((a + b))           # 8
((a++))                   # Increment
((a--))                   # Decrement
((a += 5))                # Add 5
```

### Comparison
```bash
if (( $a > $b )); then
    echo "a is greater"
fi
```

---

## **File Operations**

### Reading Files
```bash
# Line by line
while IFS= read -r line; do
    echo "$line"
done < file.txt

# All lines
content=$(cat file.txt)
echo "$content"
```

### Writing Files
```bash
echo "Hello" > file.txt           # Overwrite
echo "World" >> file.txt          # Append
```

### Checking Files
```bash
if [ -f "file.txt" ]; then
    echo "File exists"
fi

if [ -d "/path/to/dir" ]; then
    echo "Directory exists"
fi
```

---

## **Error Handling**

### Exit Codes
```bash
command
if [ $? -eq 0 ]; then
    echo "Success"
else
    echo "Failed"
fi
```

### Set Options
```bash
set -e          # Exit on error
set -u          # Error on undefined variable
set -o pipefail # Exit on pipe failure
set -x          # Debug mode (print commands)
```

### Trap Signals
```bash
trap 'echo "Cleaning up..."; rm -f /tmp/tempfile' EXIT
trap 'echo "Interrupted"; exit 1' INT
```

---

## **Debugging**

### Debug Mode
```bash
bash -x script.sh    # Debug mode
set -x               # Enable in script
set +x               # Disable in script
```

### Verbose Mode
```bash
bash -v script.sh    # Verbose mode
set -v               # Enable in script
```

---

## **Useful Commands**

### Check Syntax
```bash
bash -n script.sh    # Check syntax without running
```

### Profile Script
```bash
time bash script.sh  # Measure execution time
```

---

## **Best Practices**

1. Always use `#!/bin/bash` shebang
2. Quote variables: `"$var"` instead of `$var`
3. Use `[[ ]]` for complex conditions
4. Prefer `$()` over backticks
5. Use `set -e` to exit on errors
6. Add comments for complex logic
7. Use meaningful variable names
8. Check file existence before operations
9. Handle errors gracefully
10. Use functions for reusable code

---

## **Examples**

### Simple Backup Script
```bash
#!/bin/bash
set -e

SOURCE="/home/user/documents"
DEST="/backup/$(date +%Y%m%d)"
mkdir -p "$DEST"
rsync -av "$SOURCE/" "$DEST/"
echo "Backup completed to $DEST"
```

### Log Rotation
```bash
#!/bin/bash
LOG_FILE="/var/log/app.log"
MAX_SIZE=10485760  # 10MB

if [ -f "$LOG_FILE" ] && [ $(stat -f%z "$LOG_FILE") -gt $MAX_SIZE ]; then
    mv "$LOG_FILE" "${LOG_FILE}.old"
    touch "$LOG_FILE"
    echo "Log rotated"
fi
```

### Process Monitor
```bash
#!/bin/bash
PROCESS="nginx"
if pgrep -x "$PROCESS" > /dev/null; then
    echo "$PROCESS is running"
else
    echo "$PROCESS is not running"
    systemctl start nginx
fi
```
