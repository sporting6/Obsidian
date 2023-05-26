# $ What is an Operating System Kernel?

An operating system kernel is the central component of an operating system that serves as a core bridge between software applications and the underlying hardware of a computer system. It manages system resources, provides essential services, and facilitates communication between software and hardware.

The kernel manages various aspects of the system, including process management, memory management, and input/output operations. It schedules and coordinates the execution of processes, ensuring fair allocation of CPU time and efficient multitasking. Additionally, it manages memory by allocating and deallocating memory to processes, optimizing memory usage, and providing memory protection.

The kernel also handles input/output operations, allowing software applications to interact with peripheral devices such as disks, printers, and networks. It provides device drivers as translators between the hardware and the software, enabling communication and data transfer.


# $ What Can My Kernel do?

### Memory Paging

My OS kernel uses page tables to convert virtual memory addresses to physical memory addresses. The page table serves as a map between the two address spaces. When a program accesses virtual memory, the kernel consults the page table for the corresponding physical address. If a valid mapping exists, the operation is directed to the correct physical location. If not, a process called page fault handling is triggered. This involves retrieving data from secondary storage and allocating new physical memory. The page table is updated with the new mapping, enabling future accesses to be translated directly to the physical memory location. This mechanism allows efficient memory management and supports multitasking across different processes.

![[Screen Shot 2023-05-26 at 3.33.08 PM.png]]
(Oppermann)

### Printing To The VGA Buffer

A VGA (Video Graphics Array) buffer, also known as a frame buffer, is a region of memory in a computer's graphics system that stores the pixel data necessary to generate images on a display. It acts as an intermediary between the computer's software and the physical display hardware, allowing for efficient rendering and manipulation of graphical content.

To write to a VGA buffer, the software interacts with the memory addresses reserved for the frame buffer. Each memory location within the buffer corresponds to a pixel on the display. By modifying the pixel values stored in the buffer, the software can control the appearance and arrangement of visual elements on the screen.

### Interrupts and Taking Keyboard Inputs

Interrupts are essential mechanisms in computer systems that handle immediate events, like keyboard inputs. When a key is pressed, the keyboard controller triggers a hardware interrupt to notify the CPU. The CPU pauses its current task and executes an interrupt handler specifically designed for keyboard input. The handler captures the keystrokes and prints them to the VGA buffer. The CPU then resumes its previous task or switches to another task, allowing software to periodically read and process the stored keystrokes from the buffer. Interrupts enable efficient and timely management of keyboard inputs in computer systems.

### Manage Memory

My kernal manages dynamic memory by using a simple linked list allocator. For more information read the How Does My Kernal Manage Memory section.


# $ What is Hardware and Software?

Hardware refers to the physical components of a computer system, such as the motherboard, CPU, memory modules, storage devices, input/output devices, and peripherals. It encompasses the tangible, electronic, and mechanical parts that form the foundation of a computer system. Hardware components are responsible for executing instructions and performing calculations. They provide the necessary interfaces for communication with other hardware, firmware, and software components.

