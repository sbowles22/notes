#lecture

# Chapter 1: Introduction to Computers
*The basic shit*

## Primary Components of a Computer
- A Central Processing Unit\*
- Main Memory\*
- Input/output
- Systems interconnection

\*Focusing on these b/c they typically are **limited resources** that we must manage in our programs

### Primary Components of a CPU
- Registers
- Arithmetic and Logic Unit
- Control Unit
- Interconnection

### Main Memory
Stores **data and instructions** for and of programs.
- Primary Memory (RAM; mostly volatile, short term, low capacity, fast)
- Secondary Memory (HDD; non-volatile, long term, high capacity, slow)

Data and instructions are **fetched** from memory **addresses** 
We will select **names** (references) that are meaningful to us as programmers to link an address to.

### Processing Instructions
The CPU executes instructions using a process known as the **instruction cycle**
1. Fetch Instructions
2. Interpret Instructions
3. Fetch Data (usually from Registers or Primary Memory)
4. Process Data
5. Write results (usually to Registers or Primary Memory)

### Why is secondary memory slower than primary memory?
- Could have moving or mechanical parts (in HDD but not SSD)
- Further phisical distance from the CPU (or machine)
- Increased time required to locate specific content in a high capacity device

If primary memory is faster, why not only use primary memory?
- Money \$\$\$
- Power consumption of volatile memory

### Memory Hierarchy (mostly)
1. CPU Registers (~100)
2. Primary Memory (~$10^6$)
3. Secondary Memory (~$10^9$)

Higher is more speed, lower is more capacity.

## Programming Languages 
We have our languages known as **natural languages**. The computer has its own language, its **machine language**, which is nearly incomprehensible to humans, so we design **programming languages** to bridge the gap. Programming languages can be **compiled** into machine languages, but are still usable by humans.

### Language Heirarchy
1. Natural Language (English, Spanish)
2. High-Level Languages (C, Python, MatLab) -- not reliant on specific hardware
3. Low-Level Languages (Assembly) -- reliant on specific hardware
4. Machine Languages 

### Creating and Running Programs
You have to compile high-level languages into machine language to convert source code into instructions.

### Writing and Editing the Program
Programs must be written in a **text editor**. We use `vi` in this class. 

#### Saving in `vi`
- use `:w` to save
- use `:wq` to save & quit

**Save early and often!!!**

### Compiling the Program
A compiler is a type of software that converts source code in a programming language into the machine language of the computer. We use `gcc` in this class. If there are any syntax errors, the compilation will not be completed.

`gcc source.c` to compile `source.c` to `a.out` -- this will overwrite an existing `a.out`

If `gcc` says nothing, thats good! :)

NOTE: DO NOT VERSION CONTROL CODE PUBLICALLY B/C ACADEMIC INTEGRITY AND SHIT

#### Preprocessing
`gcc` will make minor adjustments to the program before compilation, lines with an `#include` or `#define` are preprocessor instructions.

### Program Execution
type `a.out` to execute the program!

### Structure Charts ([[Chapter 4]])
A structure chart breaks down a problem into sub problems.

### Flowcharts ([[Chapter 5]])
1. What is specified of the program? Input / output
2. Analyze the program. What mathmatical operations do we need?

A Flowchart specifies the individual steps necessary to complete the program.