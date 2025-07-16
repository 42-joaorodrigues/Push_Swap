# Push_swap

## 📘 Project Overview

**Push_swap** is a sorting algorithm project from the 42 curriculum. The goal is to sort data on a stack using a limited set of instructions with the lowest possible number of actions. This project teaches algorithm optimization, complexity analysis, and efficient data manipulation.

> **Disclaimer:**  
> This document is an unofficial summary written for educational and documentation purposes.  
> It is not affiliated with or endorsed by 42 or its partners.  
> All 42 students are responsible for adhering to the academic integrity policy.  
> You may **not** publish or share any part of the official subject PDF, evaluation scripts, or Moulinette content.

---

## Contents

- [Goals](#goals)
- [General Requirements](#general-requirements)
- [The Rules](#the-rules)
- [Operations](#operations)
- [Mandatory Part](#mandatory-part)
- [Bonus Part](#bonus-part)
- [Benchmark Requirements](#benchmark-requirements)
- [Submission Guidelines](#submission-guidelines)

---

## Goals

- Implement an efficient sorting algorithm using stack operations
- Learn about algorithm complexity and optimization
- Master various sorting techniques and choose the most appropriate solution
- Understand the trade-offs between different algorithmic approaches
- Practice rigorous C programming and memory management

---

## General Requirements

- Written in **C**, following the **42 Norm**
- No memory leaks, segmentation faults, or undefined behavior
- Use only allowed external functions: `read`, `write`, `malloc`, `free`, `exit`
- Can use `ft_printf` and any equivalent **YOU** coded
- **Libft** is authorized
- Global variables are **forbidden**
- Must include a **Makefile** with rules: `$(NAME)`, `all`, `clean`, `fclean`, `re`
- Compile with flags: `-Wall`, `-Wextra`, `-Werror`
- Use `cc` compiler

---

## The Rules

### Stack Setup
- You have **2 stacks** named `a` and `b`
- At the beginning:
  - Stack `a` contains a random amount of negative and/or positive numbers (no duplicates)
  - Stack `b` is empty
- **Goal**: Sort numbers in ascending order in stack `a` (smallest on top)

### Stack Representation
- Stacks grow from the right
- First argument should be at the top of stack `a`

---

## Operations

### Swap Operations
- `sa` (swap a): Swap the first 2 elements at the top of stack a
- `sb` (swap b): Swap the first 2 elements at the top of stack b  
- `ss`: Execute `sa` and `sb` at the same time

### Push Operations
- `pa` (push a): Take the first element at the top of b and put it at the top of a
- `pb` (push b): Take the first element at the top of a and put it at the top of b

### Rotate Operations
- `ra` (rotate a): Shift up all elements of stack a by 1 (first becomes last)
- `rb` (rotate b): Shift up all elements of stack b by 1 (first becomes last)
- `rr`: Execute `ra` and `rb` at the same time

### Reverse Rotate Operations
- `rra` (reverse rotate a): Shift down all elements of stack a by 1 (last becomes first)
- `rrb` (reverse rotate b): Shift down all elements of stack b by 1 (last becomes first)
- `rrr`: Execute `rra` and `rrb` at the same time

---

## Mandatory Part

### Program: `push_swap`

**Input**: List of integers as command line arguments  
**Output**: Smallest list of instructions to sort the stack

#### Requirements:
- Display the **minimum number of operations** needed to sort stack a
- Instructions must be separated by `\n` and nothing else
- If no parameters given, display nothing and return prompt
- On error, display `"Error"` followed by `\n` on **standard error**

#### Error Cases:
- Arguments that aren't integers
- Arguments bigger than an integer
- Duplicate numbers
- Invalid input format

#### Example:
```bash
$> ./push_swap 2 1 3 6 5 8
sa
pb
pb
pb
sa
pa
pa
pa

$> ./push_swap 0 one 2 3
Error
```

#### Verification:
Your program will be tested with a provided `checker_OS` binary:
```bash
$> ARG="4 67 3 87 23"; ./push_swap $ARG | wc -l
6
$> ARG="4 67 3 87 23"; ./push_swap $ARG | ./checker_OS $ARG
OK
```

---

## Bonus Part

### Program: `checker`

**Input**: List of integers + instructions from standard input  
**Output**: `"OK"` if sorted correctly, `"KO"` otherwise

#### Requirements:
- Takes stack a as command line arguments
- Reads instructions from **standard input** (each followed by `\n`)
- Executes instructions on the given stack
- Displays `"OK"` if stack a is sorted and stack b is empty
- Displays `"KO"` in any other case
- Displays `"Error"` on invalid input or instructions

#### Makefile Rule:
Must include a `bonus` rule for compilation

#### Example:
```bash
$> ./checker 3 2 1 0
rra
pb
sa
rra
pa
OK

$> ./checker 3 2 1 0
sa
rra
pb
KO
```

> **Note**: Bonus part will **only** be evaluated if mandatory part is **PERFECT**

---

## Benchmark Requirements

To validate the project, you must achieve specific performance targets:

### Minimum Validation (Grade 80):
- Sort **100 random numbers** in fewer than **700 operations**

### Maximum Validation (Bonus Eligible):
- Sort **100 random numbers** in fewer than **700 operations** AND
- Sort **500 random numbers** in fewer than **5500 operations**

> **Important**: All benchmarks must be passed to access bonus evaluation

---

## Submission Guidelines

- Submit to your assigned **Git repository**
- Only repository contents will be evaluated
- Evaluation includes **peer reviews** and possible **Deepthought** testing
- Double-check file names and structure
- Any error during Deepthought grading stops evaluation immediately

---

## Algorithm Strategies

While not specified in the subject, common approaches include:

- **Small stacks** (≤3 elements): Direct sorting
- **Medium stacks** (4-100 elements): Optimized insertion sort variants
- **Large stacks** (100+ elements): Radix sort, quicksort variations, or chunk-based algorithms

---

## Testing Recommendations

- Create comprehensive test suites for various input sizes
- Test edge cases: empty input, single element, already sorted, reverse sorted
- Verify operation counts meet benchmark requirements
- Test error handling thoroughly
- Use the provided `checker_OS` for verification

---

## Final Note

This project is an excellent introduction to **algorithm optimization** and **complexity analysis**. Success requires not just implementing a working solution, but understanding when and why different algorithms perform better under various conditions.

---
