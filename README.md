# COMP2100
**just some revision for comp2100 (2025) - all of this ai generated**

# COMP2100 Systems Programming - Complete Revision Guide
## Macquarie University Final Exam Preparation

---

## **WEEK 1: From Java to C**

### Key Concepts
- **Transition from Java to C**
  - No classes or objects
  - Manual memory management
  - Pointers instead of references
  - Header files (.h) and implementation files (.c)
  - No garbage collection

### C Program Structure
```c
#include <stdio.h>    // Preprocessor directive
#include <stdlib.h>

int main(int argc, char *argv[]) {
    // argc: argument count
    // argv: argument vector (array of strings)
    printf("Hello World\n");
    return 0;  // Return to OS
}
```

### Compilation Process
1. **Preprocessing**: Handle #include, #define
2. **Compilation**: C code → Assembly
3. **Assembly**: Assembly → Object code (.o)
4. **Linking**: Combine object files → Executable

### GCC Commands
```bash
gcc program.c -o program        # Compile and link
gcc -c program.c                # Compile only (create .o)
gcc -Wall program.c             # Show all warnings
gcc -g program.c                # Include debugging symbols
```

---

## **WEEK 2: C Basics and File I/O**

### Data Types
- **Integer types**: char (1 byte), short (2), int (4), long (8)
- **Floating-point**: float (4 bytes), double (8 bytes)
- **Unsigned variants**: unsigned int, unsigned char, etc.
- **Size operators**: `sizeof(type)` returns bytes

### Control Structures
```c
// If-else
if (condition) {
    // code
} else if (condition2) {
    // code
} else {
    // code
}

// Switch
switch(value) {
    case 1:
        // code
        break;
    default:
        // code
}

// Loops
for (int i = 0; i < n; i++) { }
while (condition) { }
do { } while (condition);
```

### File I/O Operations
```c
// Opening files
FILE *fp = fopen("file.txt", "r");  // modes: r, w, a, r+, w+
if (fp == NULL) {
    perror("Error opening file");
    return 1;
}

// Reading
fscanf(fp, "%d %s", &num, str);
fgets(buffer, size, fp);           // Read line
fread(buffer, size, count, fp);    // Binary read

// Writing
fprintf(fp, "Value: %d\n", value);
fputs(string, fp);
fwrite(buffer, size, count, fp);   // Binary write

// Closing
fclose(fp);
```

### Standard Streams
- `stdin` - standard input
- `stdout` - standard output  
- `stderr` - standard error

---

## **WEEK 3: Structs, Pointers and Memory**

### Structures
```c
// Definition
struct Point {
    int x;
    int y;
};

// Declaration and initialization
struct Point p1 = {10, 20};
struct Point p2;
p2.x = 5;
p2.y = 15;

// Typedef for convenience
typedef struct {
    int x;
    int y;
} Point;

Point p3 = {1, 2};  // No 'struct' keyword needed
```

### Nested Structures
```c
typedef struct {
    Point position;
    int radius;
} Circle;

Circle c;
c.position.x = 10;
```

### Pointers Basics
```c
int x = 10;
int *ptr = &x;        // ptr holds address of x
int value = *ptr;     // Dereference: get value at address

// Pointer arithmetic
ptr++;                // Move to next int (adds 4 bytes)
ptr += 5;             // Move 5 ints forward

// NULL pointer
int *p = NULL;        // Good practice to initialize
if (p != NULL) { }    // Always check before dereferencing
```

### Pointers and Structures
```c
Point p = {5, 10};
Point *ptr = &p;

// Two ways to access members
(*ptr).x = 20;        // Dereference first
ptr->x = 20;          // Arrow operator (preferred)
```

---

## **WEEK 4: Pointers and Memory Allocation**

### Dynamic Memory Allocation
```c
// malloc: allocate uninitialized memory
int *arr = (int *)malloc(10 * sizeof(int));
if (arr == NULL) {
    // Allocation failed
}

// calloc: allocate and zero-initialize
int *arr2 = (int *)calloc(10, sizeof(int));

// realloc: resize allocated memory
arr = (int *)realloc(arr, 20 * sizeof(int));

// free: release memory
free(arr);
arr = NULL;  // Good practice
```

