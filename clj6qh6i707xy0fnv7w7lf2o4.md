---
title: "Introduction to Operating Systems"
seoTitle: "Introduction to Operating Systems"
seoDescription: "This blog makes you understand what operating systems are and what are their responsibilities and how they function."
datePublished: Thu Jun 22 2023 05:59:39 GMT+0000 (Coordinated Universal Time)
cuid: clj6qh6i707xy0fnv7w7lf2o4
slug: introduction-to-operating-systems
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1687412651086/2d738deb-8bde-4b5b-9864-db87d94870e7.png
tags: operating-system, opensource, computer-science

---

An operating system is a program that manages computer hardware. It also provides a basis for application programs and acts as an intermediate between the user and computer hardware. It provides a great and convenient user experience to perform a task.

The hardware block represents all the electronic devices that are in computers like RAM, Motherboard, etc. The O.S is installed over this hardware and the application block refers to various applications that we use in day-to-day life like a calculator, excel, web browser, etc. These applications are built over O.S and the O.S act as a platform to build these applications.

# classifications of operating systems

1. Batch OS: A batch operating system is designed to process a large number of similar jobs without any user interaction. It works on a first-come, first-serve basis.
    
2. Distributed OS: A distributed operating system is a network of computers that work together as a single system. The system appears to users as a single computing machine, even though it is actually composed of multiple independent computers.
    
3. Multitasking OS: A multitasking operating system allows multiple tasks or programs to run concurrently on a computer, allowing users to switch between them seamlessly.
    
4. Network OS: A network operating system is designed to manage and operate computer networks. It allows multiple computers to communicate with each other and share resources like printers and files.
    
5. Real-Time OS: A real-time operating system is designed to respond to an event within a guaranteed time frame. These systems are commonly used in embedded systems, robotics, and other time-critical applications.
    
6. Mobile OS: A mobile operating system is designed to run on mobile devices like smartphones and tablets. These operating systems are optimized for touchscreens and support a wide range of applications and connectivity options. Examples of mobile operating systems include Android and iOS.
    

# Popularly known O.S

* Windows: Windows is a multitasking operating system that is designed to run on personal computers and servers.
    
* MacOS: MacOS is an operating system that is designed to run on Apple's Macintosh line of computers. It is a multitasking operating system that is known for its user-friendly interface and high-end hardware.
    
* Linux: Linux is an open-source operating system that can be used on a wide range of devices, from servers to smartphones. It is a multitasking operating system that is known for its stability, security, and flexibility.
    
* Android: Android is a mobile operating system that is designed to run on smartphones and tablets. It is a multitasking operating system that is known for its open-source nature, flexibility, and large app ecosystem.
    

Therefore, Windows, MacOS, Linux, and Android are all examples of multitasking operating systems.

## **Functions of the Operating System**

* **Processor Management:** An operating system manages the processor’s work by allocating various jobs to it and ensuring that each process receives enough time from the processor to function properly.
    
* **Memory Management:** An operating system manages the allocation and deallocation of the memory to various processes and ensures that the other process does not consume the memory allocated to one process.
    
* **Device Management:** There are various input and output devices. An OS controls the working of these input-output devices. It receives the requests from these devices, performs a specific task, and communicates back to the requesting process.
    
* **File Management:** An operating system keeps track of information regarding the creation, deletion, transfer, copy, and storage of files in an organized way. It also maintains the integrity of the [data](https://www.mygreatlearning.com/blog/types-of-data/) stored in these files, including the file directory structure, by protecting against unauthorized access.
    
* **Security:** The operating system provides various techniques which assure the integrity and confidentiality of user data. The following security measures are used to protect user data:
    
    * Protection against unauthorized access through login.
        
    * Protection against intrusion by keeping Firefall active.
        
    * Protecting the system memory against malicious access.
        
    * Displaying messages related to system vulnerabilities.
        
* **Error Detection:** From time to time, the operating system checks the system for any external threat or malicious software activity. It also checks the hardware for any type of damage. This process displays several alerts to the user so that the appropriate action can be taken against any damage caused to the system.
    
* **Job Scheduling:** In a multitasking OS where multiple programs run simultaneously, the operating system determines which applications should run in which order and how time should be allocated to each application.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679744630745/39f18c0c-e389-4fc2-812a-07287cab9e9c.png align="center")

## **Features of Operating Systems**

Here is a list of some important features of operating systems:

1. Provides a platform for running applications
    
2. Handles memory management and CPU scheduling
    
3. Provides file system abstraction
    
4. Provides networking support
    
5. Provides security features
    
6. Provides user interface
    
7. Provides utilities and system services
    
8. Supports application development
    

## **Components of the Operating System**

Now to perform the functions mentioned above, the operating system has two components:

* Shell
    
* Kernel
    

Shell handles user interactions. It is the outermost layer of the OS and manages the interaction between the user and the operating system by:

* Prompting the user to give input
    