Firmware sits between hardware and software. It is a type of software that is embedded into hardware devices or components during the manufacturing process. Firmware provides low-level control and instructions specific to the hardware it is installed on. It is typically stored in non-volatile memory, such as ROM (read-only memory) or flash memory which doesn't need constant power to be stored. Firmware controls hardware devices' basic functionalities and initialization processes, enabling them to work seamlessly with the rest of the computer system. Examples of firmware include the BIOS (**B**asic **I**nput/**O**utput **S**ystem) in a computer.

Software refers to the programs, data, and instructions that run on a computer system. It is a collection of codes and algorithms written in programming languages that provide specific functionalities and services to users. Software can be classified into system software (such as operating systems and device drivers) that manages and controls the hardware resources and application software (such as word processors, web browsers, and games) that are designed for specific tasks or user requirements. Software is typically stored in non-volatile storage devices such as hard drives or solid-state drives and is loaded into the computer's memory for execution.

# $ What is the Main Hardware in a computer?

-  **Central Processing Unit (CPU)**: The CPU is the "brain" of the computer that executes instructions, performs calculations, and manages data processing. It consists of the arithmetic logic unit (ALU), control unit, registers, and cache.

	- Arithmetic Logic Unit (ALU): The ALU is responsible for performing arithmetic (such as addition, subtraction, multiplication, and division) and logical operations (such as AND, OR, and NOT) on data. It carries out calculations and comparisons for processing instructions and manipulating data within the CPU.
	
	- Control Unit (CU): The Control Unit manages the execution of instructions within the CPU. It fetches instructions from memory, decodes them, and controls the flow of data between different CPU components. The Control Unit also coordinates the timing and sequencing of instructions, ensuring that they are executed in the correct order.
	
	- Registers: Registers are small, high-speed memory units located within the CPU. They store data and instructions that are currently being processed by the CPU. Registers provide quick access to data, allowing for faster execution of instructions. Common types of registers include the program counter (PC), which holds the memory address of the next instruction to be fetched, and general-purpose registers (like the accumulator) used for various calculations and data manipulation.

![[Pasted image 20230526152643.png]]
(Gayde)

-  **Random Access Memory (RAM)**: RAM is the primary memory of a computer system that stores data and instructions temporarily while the CPU is actively using them. It provides fast access to data, allowing for quick read and write operations.

-  **Motherboard**: The motherboard is the main circuit board of a computer system. It connects and houses various components, including the CPU, memory modules, expansion cards, and other essential peripherals

# $ What is Memory?

Memory(**RAM**) stores data, instructions, and program code for current or future use by the CPU (Central Processing Unit). It is a crucial part of a computer's architecture and plays a vital role in the overall performance and functionality of a system. There are two different ways memory is stored on your computer.

1.  Stack: The stack is a region of memory used for storing local variables and function call information. It is managed by the CPU and operates in a Last-In, First-Out (LIFO) manner. When a function is called, its local variables and return address are pushed onto the stack, creating a new stack frame. As functions complete, their stack frames are removed from the top of the stack. The stack is typically faster to access and has a fixed size determined during program compilation.

![[Screen Shot 2023-05-26 at 3.35.23 PM.png]]

3. Heap: The heap is a region of memory used for dynamic memory allocation. It is a pool of memory where objects and data can be allocated and deallocated as needed. Unlike the stack, memory allocation in the heap is not always managed automatically. Developers sometimes must explicitly request memory from the heap using functions like `alloc()` and are responsible for freeing it when no longer needed using `dealloc()`.  Some languages, like java, have a built in heap manager called `garbage collection` that will automatically free memory when it is no longer needed. The heap provides greater flexibility in memory management but can be slower to access and requires manual memory management to avoid memory leaks and fragmentation.

# $ How Does My Kernel Manage Memory?

Dynamic memory is memory allocated at runtime for storing data in a program. An allocator is needed to manage dynamic memory by tracking available memory, allocating memory blocks, and ensuring efficient memory utilization. It enables programs to handle varying data requirements and create dynamic data structures.

### Bump Allocator:

The bump allocator is a straightforward and efficient method for managing memory. It works by keeping track of a pointer called `next`, which points to the beginning of unused memory. When a new block of memory is needed, the allocator moves `next` to the new beginning of the unused memory.

![[Pasted image 20230526115218.png]]
(Oppermann)

However, there is a limitation to this approach. Since the `next` pointer only moves forward, it cannot reuse memory that has been deallocated. This means that when the allocator reaches the end of the available memory in the heap, it runs out of space to allocate any more memory. As a result, the following allocation request will result in an out-of-memory error.

![[Screen Shot 2023-05-26 at 1.52.05 PM.png]]
(Oppermann)

To mitigate this issue, an allocation counter can be implemented. This counter increases by one when memory is allocated and decreases by one when memory is deallocated. This allows the bump allocator to reset back to the beginning of the available memory when the counter reaches zero. However, there is still a possibility of encountering an out-of-memory error if the allocation counter is greater than one when it reaches the end of the available memory.

To fix some of these problems I used a Linked List Allocator Instead.

### Linked List Allocator

A simple linked list allocator is alot like a bump allocator. It uses a technique called a linked list, which is like a chain of blocks, to allocate and deallocate memory as needed.

Initially, the entire memory block is treated as a single free block, and a linked list node is created to represent it. This node contains information regarding the block's size and a reference that points to the next node in the list.

![[Screen Shot 2023-05-26 at 1.48.39 PM.png]]
(Oppermann)

Upon receiving a memory allocation request, the allocator traverses the linked list, starting at the head node and following the references to the other nodes, to locate a suitable free block that can accommodate the requested size. Once found, the allocator divides the free block into two segments: one for the allocated memory and another for the remaining unused memory. The allocated block is marked as "in-use," while the unused block is transformed into a new free block by updating it with its own linked list node.

When memory is no longer needed and is deallocated, the allocator marks that block as free again. It then creates a new node that the head points towards. Then, the new node points to the previos node the head was pointing towards to complete the list:

![[Screen Shot 2023-05-26 at 1.51.04 PM.png]]
(Oppermann)

While a linked list allocator offers flexibility in managing memory allocation and deallocation, it may encounter fragmentation issues over time if memory is allocated and deallocated irregularly, leading to a fragmented linked list of free blocks like shown:

![[Screen Shot 2023-05-26 at 1.55.43 PM.png]]
(Oppermann)

A a simple linked list allocator provides a fundamental yet effective approach to dynamically manage memory allocation. It strikes a balance between simplicity and memory utilization efficiency, enabling variable-sized memory requests to be handled proficiently.

# $ Limitations of My Kernel

My kernel has many limitations that I will improve on in the future, the most promenent being:
- Cannot compile programs
- Fragmentable heap management
- Lack of features


# $ My Expert:

Jack Maloney is a software engeneer, and my brother. He helped me debug, implement new features, and understand some concepts in computer architecture.

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



