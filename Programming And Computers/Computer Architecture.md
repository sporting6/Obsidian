
## What is Computer Architecture?

Computer Architecture is a model or description of the structure of a computer. Computer architecture is the combination of [microarchitecture](#Microarchitecture) and [instruction set architecture (**ISA**)](##Instruction%20Set%20Architecture). The
[**ISA**](##Instruction%20Set%20Architecture) includes the [instructions](https://en.wikipedia.org/wiki/Instruction_set_architecture#Instructions "Instruction set architecture"), [execution model](https://en.wikipedia.org/wiki/Execution_model "Execution model"), [processor registers](https://en.wikipedia.org/wiki/Processor_register "Processor register"), address and data formats among other things. The [microarchitecture](#Microarchitecture) includes the constituent parts of the processor and how these interconnect and interoperate to implement the [**ISA**](##Instruction%20Set%20Architecture).

## Instruction Set Architecture

In general the [**ISA**](##Instruction%20Set%20Architecture) specifys the supported instructions/operations, data types, registers, managing main memory ([memory consistency](https://en.wikipedia.org/wiki/Memory_consistency), [addressing modes](https://en.wikipedia.org/wiki/Addressing_mode), [virtual memory](https://en.wikipedia.org/wiki/Virtual_memory)),  and the [I/O](https://en.wikipedia.org/wiki/Input/output). A device that exicutes the ISA(example is a [CPU](https://en.wikipedia.org/wiki/Central_processing_unit)) is called an Implementation. For more info click [here](https://en.wikipedia.org/wiki/Instruction_set_architecture)

## Microarchitecture

Computer Architecture also involves [Microarchitecture](https://en.wikipedia.org/wiki/Microarchitecture) or computer organization. This is how a specific [ISA](https://en.wikipedia.org/wiki/Instruction_set_architecture) Implemented on a  [CPU](https://en.wikipedia.org/wiki/Central_processing_unit). The Microarchitecture of a machine is normally shown in diagrams varying in detail. These diagrams discribe the interconnections between different parts of the machine. These componenets mostly range from single transistors to entire [arithmetic logic units](https://en.wikipedia.org/wiki/Arithmetic_logic_unit "Arithmetic logic unit"). These diagrams generally separate the [datapath](https://en.wikipedia.org/wiki/Datapath "Datapath") (where data is placed) and the [control path](https://en.wikipedia.org/w/index.php?title=Control_path&action=edit&redlink=1 "Control path (page does not exist)") (which can be said to steer the data).

## Logic gates

A [logic gate](https://en.wikipedia.org/wiki/Logic_gate)  computes a [boolean funtion](https://en.wikipedia.org/wiki/Boolean_function) on one or more bianary inputs hat produces a single binary output. The newest form of these gates are [transistors](https://en.wikipedia.org/wiki/Transistor) which use different voltages for the bianary inputs. They are the building blocks of digital computers. Originally logic gates where [vacuum tubes](https://en.wikipedia.org/wiki/Vacuum_tube) before they evolved into many things finally becoming the transistors we know today.

The ideal logic gate is a logic gate that has zero [rinse time](https://en.wikipedia.org/wiki/Rise_time) and unlimited [fan-out](https://en.wikipedia.org/wiki/Fan-out). The rinse time is the time it takes for a signal to change from low-voltage to high voltage.

In the real world, the primary way of building logic gates uses [diodes](https://en.wikipedia.org/wiki/Diode "Diode") or [transistors](https://en.wikipedia.org/wiki/Transistor "Transistor") acting as [electronic switches](https://en.wikipedia.org/wiki/Switch#Electronic_switches). These logic gates are made out of transistors in digital computers. These logic gates are used in almost everthing, including CPUs, RAM, GPUs, SSDs, and Chipsets. Today, most transistors are made of [MOSFET](https://en.wikipedia.org/wiki/MOSFET). 

There are different types of logic gates, these inlude the most basic NOT, AND, and OR gates. NOT gates invert the given input. AND gates only return TRUE if both inputs are TRUE and OR gates return TRUE if one of them are TRUE. There are also exclusive OR gates or XOR gates which are like OR gates but they return FALSE if both conditions are met. Every other gate can be constructed by NOR or NAND gates. NOR and NAND gates are like there normal counterparts but inverted.


