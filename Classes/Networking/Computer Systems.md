________
01-24-2024 | 08:19
Status: #school 
Tags: #networkandsecurity

# Computer Systems
A computer system consists of hardware and systems software that work together to run application programs.
Systems programming is the study of the operation of such systems and gaining the ability to program such systems.
- such knowledge will make you a "power programmer"
"Hello World" as an example of how important it is to understand computer systems. 


### Representation of Hello World
Facts:
- The hello world source code is represented in memory (and stored on disk) as a sequence of bytes.
- Each byte is just a number
- Each byte represent one character
- Each character is encoded according to the ASCII table
	- The '#' is actually the number 35
	- The 'i' in 'include' is actually the number 105
- Each line is terminated by a special, invisible character called the newline character
	- Which is actually the number 10.
	- Except on Windows, where the end of the line is represented as two characters: a carriage return followed by a newline
		- Which is a 13 byte followed by a 10 byte
- Files that hold such data (text encode as ASCII characters) are termed a text file
- All other files are called binary files

# Data Representations
- So, everything in a computer is stored as a sequence of bits.
- The only thing that distinguishes different data objects is the context in which we view them.
	- Example: text editors display the bits as a sequence of characters. 
- Another example: The string "150", the integer 150, and the float 150 are each stored differently. 
- If we, as programmers, do not understand these different representations, how to manipulate them, and how to convert between them, then we can get unexpected results in our programs. 

### Programs are Translated by Other Programs into Different Forms
- The text file that contains the "Hello World" program cannot be executed by a computer
- Its human readable representation is only understood by humans
- Before the computer can run the program, the text file must be converted into the representation that the computer understands. 
- The language that the computer understands (and the only one) is the computer's machine language
- So, a file the computer can execute is made up of machine language instructions
- This file is called an [[executable file]]

# Compilation
Source Program (text) - preprocessor -> Modified Source Program (text) - Compiler -> Assembly Program (text) - assembler -> Relocatable object programs (binary) - Linker -> Executable object program (binary)

### It Pays to Understand How Compilation Systems Work
Understanding Compilation can help us:
- Optimize program performance
- Understanding link-time errors
- Avoiding security holes
- Write mixed language programs (in C, C++, Java, Python, ...)
- Understand how scoping works and take advantage of it
- and lots more...

## Processors Read and Interpret Instructions Stored in Memory
- So, once a source code file has been turned into an executable file...
- You can run it. How? from a command line **shell** or double click on its icon
- The Shell is a command-line interpreter that prints a prompt, waits for you to type a command line and then performs the command
- If the first word of the command line does not correspond to a built-in shell command, then the shell assumes that it is the name of an executable file that it should load and run.
- In this case, the shell loads and runs the hello program and then waits for it to terminate.
- The shell then prints a prompt and waits for the next input command line

### Hardware Organization of a System
![[organizationOfASystem.jpeg]]

# Main Memory
- The main memory is a temporary storage device that holds both a program and the data it manipulates while the processor is executing the program.
	- Note that main memory holds both data and code
- Physically, main memory consists of a collection of dynamic random access memory (DRAM) chips
- Logically, memory is organized as a linear array of bytes, each with its own unique address (array index) starting at 0.
- Each of the machine instructions that constitute a program can consist of a variable number of bytes.
- The sizes of data items that correspond to C program variables vary according to type. 
	- On a X86-64, a short is two bytes, an int is 4 bytes, a long is 8 bytes, a long long is 8 bytes, a float is 4 bytes, and a double is 8 bytes
	- Note: Windows is the exception (of course). A long on Windows is 4 bytes long.

# Processor
- The Central Processing Unit (CPU), or simply processor, is the engine that interprets (or executes) instructions stored in main memory. 
- It has a word-size register called the program counter (PC)
- The PC points at (contains the address of) some machine-language instructions in main memory
- The processor repeatedly executes the instruction pointed at by the program counter
	- From the time that power is applied to the system until the time that the power is shut off
- After executing an instruction, the processor updates the program counter to point to the next instruction

##### Processor continued
- A processor operates according to a very simple instruction execution model, defined by its instruction set architecture
- Instructions execute in strict sequence
- However, each instruction execution requires a number of steps, called the [[fetch-and-execute cycle]]:
	- The processor reads the instruction memory pointed at by the PC
	- It then interprets the bits in the instruction, and performs some simple operation dictated by the instruction
	- It then updates the PC(RIP if Intel) to point to the next instruction
- These simple instructions typically manipulate main memory, registers, or I/O ports
	- registers are word-sized, very fast memory located on the CPU chip
	- I/O ports are special device memory addresses used to manipulate off-chip I/O devices (such as the solid state drive, USB device, etc.)

# Processor Instructions
- The arithmetic/logic unit (ALU), which is part of the processor, computes new data and address values
- Some examples of the simple operations that the CPU might carry out are:
	- Load: Copy a byte or a word from main memory into a register, overwriting the previous contents of the register.
	- Store: Copy a byte or a word from a register to a location in main memory, overwriting the previous contents of that location
	- Add, Subtract, Divide, Multiply and other operations: Copy the contents of two registers to the ALU, perform an arithmetic operation on the two words, and store the result in a register, overwriting the previous contents of that register. 
	- Jump: Extract a word from the instruction itself and copy that word into the program counter (PC), overwriting the previous value of the PC.
- A CPU has an instruction set
- Various models of CPUs that implement the same instruction set may have different implementations of that instruction set (with different optimizations).
	- They have different micro-architectures
ISA = Instruction Set Architecture 