### Memory Segments
1. **Text/Code**: Program instructions (read-only)
2. **Data**: Global/static initialized variables
3. **BSS**: Uninitialized global/static variables
4. **Heap**: Dynamic allocation (grows upward)
5. **Stack**: Local variables, function calls (grows downward)

### Arrays and Pointers
```c
int arr[5] = {1, 2, 3, 4, 5};
int *ptr = arr;        // Array name is pointer to first element

arr[2] == *(arr + 2)   // TRUE: equivalent
ptr[2] == *(ptr + 2)   // TRUE: equivalent

// Array as function parameter (actually a pointer)
void func(int arr[], int size) { }
void func(int *arr, int size) { }  // Equivalent
```

### Strings
```c
// String as character array
char str1[6] = "hello";           // Need space for '\0'
char str2[] = "hello";            // Size calculated automatically

// String as pointer
char *str3 = "hello";             // Points to string literal (read-only)

// String functions (need #include <string.h>)
strlen(str);                      // Length (excluding '\0')
strcpy(dest, src);                // Copy
strncpy(dest, src, n);            // Copy n characters
strcmp(str1, str2);               // Compare (returns 0 if equal)
strcat(dest, src);                // Concatenate
```

### Common Pointer Errors
```c
// Dangling pointer
int *ptr = (int *)malloc(sizeof(int));
free(ptr);
*ptr = 10;  // ERROR: accessing freed memory

// Memory leak
ptr = (int *)malloc(sizeof(int));
ptr = NULL;  // ERROR: lost reference, can't free

// Uninitialized pointer
int *ptr;
*ptr = 10;  // ERROR: ptr points to random address
```

---

## **WEEK 5: Bits, Bytes and Integers**

### Number Systems
- **Binary**: Base 2 (0, 1)
- **Octal**: Base 8 (0-7), prefix `0` in C
- **Decimal**: Base 10 (0-9)
- **Hexadecimal**: Base 16 (0-9, A-F), prefix `0x` in C

### Conversion Practice
```
Decimal: 157
Binary: 10011101
Hex: 0x9D
Octal: 0235
```

### Unsigned Integers
- **n-bit unsigned**: Range 0 to 2^n - 1
- 8-bit: 0 to 255
- 16-bit: 0 to 65,535
- 32-bit: 0 to 4,294,967,295

### Two's Complement (Signed Integers)
- **n-bit signed**: Range -2^(n-1) to 2^(n-1) - 1
- 8-bit: -128 to 127
- 16-bit: -32,768 to 32,767
- 32-bit: -2,147,483,648 to 2,147,483,647

**To negate**: Flip all bits and add 1
```
5 (binary):    00000101
Flip bits:     11111010
Add 1:         11111011  = -5
```

### Bitwise Operators
```c
& (AND):    1010 & 1100 = 1000
| (OR):     1010 | 1100 = 1110
^ (XOR):    1010 ^ 1100 = 0110
~ (NOT):    ~1010 = 0101 (flips all bits)
<< (left):  1010 << 2 = 101000  (multiply by 4)
>> (right): 1010 >> 2 = 10      (divide by 4)
```

### Common Bit Manipulation Tricks
```c
// Check if bit n is set
if (x & (1 << n)) { }

// Set bit n
x |= (1 << n);

// Clear bit n
x &= ~(1 << n);

// Toggle bit n
x ^= (1 << n);

// Check if power of 2
if (x && !(x & (x - 1))) { }

// Get rightmost 1-bit
x & (-x)

// Turn off rightmost 1-bit
x & (x - 1)
```

### Integer Overflow
```c
// Unsigned overflow: wraps around
unsigned char x = 255;
x++;  // x becomes 0

// Signed overflow: undefined behavior in C
int y = INT_MAX;
y++;  // Undefined!
```

---

## **WEEK 6: Floating Point & Bit Fields**

### IEEE 754 Floating Point (32-bit float)
```
Sign (1 bit) | Exponent (8 bits) | Mantissa/Fraction (23 bits)
```

**Formula**: (-1)^sign × 1.fraction × 2^(exponent - 127)

