
# Beginner's Guide to Structured Text (ST)

Welcome to the **Beginner's Guide to Structured Text (ST)**!  
Structured Text is a high-level programming language used in industrial automation. It is one of the five programming languages defined by the IEC 61131-3 standard for programmable logic controllers (PLCs). If you have experience with languages like Pascal or C, you'll find ST familiar and powerful for controlling industrial systems.

---

## What is Structured Text?

Structured Text (ST) is a text-based programming language used in PLCs. It is known for its:
- High readability and maintainability
- Structured and organized syntax
- Ability to perform complex calculations and data processing
- Support for control structures like IF-THEN-ELSE, CASE, FOR, WHILE, and REPEAT loops
- Use of functions and function blocks for modular code

ST is widely used in industrial automation for tasks like:
- Process control and monitoring
- Machine automation
- Data handling and communication

---

## Basic Syntax

### Variables
Variables are used to store data. In ST, you need to declare variables before using them.

```pascal
VAR
    VariableName : DataType;
END_VAR;
```

Example:
```pascal
VAR
    Counter : INT;
    Temperature : REAL;
    Status : BOOL;
END_VAR;
```

### Data Types
Common data types in ST include:
- **BOOL**: Boolean (TRUE or FALSE)
- **INT**: Integer
- **REAL**: Floating point number
- **STRING**: Text
- **ARRAY**: Array of values
- **STRUCT**: Custom structure

Example:
```pascal
VAR
    Name : STRING[20];
    Readings : ARRAY[1..10] OF REAL;
    Product : STRUCT
        ID : INT;
        Price : REAL;
    END_STRUCT;
END_VAR;
```

### Expressions and Operators
You can perform calculations and comparisons using operators:
- **Arithmetic**: `+`, `-`, `*`, `/`, `MOD`
- **Comparison**: `=`, `<>`, `<`, `>`, `<=`, `>=`
- **Logical**: `AND`, `OR`, `NOT`

Example:
```pascal
VAR
    A, B, C : INT;
    Result : BOOL;
END_VAR;

A := 10;
B := 20;
C := A + B;          // Arithmetic
Result := C > 15;    // Comparison
```

---

## Control Structures

### IF-THEN-ELSE
Conditional branching using `IF-THEN-ELSE` statements.

```pascal
IF Condition THEN
    // Code when condition is TRUE
ELSE
    // Code when condition is FALSE
END_IF;
```

Example:
```pascal
IF Temperature > 50.0 THEN
    Status := TRUE;
ELSE
    Status := FALSE;
END_IF;
```

### CASE
Selects one block of code to execute from multiple options.

```pascal
CASE Variable OF
    Value1: // Code for Value1;
    Value2: // Code for Value2;
    Value3: // Code for Value3;
ELSE
    // Default code
END_CASE;
```

Example:
```pascal
CASE Mode OF
    0: Motor := OFF;
    1: Motor := FORWARD;
    2: Motor := REVERSE;
ELSE
    Motor := OFF;
END_CASE;
```

### FOR Loop
Repeats a block of code a specific number of times.

```pascal
FOR Variable := Start TO End BY Step DO
    // Code to repeat
END_FOR;
```

Example:
```pascal
FOR i := 1 TO 10 DO
    Sum := Sum + i;
END_FOR;
```

### WHILE Loop
Repeats a block of code while a condition is TRUE.

```pascal
WHILE Condition DO
    // Code to repeat
END_WHILE;
```

Example:
```pascal
WHILE Counter < 10 DO
    Counter := Counter + 1;
END_WHILE;
```

### REPEAT Loop
Repeats a block of code until a condition becomes TRUE.

```pascal
REPEAT
    // Code to repeat
UNTIL Condition
END_REPEAT;
```

Example:
```pascal
REPEAT
    Counter := Counter + 1;
UNTIL Counter >= 10
END_REPEAT;
```

---

## Functions and Function Blocks

### Functions
A function is a reusable block of code that returns a single value.

```pascal
FUNCTION FunctionName : ReturnType
VAR_INPUT
    Input1 : DataType;
    Input2 : DataType;
END_VAR;

    // Function logic
    FunctionName := Input1 + Input2;

END_FUNCTION;
```

Example:
```pascal
FUNCTION AddNumbers : INT
VAR_INPUT
    A, B : INT;
END_VAR;

    AddNumbers := A + B;

END_FUNCTION;
```

### Function Blocks
A function block is a reusable block of code that maintains its state.

```pascal
FUNCTION_BLOCK FunctionBlockName
VAR
    InternalVariable : DataType;
END_VAR;

    // Function Block logic

END_FUNCTION_BLOCK;
```

Example:
```pascal
FUNCTION_BLOCK CounterBlock
VAR
    Count : INT;
END_VAR;

    Count := Count + 1;

END_FUNCTION_BLOCK;
```

---

## Examples

### Example 1: Simple Motor Control
```pascal
VAR
    StartButton, StopButton : BOOL;
    Motor : BOOL;
END_VAR;

IF StartButton THEN
    Motor := TRUE;
ELSIF StopButton THEN
    Motor := FALSE;
END_IF;
```

### Example 2: Temperature Monitoring with Alarm
```pascal
VAR
    Temperature : REAL;
    Alarm : BOOL;
END_VAR;

IF Temperature > 100.0 THEN
    Alarm := TRUE;
ELSE
    Alarm := FALSE;
END_IF;
```

### Example 3: Counter with FOR Loop
```pascal
VAR
    i, Sum : INT;
END_VAR;

Sum := 0;
FOR i := 1 TO 10 DO
    Sum := Sum + i;
END_FOR;
```

---

## Best Practices

- Use meaningful variable names for better readability.
- Keep the code modular by using functions and function blocks.
- Comment your code to explain complex logic.
- Follow consistent naming conventions and indentation.

---

## Continue!

- Practice writing small programs using basic and advanced control structures.
- Explore advanced topics like communication protocols and hardware interfaces.
- Experiment with complex examples and real-world use cases.

---

## Additional Resources

- [IEC 61131-3 Standard Documentation](https://webstore.iec.ch/publication/4552)
- [PLC Open - Structured Text Overview](https://www.plcopen.org/)