* Interpreting the input for the operating system
    
* Handling the output from the operating system.
    

Shell provides a way to communicate with the OS by either taking input from the user or the shell script. A shell script is a sequence of system commands that are stored in a file.

The kernel is the core component of an operating system for a computer (OS). All other components of the OS rely on the core to supply them with essential services. It serves as the primary interface between the OS and the hardware and aids in the control of devices, networking, file systems, and process and memory management.

# Process scheduling

Process scheduling is the mechanism used by an operating system to manage the allocation of system resources, particularly the CPU, to running processes.

When a computer system has multiple processes running simultaneously, the operating system must decide which process should be given access to the CPU at any given time. This decision is made by the process scheduler, which selects the next process to run from a queue of waiting processes.

There are various scheduling algorithms that the operating system can use to make this decision. These algorithms differ in their approach to selecting the next process to run and may prioritize different factors such as fairness, responsiveness, or throughput.

Some common scheduling algorithms include:

1. First-Come, First-Served (FCFS): The operating system executes processes in the order they arrive in the system queue.
    
2. Round Robin: Each process is given a small amount of time to execute before being interrupted and replaced with the next process in the queue. This approach ensures that no process monopolizes the CPU for too long.
    
3. Shortest Job First (SJF): The operating system prioritizes processes with the shortest expected execution time.
    
4. Priority-based: Processes are assigned a priority level based on their importance, and the scheduler executes processes with the highest priority first.
    
5. Multi-level Queue: Processes are divided into separate queues based on their priority, and each queue has its own scheduling algorithm.
    

The process scheduler plays a crucial role in ensuring that the operating system uses resources efficiently and that processes are executed in a timely manner. By selecting the appropriate scheduling algorithm, the operating system can balance competing demands for system resources and provide a responsive and efficient computing environment

Process synchronization is the coordination of activities between multiple concurrent processes in a computer system. When multiple processes are executing concurrently, they may need to access shared resources, such as memory or I/O devices, which can lead to issues such as race conditions, deadlocks, and data inconsistencies. Process synchronization aims to prevent these issues by ensuring that the processes access shared resources in a controlled and coordinated manner.

One common approach to process synchronization is the use of synchronization primitives, such as semaphores, mutexes, and monitors. These primitives provide mechanisms for processes to communicate and coordinate with each other, ensuring that only one process can access a shared resource at a time and preventing data inconsistencies and race conditions.

For example, imagine two concurrent processes that both need to access a shared resource, such as a printer. Without proper synchronization, both processes may attempt to access the printer at the same time, leading to issues such as incomplete or garbled printouts. However, by using synchronization primitives such as semaphores, the processes can coordinate their access to the printer, ensuring that only one process accesses the printer at a time and preventing data inconsistencies.

# Process synchronization

Process synchronization is the coordination of activities between multiple concurrent processes in a computer system. When multiple processes are executing concurrently, they may need to access shared resources, such as memory or I/O devices, which can lead to issues such as race conditions, deadlocks, and data inconsistencies. Process synchronization aims to prevent these issues by ensuring that the processes access shared resources in a controlled and coordinated manner.

One common approach to process synchronization is the use of synchronization primitives, such as semaphores, mutexes, and monitors. These primitives provide mechanisms for processes to communicate and coordinate with each other, ensuring that only one process can access a shared resource at a time and preventing data inconsistencies and race conditions.

For example, imagine two concurrent processes that both need to access a shared resource, such as a printer. Without proper synchronization, both processes may attempt to access the printer at the same time, leading to issues such as incomplete or garbled printouts. However, by using synchronization primitives such as semaphores, the processes can coordinate their access to the printer, ensuring that only one process accesses the printer at a time and preventing data inconsistencies.

Process synchronization is a critical aspect of concurrent programming and is used in a wide range of applications, including operating systems, distributed systems, and real-time systems. By ensuring that processes can access shared resources in a controlled and coordinated manner, process synchronization helps to improve the reliability, performance, and correctness of concurrent programs.

# Process management

Process management is a critical component of operating systems that involves managing the lifecycle of processes running on a computer. A process is an instance of a running program, and process management includes creating and starting new processes, managing their execution, and terminating them when they are no longer needed.

The primary functions of process management include:

1. Process creation: This involves creating new processes from existing ones or starting new processes from executable files. The operating system allocates resources, such as memory and CPU time, to the new process and sets up the environment for the process to run.
    
2. Process scheduling: This involves allocating CPU time to running processes and managing the order in which processes execute. The operating system uses a process scheduler to manage the allocation of CPU time to running processes and ensure that they operate correctly and efficiently.
    
3. Process synchronization: This involves coordinating the activities of concurrent processes to ensure that they do not interfere with each other. Synchronization mechanisms, such as semaphores, mutexes, and monitors, are used to prevent issues such as race conditions and deadlocks.
    