### Special Values
- **Zero**: exponent = 0, fraction = 0
- **Infinity**: exponent = 255, fraction = 0
- **NaN**: exponent = 255, fraction ≠ 0
- **Denormalized**: exponent = 0, fraction ≠ 0

### Floating Point Limitations
```c
float a = 0.1;
float b = 0.2;
// a + b might not equal 0.3 exactly!

// Never compare floats with ==
if (fabs(a - b) < 0.00001) { }  // Better approach
```

### Bit Fields
```c
// Compact representation for flags
struct Flags {
    unsigned int flag1 : 1;  // 1 bit
    unsigned int flag2 : 1;  // 1 bit
    unsigned int value : 6;  // 6 bits
    // Total: 8 bits = 1 byte
};

struct Flags f;
f.flag1 = 1;
f.flag2 = 0;
f.value = 42;
```

---

## **WEEK 7: Introduction to Assembly Language**

### x86-64 Registers (64-bit)
```
General Purpose:
%rax, %rbx, %rcx, %rdx    - Accumulator, Base, Counter, Data
%rsi, %rdi                - Source Index, Destination Index
%rbp                      - Base Pointer (frame pointer)
%rsp                      - Stack Pointer
%r8-%r15                  - Additional registers

32-bit: %eax, %ebx, etc.
16-bit: %ax, %bx, etc.
8-bit:  %al, %ah, %bl, %bh, etc.
```

### Basic Instructions
```assembly
; Data movement
mov $5, %rax        ; Move immediate value 5 to rax
mov %rax, %rbx      ; Copy rax to rbx
mov (%rax), %rbx    ; Load from memory address in rax

; Arithmetic
add $10, %rax       ; rax += 10
sub %rbx, %rax      ; rax -= rbx
imul $3, %rax       ; rax *= 3 (signed)
idiv %rbx           ; rax = rax/rbx, rdx = remainder

; Logic
and $0xFF, %rax     ; rax &= 0xFF
or  $0x80, %rax     ; rax |= 0x80
xor %rax, %rax      ; rax = 0 (common idiom)
not %rax            ; Flip all bits

; Shifts
sal $2, %rax        ; Shift arithmetic left (multiply by 4)
sar $2, %rax        ; Shift arithmetic right (divide by 4)
shl $2, %rax        ; Shift logical left
shr $2, %rax        ; Shift logical right
```

### Addressing Modes
```assembly
mov $0x4, %rax          ; Immediate: value 4
mov %rbx, %rax          ; Register: copy rbx
mov 0x8049a58, %rax     ; Direct: from memory address
mov (%rbx), %rax        ; Indirect: from address in rbx
mov 4(%rbx), %rax       ; Displacement: from rbx + 4
mov (%rbx,%rcx), %rax   ; Indexed: from rbx + rcx
mov (%rbx,%rcx,4), %rax ; Scaled: from rbx + rcx*4
mov 8(%rbx,%rcx,4), %rax; General: from rbx + rcx*4 + 8
```

---

## **WEEK 8: Conditional Execution and Procedure Calls**

### Condition Codes (EFLAGS)
- **CF** (Carry): Unsigned overflow
- **ZF** (Zero): Result was zero
- **SF** (Sign): Result was negative
- **OF** (Overflow): Signed overflow

### Comparison and Tests
```assembly
cmp %rbx, %rax      ; Compare (rax - rbx), set flags
test %rax, %rax     ; Test (rax & rax), set flags (checks if zero)
```

### Conditional Jumps
```assembly
je  label    ; Jump if equal (ZF=1)
jne label    ; Jump if not equal (ZF=0)
jg  label    ; Jump if greater (signed)
jge label    ; Jump if greater or equal (signed)
jl  label    ; Jump if less (signed)
jle label    ; Jump if less or equal (signed)
ja  label    ; Jump if above (unsigned)
jb  label    ; Jump if below (unsigned)
jmp label    ; Unconditional jump
```

### C to Assembly: If-Else
```c
if (x > y) {
    z = x;
} else {
    z = y;
}
```
```assembly
    mov x, %rax
    mov y, %rbx
    cmp %rbx, %rax
    jle else_branch
    mov %rax, z
    jmp end
else_branch:
    mov %rbx, z
end:
```

### Function Calling Convention (x86-64 System V)

