# Learning Dependecies

### Key Takeaways
- **Bourne Again Shell**: 
- **Conditional Execution**: 
- **Arguments, Variables and Arrays**:
- **Comparison Operators**:
- **Arithmetic**:
- **Input and Output Control**:
- **Flow Control - Loops**:
- **PFlow Control - Branches**:
- **Functions**:
- **Debugging**:

### Reflections

## 21st March 2025
## Bourne Again Shell

1. Understanding Bash and Its Importance
- Bash is a scripting language used to communicate with Unix-based OS.
- Since May 2019, Windows Subsystem for Linux (WSL) allows Bash usage on Windows.
- Unlike programming languages, scripting does not require compilation before execution.
- Mastering Bash is crucial for efficient work, especially in privilege escalation.
2. Importance of Bash for Penetration Testers
- Pentesters must be comfortable with both Windows and Unix-based systems.
- In Unix-based networks, filtering and automating processes help manage large amounts of data.
- Combining multiple commands and working with their outputs enhances efficiency.
- Scripting automates repetitive tasks and speeds up information gathering.

## 26th March 2025 
## Conditional execution 
lets scripts make decisions based on conditions. This allows more flexible and dynamic behaviour than simply running commands in order.

- Executes different code blocks depending on conditions.
- Skips other blocks once a matching condition is found.
- Resumes execution after the conditional block ends.

**Main Components:**

1. **Shebang (`#!/bin/bash`)**:
    
    Tells the system which interpreter to use to run the script (e.g., Bash, Python).
    
2. **If-Else-Fi syntax**:
    
    Used to check and react to conditions:
    
    ```bash
    bash
    CopyEdit
    if [ condition ]; then
      # code
    elif [ other_condition ]; then
      # code
    else
      # fallback code
    fi
    
    ```
    
3. **Special Variables**:
    - `$#` — Number of arguments passed to the script.
    - `$0` — Script name.
    - `$1`, `$2` — Argument values.

## 🔹 **Examples:**

## 🧪 Basic `if`:

```bash
bash
CopyEdit
if [ $# -eq 0 ]; then
  echo "No arguments provided"
  exit 1
fi

```

## With `else`:

```bash
bash
CopyEdit
if [ $value -gt 10 ]; then
  echo "Greater than 10"
else
  echo "Less or equal to 10"
fi

```

### 🧪 With `elif`:

```bash
bash
CopyEdit
if [ $value -gt 10 ]; then
  echo "Greater"
elif [ $value -lt 10 ]; then
  echo "Smaller"
else
  echo "Equal or invalid"
fi

```

## **Extended Example in Context:**

Script checks the number of arguments:

- If none → ask for domain input and exit.
- If one → assign to `domain`.
- If more than one → error message and exit.

## **Usage in Loops:**

Conditional logic can also be used *inside loops* to trigger actions based on iteration count or variable values.


## Exercises done:
1. Conditional Execution: Create an "If-Else" condition in the "For"-Loop of the "Exercise Script" that prints you the number of characters of the 35th generated value of the variable "var". Submit the number as the answer.

```
#!/bin/bash

# Variable to encode
var="nef892na9s1p9asn2aJs71nIsm"

for counter in {1..35}
do
	var=$(echo $var | base64)

	if [ $counter -eq 35 ];then
		echo $var | wc -c
	fi
done
```


 


