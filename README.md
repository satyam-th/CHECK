
# DSA Practice Questions with C Examples

## Algorithm

### What is an algorithm?
A step-by-step set of operations to be performed to solve a problem.

### Features of an Algorithm
- Input/Output
- Finiteness
- Definiteness
- Effectiveness

### Characteristics of Algorithms
Same as features above with more emphasis on correctness and generality.

### Why Know DS & Algorithms?
Data structures and algorithms allow us to write efficient, optimal, and scalable programs.

### Array as an ADT
- Fixed-size, homogeneous elements in contiguous memory
- Supports access via index, insertion, deletion, traversal

### Time & Space Complexity
Time: Measure steps as a function of input size  
Space: Memory consumed during execution

### Serial vs Parallel Algorithms

| Feature | Serial | Parallel |
|--------|--------|----------|
| Execution | One step at a time | Multiple steps simultaneously |
| Speed | Slower | Faster for large tasks |
| Example | For loop sum | Multi-threaded sum |

---

## Stack

### Stack ADT (LIFO)

#### Operations:
- push
- pop
- peek
- isEmpty

#### C Example:
```c
#define MAX 100
int stack[MAX], top = -1;

void push(int x) { stack[++top] = x; }
int pop() { return stack[top--]; }
int peek() { return stack[top]; }
```

### Infix to Postfix Algorithm
Use stack to manage operator precedence and convert infix into postfix.

### Infix to Prefix Algorithm
1. Reverse infix
2. Convert to postfix
3. Reverse output

### Example: `A + (B - C) * (D - E) + F / G ^ (H - I)`
Postfix: `A B C - D E - * + F G H I - ^ / +`  
Prefix: `+ + A * - B C - D E / F ^ G - H I`

### Postfix Evaluation (C):
```c
int evaluatePostfix(char* exp) {
    int stack[100], top = -1;
    for (int i = 0; exp[i]; i++) {
        if (isdigit(exp[i])) stack[++top] = exp[i] - '0';
        else {
            int b = stack[top--], a = stack[top--];
            if (exp[i] == '+') stack[++top] = a + b;
            if (exp[i] == '-') stack[++top] = a - b;
            if (exp[i] == '*') stack[++top] = a * b;
            if (exp[i] == '/') stack[++top] = a / b;
        }
    }
    return stack[top];
}
```

---

## Recursion

### What is Recursion?
A function calling itself to solve smaller sub-problems.

### C Examples
```c
int factorial(int n) {
    return (n == 0) ? 1 : n * factorial(n - 1);
}

int fibonacci(int n) {
    return (n <= 1) ? n : fibonacci(n-1) + fibonacci(n-2);
}
```

### Tower of Hanoi Algorithm
```c
void hanoi(int n, char from, char to, char aux) {
    if (n == 1) {
        printf("Move disk 1 from %c to %c\n", from, to);
        return;
    }
    hanoi(n-1, from, aux, to);
    printf("Move disk %d from %c to %c\n", n, from, to);
    hanoi(n-1, aux, to, from);
}
```

### Recursion: Merits & Demerits
- +: Simple, elegant, solves divide-and-conquer problems
- -: High memory, slower than iterative

---

## Queue

### Queue ADT
Linear structure (FIFO).

### C Linear Queue
```c
int queue[MAX], front = -1, rear = -1;

void enqueue(int val) {
    if (rear == MAX-1) return;
    if (front == -1) front = 0;
    queue[++rear] = val;
}

int dequeue() {
    if (front == -1 || front > rear) return -1;
    return queue[front++];
}
```

### Circular Queue Algorithm
Use `%MAX` to wrap around the ends

### Priority Queue
Items are ordered by priority, not insertion order. Can be implemented using arrays, heaps.

---

## Linked List

### Benefits over Array
- Dynamic size
- Efficient insertions/deletions

### SLL Insertion at Specific Position
```c
void insertAtPos(int pos, int data) {
    Node* temp = malloc(sizeof(Node));
    temp->data = data;
    if (pos == 1) {
        temp->next = head;
        head = temp;
        return;
    }
    Node* current = head;
    for (int i = 1; i < pos - 1 && current; i++) current = current->next;
    if (!current) return;
    temp->next = current->next;
    current->next = temp;
}
```

### Types:
| Type | Description |
|------|-------------|
| SLL | Single pointer per node |
| DLL | Two pointers (prev/next) |
| CLL | Last node points to head |
| DCLL | DLL + circular link |

### DLL Structure
```c
typedef struct Node {
    int data;
    struct Node* prev, *next;
} Node;
```

### Inserting at Beginning in SLL
```c
void insertBeginning(int data) {
    Node* newNode = malloc(sizeof(Node));
    newNode->data = data;
    newNode->next = head;
    head = newNode;
}
```

### Deleting Specific Node
```c
void deleteNode(int key) {
    Node* temp = head, *prev = NULL;
    if (temp && temp->data == key) {
        head = temp->next;
        free(temp);
        return;
    }
    while (temp && temp->data != key) {
        prev = temp;
        temp = temp->next;
    }
    if (!temp) return;
    prev->next = temp->next;
    free(temp);
}
```

---