**Argument Passing** (first 6 in registers):
1. %rdi
2. %rsi
3. %rdx
4. %rcx
5. %r8
6. %r9
- Additional arguments on stack (right to left)

**Return Value**: %rax

**Caller-saved**: %rax, %rcx, %rdx, %rsi, %rdi, %r8-r11
**Callee-saved**: %rbx, %rbp, %r12-r15

### Function Prologue and Epilogue
```assembly
function:
    ; Prologue
    push %rbp           ; Save old base pointer
    mov %rsp, %rbp      ; Set new base pointer
    sub $16, %rsp       ; Allocate 16 bytes local space
    
    ; Function body
    ...
    
    ; Epilogue
    mov %rbp, %rsp      ; Restore stack pointer
    pop %rbp            ; Restore base pointer
    ret                 ; Return
```

### Stack Frame Layout
```
Higher addresses
+------------------+
| Arguments 7+     |
+------------------+
| Return address   |
+------------------+
| Old %rbp         | <-- %rbp points here
+------------------+
| Local variables  |
+------------------+
| Saved registers  | <-- %rsp points here
+------------------+
Lower addresses
```

---

## **WEEK 9: Arrays and Memory**

### Array Access in Assembly
```c
int arr[10];
int x = arr[3];
```
```assembly
; Assuming arr base address in %rdi, i in %rsi
mov (%rdi,%rsi,4), %rax    ; rax = arr[i]
                            ; 4 = sizeof(int)
```

### Multi-dimensional Arrays
```c
int matrix[3][4];  // 3 rows, 4 columns
// Stored row-major: row0, then row1, then row2
```

**Address calculation**: `base + (row * num_cols + col) * sizeof(element)`

```assembly
; matrix[i][j] where matrix base in %rdi, i in %rsi, j in %rdx
imul $4, %rsi, %rax      ; i * num_cols (4)
add %rdx, %rax           ; + j
lea (%rdi,%rax,4), %rax  ; base + offset * sizeof(int)
```

### Struct Access in Assembly
```c
struct Person {
    int age;      // offset 0
    char name[20];// offset 4
    float salary; // offset 24
};
```
```assembly
; Assuming Person* in %rdi
mov 0(%rdi), %eax       ; age
lea 4(%rdi), %rax       ; address of name
movss 24(%rdi), %xmm0   ; salary (float)
```

### Stack Arrays
```c
void func() {
    int arr[100];  // Allocated on stack
}
```
```assembly
func:
    push %rbp
    mov %rsp, %rbp
    sub $400, %rsp     ; 100 * 4 bytes
    ; arr[0] at -400(%rbp)
    ; arr[99] at -4(%rbp)
```

---

## **WEEK 10: Buffer Overflow, struct and union**

### Buffer Overflow Attack
```c
void vulnerable() {
    char buffer[8];
    gets(buffer);  // DANGEROUS! No bounds checking
}
```

**Attack**: Input > 8 bytes overwrites:
1. Local variables
2. Saved %rbp
3. Return address ← Can redirect execution!
4. Function arguments

### Stack Smashing Example
```
Before overflow:
+------------------+
| Return address   | <-- Want to change this
+------------------+
| Saved %rbp       |
+------------------+
| buffer[8]        | <-- Writing starts here
+------------------+

After overflow with "AAAAAAAAAAAABBBBCCCC":
+------------------+
| CCCC             | <-- Return address overwritten!
+------------------+
| BBBB             | <-- %rbp overwritten
+------------------+
| AAAAAAAA         | <-- Buffer
+------------------+
```

### Protection Mechanisms
- **Stack Canaries**: Random value placed before return address
- **ASLR** (Address Space Layout Randomization): Randomize memory locations
- **NX Bit** (No-Execute): Mark stack as non-executable
- **Safe functions**: Use `fgets()`, `strncpy()` instead of `gets()`, `strcpy()`

### Union
```c
union Data {
    int i;
    float f;
    char str[20];
};  // All members share same memory

union Data d;
d.i = 10;
// d.f and d.str now contain garbage
// Only one member valid at a time
```

**Size**: Size of largest member

**Use cases**:
- Type punning (reinterpret bits)
- Memory saving when only one field used at a time
- Variant types

