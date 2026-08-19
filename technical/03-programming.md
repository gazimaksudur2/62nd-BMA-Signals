# Programming & Core Concepts — Technical Study Notes

> **Why it is asked:** C programs appear in every 54th–55th BMA paper (Fibonacci, case conversion, factorial, sort, GCD). OOP and Kernel are confirmed short-note topics. Structures, tokens, and pointers are listed in 36th and 55th papers.

---

## 1. OOP — Object-Oriented Programming

OOP organises software around objects (data + behaviour) rather than functions.

### Four pillars

| Pillar | Definition | C++ example |
|---|---|---|
| **Encapsulation** | Bundling data (attributes) and methods (functions) into a class, and restricting direct access via access modifiers | `private` data with `public` getter/setter |
| **Abstraction** | Exposing only essential details; hiding implementation | Abstract class / interface |
| **Inheritance** | A derived class acquires attributes and methods from a base class | `class Dog : public Animal {}` |
| **Polymorphism** | Same interface, different behaviour — function overloading (compile-time) and virtual functions (run-time) | `area()` works differently for `Circle` and `Rectangle` |

### Class vs Object

- **Class:** A blueprint/template defining attributes and methods. (Concept, no memory.)
- **Object:** A specific instance of a class that exists in memory. (Real, has memory.)

---

## 2. Kernel

**Definition:** The kernel is the core of an operating system that manages communication between hardware and software. It runs in **kernel mode** (privileged) and has direct hardware access.

**Functions:**
- **Process management:** creating, scheduling, and terminating processes
- **Memory management:** allocating and freeing RAM; virtual memory
- **Device management:** communicating with hardware via device drivers
- **File system management:** reading/writing files; access control
- **System calls:** interface between user programs and the kernel

**User mode vs Kernel mode:**

| Mode | Privilege | Who runs here |
|---|---|---|
| User mode | Restricted | Applications, user programs |
| Kernel mode | Full hardware access | OS kernel, device drivers |

A process requests OS services via **system calls** (e.g. `read()`, `write()`, `fork()`), which switch the CPU from user mode to kernel mode and back.

---

## 3. C Tokens

A **token** is the smallest meaningful element in a C program. Six types:

| Token type | Description | Examples |
|---|---|---|
| **Keywords** | Reserved words with fixed meaning | `int`, `if`, `while`, `return`, `void` |
| **Identifiers** | Names for variables, functions, arrays | `count`, `main`, `result` |
| **Constants** | Fixed values that do not change | `100`, `3.14`, `'A'`, `"hello"` |
| **String literals** | Sequence of characters in double quotes | `"Hello, World!"` |
| **Operators** | Symbols that perform operations | `+`, `-`, `*`, `=`, `==`, `&&` |
| **Special symbols** | Punctuation used in program structure | `{`, `}`, `;`, `(`, `)`, `[`, `]` |

---

## 4. Structures and Arrays

### Structure
A user-defined data type that groups related variables of different types.

```c
struct Student {
    int  id;
    char name[50];
    float cgpa;
};

struct Student s1;
s1.id   = 101;
s1.cgpa = 3.75;
```

### Array
A collection of elements of the **same type** stored in contiguous memory.

```c
int marks[5] = {80, 90, 75, 88, 95};
printf("%d", marks[2]);  /* outputs 75 */
```

**Representation in memory:**
```
marks[0]  marks[1]  marks[2]  marks[3]  marks[4]
  80        90        75        88        95
 addr      addr+4    addr+8   addr+12   addr+16
```

---

## 5. Pointers

A **pointer** is a variable that stores the memory address of another variable.

```c
int  x   = 10;
int *ptr = &x;   /* ptr holds the address of x */

printf("%d", *ptr);  /* 10 — dereference: get value at address */
printf("%p", ptr);   /* address of x, e.g. 0x7ffee4b2 */
```

