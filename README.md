
# Data Structures and Algorithms Q&A (with C Examples)

## Algorithm

### What is an algorithm?
An **algorithm** is a step-by-step procedure for solving a problem or performing a task. It takes input, processes it, and produces output.

---

### Major Characteristics of Algorithms
- **Input**: Zero or more inputs
- **Output**: At least one output
- **Finiteness**: Ends after finite steps
- **Definiteness**: Clear and unambiguous
- **Effectiveness**: Feasible with basic tools
- **Correctness**: Produces correct output
- **Generality**: Applies to all relevant inputs

---

### Features of Algorithms
- Clear input/output
- Language independent
- Finite steps
- Feasible and efficient

---

### Why Learn DS & Algorithms?
- Optimized resource use
- Faster execution
- Better scalability

---

### Time & Space Complexity

#### Time Complexity
- **Big-O (Worst case)**
- **Omega (Best case)**
- **Theta (Average case)**

Steps:
1. Count operations
2. Drop constants/lower terms
3. Express in Big-O

#### Space Complexity
- Memory usage during execution

---

## Stack

### Stack ADT (LIFO)
#### Operations:
- `push(x)`
- `pop()`
- `peek()`
- `isEmpty()`

#### C Example:
```c
#define MAX 100
int stack[MAX], top = -1;

void push(int x) {
    if (top == MAX-1) return;
    stack[++top] = x;
}

int pop() {
    return (top == -1) ? -1 : stack[top--];
}

int peek() {
    return (top == -1) ? -1 : stack[top];
}
```

---

## Expression Conversion

### Infix to Postfix (C)
```c
#include <stdio.h>
#include <ctype.h>

int precedence(char op) {
    if (op == '^') return 3;
    if (op == '*' || op == '/' || op == '%') return 2;
    if (op == '+' || op == '-') return 1;
    return 0;
}
```

---

### Infix to Prefix (Steps)
1. Reverse infix
2. Convert to postfix
3. Reverse result

---

### Postfix Evaluation (C)
```c
int evaluatePostfix(char* exp) {
    int stack[100], top = -1;
    for (int i = 0; exp[i]; i++) {
        if (isdigit(exp[i])) {
            stack[++top] = exp[i] - '0';
        } else {
            int b = stack[top--];
            int a = stack[top--];
            switch (exp[i]) {
                case '+': stack[++top] = a + b; break;
                case '-': stack[++top] = a - b; break;
                case '*': stack[++top] = a * b; break;
                case '/': stack[++top] = a / b; break;
            }
        }
    }
    return stack[top];
}
```

---

## Recursion

### What is Recursion?
Function calling itself

---

### Factorial (C)
```c
int factorial(int n) {
    if (n == 0) return 1;
    return n * factorial(n - 1);
}
```

---

### Fibonacci (C)
```c
int fibonacci(int n) {
    if (n <= 1) return n;
    return fibonacci(n-1) + fibonacci(n-2);
}
```

---

## Notes
- Postfix evaluation is stack-based
- Prefix uses reverse logic of postfix
- Recursion must have base case