### Struct vs Union
```c
struct S {
    int a;
    int b;
};  // Size: 8 bytes (both stored)

union U {
    int a;
    int b;
};  // Size: 4 bytes (overlapping)
```

### Struct Alignment and Padding
```c
struct Example {
    char c;     // 1 byte
    // 3 bytes padding
    int i;      // 4 bytes
    char d;     // 1 byte
    // 3 bytes padding
};  // Total: 12 bytes (not 6!)
```

**Rules**:
- Members aligned to their size
- Struct size is multiple of largest member alignment
- Use `#pragma pack` or `__attribute__((packed))` to disable

---

## **WEEK 11: Memory and Cache**

### Memory Hierarchy
```
Registers     (~1 cycle, bytes)
    ↓
L1 Cache      (~4 cycles, 32-64 KB)
    ↓
L2 Cache      (~10 cycles, 256 KB-1 MB)
    ↓
L3 Cache      (~40 cycles, 8-64 MB)
    ↓
RAM           (~100 cycles, GBs)
    ↓
SSD/Disk      (~100,000 cycles, TBs)
```

### Cache Organization
**Cache Line**: Typically 64 bytes (smallest unit of cache storage)

**Three types**:
1. **Direct-mapped**: Each memory address maps to one cache line
2. **Fully associative**: Any memory can go anywhere in cache
3. **N-way set associative**: Hybrid (most common)

### Cache Address Breakdown
```
|  Tag  |  Set Index  |  Block Offset  |
```
- **Block offset**: Which byte within cache line
- **Set index**: Which set in cache
- **Tag**: Identify which memory address

### Locality Principles

**Temporal Locality**: Recently accessed data likely accessed again soon
```c
// Good temporal locality
for (int i = 0; i < n; i++) {
    sum += arr[i];  // 'sum' reused in every iteration
}
```

**Spatial Locality**: Nearby data likely accessed soon
```c
// Good spatial locality
for (int i = 0; i < n; i++) {
    sum += arr[i];  // Sequential access
}

// Bad spatial locality
for (int i = 0; i < n; i += 100) {
    sum += arr[i];  // Skipping elements
}
```

### Cache-Friendly Code

**Row-major traversal** (Good):
```c
for (int i = 0; i < rows; i++) {
    for (int j = 0; j < cols; j++) {
        sum += matrix[i][j];  // Sequential in memory
    }
}
```

**Column-major traversal** (Bad for C):
```c
for (int j = 0; j < cols; j++) {
    for (int i = 0; i < rows; i++) {
        sum += matrix[i][j];  // Jumping around
    }
}
```

### Cache Misses
- **Cold miss** (Compulsory): First access to data
- **Capacity miss**: Cache too small for working set
- **Conflict miss**: Multiple addresses map to same location

---

## **WEEK 12: I/O, Virtual Memory, Exceptional Control Flow**

### Virtual Memory

**Benefits**:
1. Protection: Each process has own address space
2. Memory management: Can use more memory than physical RAM
3. Simplification: Each process sees full address space

**Address Translation**:
```
Virtual Address → MMU → Physical Address
```

### Paging
- Memory divided into **pages** (typically 4 KB)
- **Page table**: Maps virtual pages to physical frames
- **TLB** (Translation Lookaside Buffer): Cache for page table entries

### Page Table Entry (PTE)
```
| Valid | Permissions | Physical Frame Number | Other bits |
```
- **Valid bit**: Is page in memory or on disk?
- **Permissions**: Read, Write, Execute
- **Dirty bit**: Has page been modified?
- **Reference bit**: Has page been accessed?

### Page Fault
When accessing page not in memory:
1. CPU traps to OS
2. OS loads page from disk
3. Updates page table
4. Restarts instruction

### Memory-Mapped I/O
```c
int fd = open("file.txt", O_RDONLY);
void *addr = mmap(NULL, length, PROT_READ, MAP_PRIVATE, fd, 0);
// Now can access file like memory
char c = ((char *)addr)[100];  // Read byte 100
munmap(addr, length);
```

### System Calls

**Process control**:
```c
pid_t fork();           // Create child process
int exec(const char *); // Replace process image
void exit(int status);  // Terminate process
pid_t wait(int *status);// Wait for child
```