**Key operators:**
- `&` — address-of operator (gives address of a variable)
- `*` — dereference operator (gives value at an address)

**Why pointers matter:**
- Dynamic memory allocation (`malloc`, `free`)
- Passing large structures by reference (efficient)
- Building linked lists, trees

---

## 6. C Programs (Exam-ready)

> All programs use standard ISO C (no `conio.h`, no `clrscr()`). `int main(void)` is correct; `void main()` is non-standard.

### 6.1 Factorial using Recursion

```c
#include <stdio.h>

int factorial(int n) {
    if (n <= 1)
        return 1;
    return n * factorial(n - 1);
}

int main(void) {
    int num;
    printf("Enter a positive integer: ");
    scanf("%d", &num);
    printf("Factorial of %d = %d\n", num, factorial(num));
    return 0;
}
```

**How recursion works for n=4:**  
`factorial(4)` → `4 * factorial(3)` → `4 * 3 * factorial(2)` → `4 * 3 * 2 * factorial(1)` → `4 * 3 * 2 * 1 = 24`

---

### 6.2 Fibonacci Series

```c
#include <stdio.h>

int main(void) {
    int n, a = 0, b = 1, next;
    printf("Enter number of terms: ");
    scanf("%d", &n);
    printf("Fibonacci: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", a);
        next = a + b;
        a = b;
        b = next;
    }
    printf("\n");
    return 0;
}
```

Sample output for n=7: `0 1 1 2 3 5 8`

---

### 6.3 Lowercase to Uppercase (Convert a String)

```c
#include <stdio.h>

int main(void) {
    char str[100];
    printf("Enter string: ");
    scanf("%s", str);
    for (int i = 0; str[i] != '\0'; i++) {
        if (str[i] >= 'a' && str[i] <= 'z')
            str[i] = str[i] - 32;  /* 'a' - 'A' = 32 in ASCII */
    }
    printf("Uppercase: %s\n", str);
    return 0;
}
```

---

### 6.4 GCD using Euclid's Subtraction Method