4. Process communication: This involves allowing processes to communicate with each other and share data. Inter-process communication mechanisms, such as pipes, shared memory, and message queues, are used to enable processes to exchange information and cooperate with each other.
    
5. Process termination: This involves stopping processes when they are no longer needed or when they have completed their tasks. The operating system deallocates resources, such as memory and file handles, associated with the terminated process and cleans up any remaining data structures.
    

Overall, process management is a critical component of operating systems, and it plays a vital role in ensuring that applications and system processes operate correctly, efficiently, and safely.

# Memory management

Memory management is a critical function of modern operating systems, which is responsible for managing the allocation and deallocation of memory resources to processes. The memory management subsystem of the operating system is responsible for the following tasks:

1. Memory allocation: The memory management subsystem is responsible for allocating memory to processes as they request it. It manages a pool of memory resources and assigns portions of this pool to processes as needed. Memory allocation is typically done using one of several memory allocation algorithms, such as first-fit, best-fit, or worst-fit.
    
2. Memory protection: The memory management subsystem ensures that each process can only access its allocated memory, preventing processes from accessing memory they do not own. This is done by setting up memory protection mechanisms such as page tables and virtual memory systems.
    
3. Memory mapping: The memory management subsystem provides mechanisms for processes to access shared memory resources, such as shared libraries or shared memory segments. This is done by mapping the shared memory resources into the address space of each process that needs access to them.
    
4. Memory swapping: The memory management subsystem provides mechanisms for swapping memory pages in and out of physical memory to disk. This is done to free up physical memory when it becomes scarce and to allow processes to access larger memory spaces than the amount of physical memory available.
    
5. Memory fragmentation: The memory management subsystem tries to minimize memory fragmentation, which occurs when memory is allocated and deallocated in a non-contiguous manner, leaving small unused gaps in the memory pool. Fragmentation can lead to inefficient use of memory and can cause issues such as memory leaks.
    

Overall, memory management is a critical function of modern operating systems and plays a vital role in ensuring the efficient and effective use of system resources.

# Logical address and Physical address

The logical address is a virtual address that is used by a process to refer to a memory location. Logical addresses are generated by the CPU, and they are translated to physical addresses by the memory management unit (MMU) before the actual memory access takes place. Each process has its own set of logical addresses, and these addresses are mapped to physical addresses by the operating system.

The physical address, on the other hand, is a memory address that directly refers to a physical location in memory. Physical addresses are used by the memory management hardware to locate the actual physical memory location that stores the data. The physical address is the actual location of the data in the computer's memory.

The translation of logical addresses to physical addresses is done by the memory management unit (MMU) using a technique called virtual memory. Virtual memory allows the operating system to use more memory than is physically available in the computer by creating a virtual memory space that is larger than the physical memory space. Logical addresses are used to access this virtual memory space, and the MMU translates them to physical addresses when data is actually accessed.

Overall, logical addresses and physical addresses are two important concepts in computer memory management. Logical addresses are used by processes to refer to memory locations, while physical addresses are used by the memory management hardware to locate the actual physical memory location that stores the data.

# Contiguous and Partitioned memory

Contiguous and partitioned memory are two different approaches to memory management in operating systems.

Contiguous memory management is an approach where the entire physical memory is treated as a single contiguous block of memory. In this approach, each process is assigned a contiguous block of physical memory, which means that the memory allocated to a process is a contiguous chunk of memory. This approach is simple to implement, but it suffers from fragmentation when there is a lot of memory allocation and deallocation.

Partitioned memory management, on the other hand, is an approach where the physical memory is divided into fixed-sized partitions, and each partition is assigned to a process. In this approach, each process is allocated one or more partitions of memory, and the remaining partitions are kept available for future use. This approach reduces fragmentation and improves memory utilization but requires additional overhead for managing the partitioning of memory.

In modern operating systems, partitioned memory management is more commonly used. It allows the operating system to allocate memory more efficiently and to prevent processes from interfering with each other's memory. Partitioned memory management can be further divided into two subtypes: fixed partitioning and dynamic partitioning.

Fixed partitioning is an approach where the physical memory is divided into fixed-sized partitions, and each partition is allocated to a process. In contrast, dynamic partitioning is an approach where the memory is divided into variable-sized partitions, and each process is allocated only the memory it needs. Dynamic partitioning is more flexible than fixed partitioning, but it requires additional overhead to manage the variable-sized partitions.

**If you find value in this content, don't forget to like and comment on the blog post. Feel free to follow me on** [**Twitter**](https://twitter.com/dhanuks26)**,** [**GitHub**](https://github.com/DhanushGowda26)**, and** [**Hashnode**](https://dhanushks.hashnode.dev/) **for more valuable content. Stay tuned for future articles where we explore more such content.**

**Thank you so much for taking the time to read my long blog. I truly appreciate your effort and interest.**

**If you have any further questions or need additional information, please don't hesitate to ask. 😊**