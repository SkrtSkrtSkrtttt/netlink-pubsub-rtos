# Netlink Pub/Sub RTOS

This project implements a multi-stage real-time publish-subscribe (pub/sub) system in Linux using Netlink sockets, kernel modules, and userspace multithreading. It enables dynamic communication between multiple producer and consumer processes through the kernel using efficient IPC and thread-safe design patterns.

## Objective

- Design a pub/sub system that routes messages from publishers to subscribers via a Linux kernel module.
- Use Netlink sockets for communication between userspace and kernel space.
- Implement multi-threaded producers and consumers in userspace.
- Support dynamic registration and message forwarding between processes.

## Project Stages

### Part 1: Producers, Consumers, Mutexes, and Threads

- Implement a basic producer-consumer system using C and POSIX threads.
- Use mutexes to avoid race conditions and segmentation faults.
- Develop producer and consumer functions that push/pull from a shared buffer.

### Part 2: Basic Netlink Pub/Sub Network

- Establish Netlink communication between one userspace process and a kernel module.
- Extend the system to support one publisher and two subscriber processes.
- Use a 1-byte identifier in the message payload to distinguish between publisher and subscriber roles.
- Kernel receives messages from the publisher and forwards them to subscribers.

### Part 3: Kernel Linked Lists and Userspace Threads

- Support a dynamic number of processes using kernel linked lists (`list_head`).
- Maintain a list of active publishers and subscribers by PID.
- Implement two threads per userspace process: one for sending (publishing) and one for receiving (subscribing).
- Ensure proper memory deallocation when the kernel module is removed.

## Technologies Used

- C (Userspace & Kernel Module)
- Netlink Sockets
- POSIX Threads (`pthread`)
- Linux Kernel Programming (Makefiles, `list_head`)
- Virtual Machine / Ubuntu Environment

## System Architecture

- **Userspace**:
  - Multithreaded client program (input handler + listener)
  - Registers with the kernel as a publisher or subscriber
- **Kernel Module**:
  - Tracks all processes using linked lists
  - Forwards messages to subscribers based on sender identity

## Usage

1. Compile and insert the kernel module
2. Run user program and select role (publisher or subscriber)
3. Publishers send messages using stdin
4. Subscribers print messages forwarded by the kernel

## References

- [Netlink Sockets Overview – Linux Journal](https://www.linuxjournal.com/article/7356)
- [Kernel Linked Lists – Kernel Newbies](https://kernelnewbies.org/FAQ/LinkedLists)
- [Pthreads in C – GeeksforGeeks](https://www.geeksforgeeks.org/multithreading-c-2/)

## Author

- Naafiul Hossain