### Return to Hello World
So, what happens when we run our example program?
The shell
- As we type the characters ./hello at the keyboard, the shell program reads each one into a register and then stores it in memory
- When we hit the enter key on the keyboard, the shell knows that we have finished typing the command.
- The shell then asks the OS to run the hello executable file
- The OS loads the code and data of the executable file into main memory
- The processor then begins executing the machine-language instructions in the hello program's main routine.
- The instructions copy the address of the hello string into a register and then calls the OS to print the string
- The OS then prints the string

# Caching
- As can be seen from the previous example, a program can spend a lot of its time moving data around
- For another example, consider reading a file
	- Each access of the disk device takes a lot of time (from the processor's point of view)
- To speed things up, the OS will do a bulk read from the slow disk device into faster memory called a cache
- Then each subsequent access to the file reads the requested bytes from the fast cache instead of the slow device

Registry's = fastest memory period
Cache = much faster than ram, bc you don't have to go across I/O bridge
Ram = faster than SSD or HDD 
Principle of LOCALITY - references tend to cluster
Prefetching is when caches pre-grab the next set of instructions because they know what will need to come next (thats why we say references tend to cluster!)

## Storage Devices Form a Hierarchy
![[StorageHierarchy.png]]

Graphics = Matrices
VRAM/Graphics Cards are good for high-performance computing is because they are great at manipulating matrices and connected to really fast memory. In hierarchy - above ram. SIMD - single instruction multiple data

### The Operating System Manages the Hardware
Neither the shell or the hello program from our example accessed I/O devices directly.
They relied on the services provided by the Operating System (OS)
All attempts by an application program to manipulate the hardware must go through the operating system.
The operating system has two primary purposes: 
1. to efficiently and safely provide hardware and software resources to the applications (the resource management principle)
2. to provide applications with simple and uniform mechanisms for manipulating complicated and often wildly different low-level hardware devices (the beautification principle)
The Operating System achieves both goals via the fundamental abstractions: processes, virtual memory, and files.
API = Application Programming Interface

# Processes
When a program such as hello world runs on a modern system, the operating system provides the illusion that the program is the only one running on the system.
- As if the program has exclusive access to the processor, memory and devices
- However, this is an illusion
This illusion is provided by the notion of a process.
A process is the operating system's abstraction for a running program.
Multiple processes can run concurrently on the same system, and each process appears to have exclusive use of the hardware.
[[Concurrency]]: Two or more programs are active in the computer system
- If the computer system has more programs active then there are processors, then the instructions of the process are interleaved on the processors.

### Processes (2)
- The operating system performs this interleaving with a mechanism known as **context switching**

## Threads 
- By default, a process has a single point of execution.
- However, a process can actually consist of multiple execution units, called threads. 
- All the threads in a process share the same code and global data.
- Threads are an increasingly important programming model
	- Network servers require concurrency, and its easier to share data between multiple threads than between multiple processes
	- Switching between threads in a process is less computationally expensive than switching between processes. 

threads can spawn off of each other and include their own stack and registers
- threads live inside one process with the shared process memory
- weakness of multi-threading means one thread could be a bad actor (i.e. reference a null ptr or somethin) and cause all the other threads to crash. If a process is a bad actor, only it crashes.

### Virtual Memory
- It is true that an OS make it look like, to a process, that is has the computers memory all to itself.
	- Due to process isolation and logical addressing, usually implemented with paging. 
- However, virtual memory makes it look, to the process, like there is more RAM than there actually is. 
- So, why is virtual memory good?
	- More multiprogramming (more programs in memory at once) means more concurrency to keep the processor and devices busy
	- during peak times (when memory utilization is high), the OS can still keep the processes running (instead of kicking them out)
- How is virtual memory implemented? by utilizing secondary storage to temporarily hold pieces of RAM so that an entire process does not need to be in memory at one time. 
Unix is faster than windows because it doesn't go through file system to utilize virtual memory. Windows does. 

# Memory Organization
The address space seen by each process consists of a number of well-defined areas, each with a specific purpose:
- Program code
- Program data
- Program heap
- Shared libraries (shared memory between programs)
- Stack

# Files
- A **file** is a sequence of bytes
- In Unix, every I/O device, including disks, keyboards, displays, and even networks, is modeled as a file
	- Most general purpose operating systems mirror this behavior to an extent, even Windows
	- Of course, all modern OSs borrow many concepts from Unix
- All input and output in the system is performed by reading and writing files 
	- using a small set of system calls known as Unix I/O
- This simple and elegant model of a file is nonetheless very powerful
	- it provides applications with.a uniform view of all the varied I/O devices that might be contained in the system.

### Concurrency and Parallelism
- We want computers to do more and do it faster
- Both of these factors improve when the processor does more things at once
- We use the term concurrency to refer to the general concept of a system with multiple, simultaneous activities 
	- Those activities can be happening in parallel, but not necessarily
- We use the term parallelism to refer to the use of concurrency to make a system run faster
	- In this case, the computer is actually executing instruction simultaneously, typically by using more than one core or processor
- Parallelism can be exploited at multiple levels of abstraction in a computer system

### Threads 
- With threads, we can even have multiple control flows executing within a single process
- Support for concurrent execution has been found in computer systems since the advent of time-sharing in the early 1960s
	- Windows did not support multi-threading until 1993, decades behind other operating systems in technology
- Traditionally, this concurrent execution was only simulated, by having a single computer rapidly switch among it's executing processes
	- Concurrently, but not parallel
- This form of concurrency allows multiple users to interact with a system at the same time, 
	- such as when many people want to get pages from a single Web server
	- It also allows a single user to engage in multiple tasks concurrently 
- Until recently, most actual computing was done by a single processor, even if that processor had to switch among multiple tasks.
- Such a configuration is known as a uni-processor-system



