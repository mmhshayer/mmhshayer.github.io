---
author: "Mohammad Mustakim Hassan"
title: "Queue Data Structure"
date: "2023-05-06"
description: "Notes on Queue Data Structure"
tags: ["data structure", "queue"]
ShowToc: true
draft: true
---

## Introduction
A queue is a linear data structure that follows the First In, First Out (FIFO) principle. It consists of a collection of elements with two main operations: enqueue (adding an element to the rear) and dequeue (removing the front element).

## Operations
Queues support various operations, including:
- **Enqueue**: Adding an element to the rear of the queue.
- **Dequeue**: Removing the front element from the queue.
- **Peek**: Viewing the front element of the queue without removing it.
- **isEmpty**: Checking if the queue is empty.
- **Size**: Getting the number of elements in the queue.

## Example
Consider a queue representing a line of people waiting at a ticket counter:
```javascript
const ticketQueue = [];
```

**Enqueue**: Adding an element to the rear of the queue.
```javascript
ticketQueue.push('Alice');
ticketQueue.push('Bob');
ticketQueue.push('Charlie');
```

**Dequeue**: Removing the front element from the queue.
```javascript
const nextPerson = ticketQueue.shift(); // Output: 'Alice'
```

**Peek**: Viewing the front element of the queue without removing it.
```javascript
const firstPerson = ticketQueue[0]; // Output: 'Bob'
```

**isEmpty**: Checking if the queue is empty.
```javascript
const isEmpty = ticketQueue.length === 0; // Output: false
```

**Size**: Getting the number of elements in the queue.
```javascript
const queueSize = ticketQueue.length; // Output: 2
```

## Advantage
- **Simple and Efficient**: Queues are easy to implement and provide efficient operations for adding and removing elements, making them suitable for scenarios requiring a first-in, first-out data structure.
- **Order Preservation**: Queues preserve the order of elements, ensuring that the element inserted first is the first to be removed, which is essential in applications requiring ordered processing.
- **Concurrency Control**: Queues are used in concurrent programming for synchronization and communication between threads, facilitating safe data exchange and coordination.

## Disadvantage
- **Limited Access**: Queues offer limited access to elements, as only the front and rear elements are accessible for modification or removal. Accessing elements at arbitrary positions requires dequeuing and enqueuing elements until the desired element is reached.
- **Static Size**: In some implementations, queues may have a fixed size, leading to queue overflow errors when attempting to enqueue elements beyond the capacity.
- **Blocking Operations**: In certain scenarios, dequeuing elements from an empty queue or enqueuing elements to a full queue may block the execution flow, requiring additional handling or synchronization mechanisms.

## Application
Queues find applications in various scenarios, including:
- **Job Scheduling**: Managing job queues in operating systems and task schedulers to ensure fair resource allocation and efficient task execution.
- **Breadth-First Search**: Implementing breadth-first search algorithms in graph traversal for exploring nodes level by level, such as in shortest path finding and network routing.
- **Message Queues**: Facilitating communication between distributed systems, microservices, and components by using message queues for asynchronous message passing and event-driven architectures.
- **Buffering and Pipeline Processing**: Buffering input/output data streams and implementing pipeline processing in data processing systems to improve throughput and resource utilization.

## Example JavaScript Implementation
```javascript
class Queue {
    constructor() {
        this.items = [];
    }

    enqueue(element) {
        this.items.push(element);
    }

    dequeue() {
        if (this.isEmpty()) {
            return "Underflow";
        }
        return this.items.shift();
    }

    peek() {
        return this.isEmpty() ? "Queue is empty" : this.items[0];
    }

    isEmpty() {
        return this.items.length === 0;
    }

    size() {
        return this.items.length;
    }
}

// Example usage
const queue = new Queue();
queue.enqueue(10);
queue.enqueue(20);
queue.enqueue(30);

console.log(queue.peek()); // Output: 10
console.log(queue.dequeue()); // Output: 10
console.log(queue.size()); // Output: 2
console.log(queue.isEmpty()); // Output: false
```