*(This is the exact algorithm from the source file's MCQ — the answer is GCD.)*

```c
#include <stdio.h>

int main(void) {
    int x, y;
    printf("Enter two positive integers: ");
    scanf("%d %d", &x, &y);
    int m = x, n = y;
    while (m != n) {
        if (m > n) m = m - n;
        else       n = n - m;
    }
    printf("GCD = %d\n", m);
    return 0;
}
```

---

### 6.5 Bubble Sort (Sort 4 Items)

```c
#include <stdio.h>

int main(void) {
    int arr[4], n = 4;
    printf("Enter 4 integers: ");
    for (int i = 0; i < n; i++)
        scanf("%d", &arr[i]);

    /* Bubble sort */
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - 1 - i; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp   = arr[j];
                arr[j]     = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }

    printf("Sorted: ");
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    printf("\n");
    return 0;
}
```

---

## Q&A Bank

### True / False

**T1.** In C, `void main()` is the standard entry point.  
→ **False** (`int main(void)` or `int main(int argc, char *argv[])` is the ISO C standard.)

**T2.** The kernel runs in a privileged mode with full hardware access.  
→ **True**

**T3.** Inheritance is one of the four pillars of OOP.  
→ **True**

**T4.** A pointer variable stores the value of another variable.  
→ **False** (A pointer stores the *address* of another variable.)

**T5.** In the Fibonacci series, each term is the sum of the two preceding terms.  
→ **True**

**T6.** A keyword can be used as an identifier in C.  
→ **False** (Keywords are reserved and cannot be used as identifiers.)

---

### MCQ

**Q1.** Which of the following is NOT a token in C?  
(a) Keyword  (b) Identifier  (c) Comment  (d) Operator  
→ **(c)** Comment (comments are stripped by the preprocessor; they are not tokens.)

**Q2.** What does the `&` operator do in C?  
(a) Performs bitwise AND  (b) Returns the address of a variable  (c) Dereferences a pointer  (d) Logical AND  
→ **(b)** when used as a unary prefix operator, `&` returns the address of a variable.  
*(Note: as a binary operator it performs bitwise AND; context determines meaning.)*

**Q3.** Which OOP concept allows a class to use properties of another class?  
(a) Encapsulation  (b) Polymorphism  (c) Inheritance  (d) Abstraction  
→ **(c)** Inheritance

**Q4.** The first two terms of the Fibonacci series are:  
(a) 1, 1  (b) 0, 0  (c) 0, 1  (d) 1, 2  
→ **(c)** 0, 1 (standard definition; series: 0, 1, 1, 2, 3, 5, 8 …)

**Q5.** What is the kernel?  
(a) A user application  (b) The core of the OS managing hardware  (c) A type of file system  (d) A network protocol  
→ **(b)**

---

### Descriptive Q&A

**Q.** What is a Kernel? Explain its functions. (10 marks)

**A.**  
The **kernel** is the central component of an operating system. It is the first program loaded after the bootloader and remains in memory throughout the system's operation. It acts as a bridge between hardware and software, running in **kernel mode** with unrestricted access to CPU and memory.

**Core functions:**
1. **Process management:** Creates, schedules (CPU time allocation), suspends, and terminates processes. Uses scheduling algorithms (Round Robin, Priority).
2. **Memory management:** Allocates and de-allocates RAM; implements virtual memory (swapping); protects processes from each other.
3. **Device management:** Communicates with hardware devices via device drivers; manages I/O operations.
4. **File system management:** Provides a file abstraction over storage; manages read/write permissions and directory structure.
5. **System calls:** Provides a controlled interface through which user programs can request kernel services (e.g. `open()`, `read()`, `write()`, `fork()`).

**User mode vs Kernel mode:**  
User applications run in **user mode** with limited privileges. When a system call is made, the CPU switches to **kernel mode**, executes the privileged operation, then returns to user mode. This separation prevents user programs from accidentally (or maliciously) corrupting system state.

---

**Q.** What is OOP? Explain its four fundamental principles. (10 marks)

**A.**  
**Object-Oriented Programming (OOP)** is a programming paradigm that organises code around *objects* — entities combining **data** (attributes) and **behaviour** (methods). It mirrors real-world modelling and improves code reusability, maintainability, and modularity.

**Four principles:**

1. **Encapsulation:** Wrapping data and the functions that operate on it into a single unit (class), and controlling access using access modifiers (`private`, `public`, `protected`). Prevents external code from directly modifying internal state.  
   *Example:* A `BankAccount` class keeps `balance` private; only `deposit()` and `withdraw()` can change it.

2. **Abstraction:** Showing only necessary details and hiding implementation complexity. A user uses a method without knowing how it works internally.  
   *Example:* `sort()` — you call it without knowing whether it uses quicksort or merge sort.

3. **Inheritance:** A derived (child) class inherits attributes and methods from a base (parent) class, enabling code reuse and hierarchical relationships.  
   *Example:* `Vehicle` (parent) has `speed` and `fuel`; `Car` (child) inherits these and adds `numberOfDoors`.

4. **Polymorphism:** The same interface (method name) behaves differently depending on the object or input. Two types:
   - *Compile-time (overloading):* Multiple methods with same name but different parameters.
   - *Run-time (overriding):* Derived class overrides a base class method using virtual functions.

---

### Common Traps

| Misconception | Correction |
|---|---|
| `clrscr()` is standard C | It is a Turbo C extension — do not use in exam code |
| `void main()` is fine | Standard is `int main(void)` |
| Fibonacci starts at 1, 1 | Standard definition starts at **0, 1** |
| `&arr[0]` and `arr` are always identical | They are conceptually the same (base address) but their pointer types differ in C (`int *` vs `int (*)[n]`). For exam purposes they are the same. |