**Fork behavior**:
```c
pid_t pid = fork();
if (pid == 0) {
    // Child process
    printf("I'm the child\n");
} else {
    // Parent process
    printf("I'm the parent, child PID: %d\n", pid);
}
// Both processes continue here
```

### Signals

**Common signals**:
- `SIGINT` (2): Interrupt (Ctrl+C)
- `SIGTERM` (15): Termination request
- `SIGKILL` (9): Kill (cannot be caught)
- `SIGSEGV` (11): Segmentation fault
- `SIGCHLD` (17): Child terminated

**Signal handling**:
```c
#include <signal.h>

void handler(int signum) {
    printf("Caught signal %d\n", signum);
}

signal(SIGINT, handler);  // Register handler
```

### Exception Types
1. **Interrupts**: From I/O devices (async)
2. **Traps**: Intentional (syscalls)
3. **Faults**: Recoverable errors (page fault)
4. **Aborts**: Unrecoverable errors

---

## **Common Exam Topics & Practice**

### Data Representation Conversions
**Practice**: Convert between binary, hex, decimal, two's complement

Example: What is -42 in 8-bit two's complement?
```
42 in binary: 00101010
Flip bits:    11010101
Add 1:        11010110  = 0xD6 = -42
```

### Assembly Reading
**Practice**: Trace through assembly code, determine output

Example:
```assembly
mov $5, %rax
mov $3, %rbx
imul %rbx, %rax
add $2, %rax
; What's in %rax? Answer: 17
```

### C Pointer Questions
**Practice**: Predict output or identify errors

Example:
```c
int arr[] = {10, 20, 30};
int *p = arr + 1;
printf("%d\n", *p);      // 20
printf("%d\n", *(p+1));  // 30
printf("%d\n", p[-1]);   // 10
```

### Buffer Overflow Scenarios
**Practice**: Identify vulnerable code, explain exploits

### Memory Layout Questions
**Practice**: Draw stack/heap after operations

### Cache Performance
**Practice**: Calculate hit rate, explain cache-friendly code

---

## **GDB Command Reference (for Bomb Lab)**

```bash
gdb ./bomb              # Start debugger
(gdb) break main        # Set breakpoint
(gdb) run               # Start execution
(gdb) run < input.txt   # Run with input file
(gdb) continue          # Continue to next breakpoint
(gdb) next              # Step over (n)
(gdb) step              # Step into (s)
(gdb) finish            # Run until return
(gdb) print $rax        # Print register
(gdb) print/x $rax      # Print in hex
(gdb) x/s $rdi          # Examine string at rdi
(gdb) x/10x $rsp        # Examine 10 hex values at stack
(gdb) disas phase_1     # Disassemble function
(gdb) info registers    # Show all registers
(gdb) info frame        # Show current stack frame
(gdb) backtrace         # Show call stack
```

---

## **Study Checklist**

### Week 1-6 Fundamentals
- [ ] Compile and run C programs with gcc
- [ ] Read/write files with proper error handling
- [ ] Create and manipulate structs
- [ ] Use pointers correctly (malloc, free, dereferencing)
- [ ] Perform bitwise operations
- [ ] Convert between number systems
- [ ] Understand two's complement
- [ ] Work with bit fields

### Week 7-12 Systems
- [ ] Read and write basic assembly
- [ ] Understand register conventions
- [ ] Trace function calls and stack frames
- [ ] Identify buffer overflow vulnerabilities
- [ ] Understand cache locality
- [ ] Explain virtual memory and paging
- [ ] Use system calls (fork, exec, wait)
- [ ] Debug with GDB

### Assignments
- [ ] Review Data File Lab code and viva questions
- [ ] Review all Bomb Lab phases
- [ ] Practice GDB debugging techniques

---

## **Final Tips**

1. **Practice coding by hand**: Exams often don't allow computers
2. **Draw diagrams**: Memory layouts, stack frames, cache organization
3. **Work through past exams**: If available from your lecturer
4. **Understand, don't memorize**: Know why, not just what
5. **Test edge cases**: NULL pointers, overflow, boundary conditions
6. **Time management**: Don't spend too long on one question

Good luck with your exam! 🚀
