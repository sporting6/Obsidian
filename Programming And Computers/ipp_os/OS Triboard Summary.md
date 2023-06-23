# $ What is an Operating System Kernel?

- Core component bridging software and hardware
- Handles process management, scheduling, and multitasking
- Manages memory allocation
- Coordinates input/output operations with peripheral devices
- Provides device drivers for hardware and software communication


# $ What Can My Kernel do?



### Memory Paging

![[Memory Paging.png]]


.
.
.
.
.
.
.
.


### Interrupts and Taking Keyboard Inputs
- An interrupt is a signal for the CPU to handle an urgent task by invoking the appropriate interrupt handler
- These interrupts are generally sent by peripherals like your keyboard
- An example would be, when a key is pressed:
	1. An interrupt is sent to the CPU
	2. The CPU processes the interrupts and calls the appropriate interrupt handler
	3. The interrupt handler prints the given key to the screen

### Printing To The VGA Buffer

- The VGA buffer is a special buffer or area in memory that holds data that is then printed to the screen
- It is generally 25x80 ASCII characters
- Each bit references a different pixel on the screen
- The OS can then easily print to the screen by changing the data stored in the VGA buffer

![[VGA Buffer.png]]

### Manage Memory

My kernel manages dynamic memory by using a simple linked list allocator. For more information read the How Does My Kernel Manage Memory section.

.
.
.
.
.

# $ What is Hardware and Software?

### Hardware
- Physical components of a computer system
- Includes motherboard, CPU, memory modules, storage devices, etc
- Responsible for executing instructions and performing calculations

### Firmware
- Firmware is software embedded into hardware devices during manufacturing
- Semi-Permanent Software embedded in your hardware that provides low-level control and instructions
- Stored in non-volatile(retains data without power) memory like ROM(Read Only Memory) or flash memory
- Examples include BIOS(**B**asic **I**nput/**O**utput **S**ystem) that runs immediately when the computer is booted

.
.
.
.
.
.
.

### Software
- Programs, data, and instructions running on a computer
- Collection of codes and algorithms written in programming languages
- System software manages hardware resources (e.g., operating systems, device drivers)
- Application software is designed for specific tasks or user requirements (e.g., word processors, web browsers, games)
- Stored in non-volatile(retains data without power) storage devices and loaded into computer memory for execution



# $ What is the Main Hardware in a computer?

-  **Central Processing Unit (CPU)**: The CPU is the "brain" of the computer that executes instructions, performs calculations, and manages data processing. It consists of the arithmetic logic unit (ALU), control unit, registers, and cache.

![[CPU Diagram (Gayde).png]]
(Gayde)

-  **Random Access Memory (RAM)**: RAM is the primary memory of a computer system that stores data and instructions temporarily while the CPU is actively using them. It provides fast access to data, allowing for quick read and write operations.








# $ What is Memory?

- Stores data, instructions, and program code for CPU usage
- Temporary storage that is accessed randomly
- There are two main types of memory storage in a computer system

### Stack 
- Stack is a memory region for storing local variables and function call information
- Everything on the stack must have a know fixed size
- Managed by the CPU and operates in a Last-In, First-Out (LIFO) manner
- Stack is faster to access and has a fixed size determined when the program is compiled

### Heap
- Heap is a memory region for dynamic memory allocation
- Used as a pool for allocating and deallocating objects and data
- Memory allocation in the heap is not always managed automatically
- Heap provides flexibility in memory management but can be slower to access

![[Stack_Heap.png]]






# $ How Does My Kernel Manage Memory?

Dynamic memory is allocated at runtime for storing data. An allocator manages by tracking available space, and allocating memory blocks. It enables programs to handle varying data requirements and create dynamic data structures.





### Bump Allocator:

![[Bump Allocator.png]]

- The bump allocator can only move the the right
- It cannot reuse deallocated memory
- This leads to holes, or fragmentation, in the heap
- This causes poor memory efficiency
- When the allocator reaches the end of available memory, it triggers an out-of-memory error

To fix some of these problems I used a Linked List Allocator Instead.




### Linked List Allocator

- The linked list starts out by keeping track of the first block of memory through a pointer called the `head`
- A pointer is a value that "points" or references another value
- This node keeps track of the size and where the next node is.

![[Linked List.png]]

.
.
.
.
.
There are still some issues with my current linked list allocator
- It can experience fragmentation over time when its divided into many small different pieces.
- As a result, the allocator may struggle to find contiguous blocks of memory for larger allocation requests
- Strategies such as compaction or memory pooling can be employed to mitigate fragmentation and improve memory utilization

To solve these problems we can use a compactor:

![[Figure 8.png]]
.
.
.
.


# $ Limitations of My Kernel

My kernel has many limitations that I will improve on in the future, the most prominent being:
- Cannot compile programs
- Fragmentable heap management
- Lack of features


# $ My Expert:

My brother, Jack Maloney, who is a skilled software engineer, played a crucial role in this project. He helped me find and fix problems, add new features, and understand complex concepts about computer architecture. I am really grateful that he was there to support me throughout the project, and his contributions were a major factor in its success.








# $ Bibliography

Gayde, William. Graphic. Apr. 2020. Image.

Oppermann, Philipp. "Allocator Designs." Writing an OS in Rust, 20 Jan. 2020, 
	os.phil-opp.com/allocator-designs/. Accessed 4 June 2023.

Graphics, and Information.

---. "Heap Alloctation." Writing an OS in Rust, June 2019, 
	os.phil-opp.com/heap-allocation/. Accessed 4 June 2023.

Graphics and Information.

---. "Introduction to Paging." Writing an OS in Rust, 14 Jan. 2019,
	os.phil-opp.com/paging-introduction/. Accessed 26 May 2023.



