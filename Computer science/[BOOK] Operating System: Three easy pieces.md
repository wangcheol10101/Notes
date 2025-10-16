The OS takes a physical resource (such as the processor, or memory, or a disk) and transforms it into a <ins>more general, powerful, and easy-to-use virtual form</ins> of itself.
In order to <ins>allow users to tell the OS what to do</ins> and thus make use of the features of the virtual machine (such as running a program, or allocating memory, or accessing a file), <ins>the OS also provides some interfaces (system call)</ins> that you can call.

> [!NOTE]
> System calls are ultimately invoked using assembly instructions.
> High-level languages provide abstractions(libaaries) so you don't have to write assembly yourself.

**What does a running program do?**
The processor fetches an instruction from memory, decodes it (i.e., ﬁgures out which instruction this is), and executes it.

> [!NOTE]
> Runnable code is typically in binary (machine code) format, which the processor can directly execute. Assembly code is a human-readable representation of machine instructions and must be assembled into binary before it can run on hardware.

> [!NOTE]
> When a program is running, its runnable binary code (or at least the parts needed for execution) is loaded into memory. The processor then fetches the current instruction from memory and loads it into a register (such as the instruction register) to decode and execute it.

**Defination of Virtualizing the CPU**
Turning a single CPU (or small set of them) into a seemingly infinite number of CPUs and thus allowing many programs to seemingly run at once is what we call virtualizing the CPU.

Memory is just an array of bytes; to read memory, one must specify an address to be able to access the data stored there.
Each instruction of the program is in memory too, thus memory is accessed on each instruction fetch.

**Process Identifier (PID)**
PID is unique per running process.

> [!NOTE]
> The PID is stored as a field in the kernel’s process data structure (like task_struct in Linux), and all such structures are managed in a table or list by the OS kernel.
> The process table (which holds structures like task_struct) is stored in main memory, not in processor registers.

> [!IMPORTANT]
> Two processes can both use the same memory address, but they’ll map to different physical locations behind the scenes.


**Defination of Address Space**
An address space is the range of memory addresses that a process or thread can use. <ins>Each process is given its own private address space by the operating system, which means it cannot directly access the memory of other processes</ins>.

**Defination of Thread**
A thread is the smallest unit of execution <ins>within a process</ins>. Each thread represents a separate flow of control, <ins>sharing the same address space and resources (such as memory and open files) with other threads in the same process</ins>, but <ins>maintaining its own registers</ins>, stack, and program counter.


**Register**
A register is a small, fast storage location inside a CPU. Registers temporarily hold data, instructions, or addresses that the CPU is currently using or processing.
Each thread has its own set of these registers.

**Main Types of Registers**

> [!NOTE]
> Think of the stack as a stack of plates (the whole structure), and each plate as a stack frame (one function call’s data).
> Stack frames are created and destroyed as functions are called and return. The stack itself persists for the lifetime of the thread.

---
# Operating System: Three Easy Pieces — Key Concepts

## 1. What is an Operating System (OS)?
**Definition:**
The OS takes a physical resource (such as the processor, memory, or disk) and transforms it into a <ins>more general, powerful, and easy-to-use virtual form</ins> of itself.

To <ins>allow users to tell the OS what to do</ins> and make use of the features of the virtual machine (such as running a program, allocating memory, or accessing a file), <ins>the OS provides interfaces (system calls)</ins> that you can call.

> [!NOTE]
> System calls are ultimately invoked using assembly instructions.
> High-level languages provide abstractions (libraries) so you don't have to write assembly yourself.

---
## 2. Running Programs & CPU Virtualization
**What does a running program do?**
The processor fetches an instruction from memory, decodes it (figures out which instruction this is), and executes it.

> [!NOTE]
> Runnable code is typically in binary (machine code) format, which the processor can directly execute. Assembly code is a human-readable representation of machine instructions and must be assembled into binary before it can run on hardware.

> [!NOTE]
> When a program is running, its runnable binary code (or at least the parts needed for execution) is loaded into memory. The processor then fetches the current instruction from memory and loads it into a register (such as the instruction register) to decode and execute it.

**Virtualizing the CPU:**
Turning a single CPU (or small set of them) into a seemingly infinite number of CPUs and thus allowing many programs to seemingly run at once is called virtualizing the CPU.

Memory is just an array of bytes; to read memory, one must specify an address to access the data stored there. Each instruction of the program is in memory too, so memory is accessed on each instruction fetch.

---
## 3. Processes & Threads
### Process Identifier (PID)
PID is unique per running process.

> [!NOTE]
> The PID is stored as a field in the kernel’s process data structure (like `task_struct` in Linux), and all such structures are managed in a table or list by the OS kernel.
> The process table (which holds structures like `task_struct`) is stored in main memory, not in processor registers.

> [!IMPORTANT]
> Two processes can both use the same memory address, but they’ll map to different physical locations behind the scenes.

### Address Space
An address space is the range of memory addresses that a process or thread can use. <ins>Each process is given its own private address space by the operating system, which means it cannot directly access the memory of other processes</ins>.

### Thread
A thread is the smallest unit of execution <ins>within a process</ins>. Each thread represents a separate flow of control, <ins>sharing the same address space and resources (such as memory and open files) with other threads in the same process</ins>, but <ins>maintaining its own registers</ins>, stack, and program counter.

---
## 4. Registers & The Stack
### Register
A register is a small, fast storage location inside a CPU. Registers temporarily hold data, instructions, or addresses that the CPU is currently using or processing.
Each thread has its own set of these registers.

#### Main Types of Registers
- **General Purpose Registers**: Used to hold operands and intermediate results during computation (e.g., `EAX`, `EBX` in x86).
- **Program Counter (PC) / Instruction Pointer (IP)**: Holds the address of the next instruction to execute.
- **Stack Pointer (SP)**: Points to the top of the current stack in memory, used for function calls and local variables.
- **Base Pointer (BP) / Frame Pointer (FP)**: Used to reference function parameters and local variables within the stack frame.
- ...

> [!NOTE]
> Think of the stack as a stack of plates (the whole structure), and each plate as a stack frame (one function call’s data).
> Stack frames are created and destroyed as functions are called and return. The stack itself persists for the lifetime of the thread.

