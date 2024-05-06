---
author: "Mohammad Mustakim Hassan"
title: "Linked List Data Structure"
date: "2023-05-06"
description: "Notes on Linked List Data Structure"
tags: ["data structure", "linked list"]
ShowToc: true
draft: true
---

## Introduction
A linked list is a linear data structure consisting of a sequence of elements, called nodes, where each node contains a data value and a reference (pointer) to the next node in the sequence. Unlike arrays, linked lists do not store elements in contiguous memory locations.

## Operations
Linked lists support various operations, including:
- **Insertion**: Inserting elements at the beginning, end, or any position in the linked list.
- **Deletion**: Removing elements from the linked list.
- **Traversal**: Iterating over all elements of the linked list to perform certain operations.
- **Search**: Searching for elements in the linked list.

## Example
Consider a singly linked list representing a sequence of integers: 
```javascript
const scores = [85, 92, 78, 95, 88];
const thirdScore = scores[2]; // Output: 78
```
**Insertion**: If we want to insert the element 15 at the beginning, we create a new node with value 15 and point it to the current head:
```javascript
scores.push(90);
console.log(scores); // Output: [85, 92, 78, 95, 88, 90]
```
**Deletion**: If we want to delete the node with value 7, we update the next reference of the previous node to skip the node with value 7:
```javascript
scores.splice(1, 1);
console.log(scores); // Output: [85, 78, 95, 88, 90]
```
**Traversal**: We can traverse the linked list to print all elements:
```javascript
let sum = 0;
for (let i = 0; i < scores.length; i++) {
    sum += scores[i];
}
const average = sum / scores.length;
console.log(average); // Output: 87.6
```
**Search**: To find if the value 5 exists in the linked list, we traverse the list until we find the node with value 5.
```javascript
const index = scores.indexOf(88);
console.log(index); // Output: 3 (index of score 88)
```

## Advantage
- **Dynamic Size**: Linked lists can dynamically grow and shrink in size, making them suitable for situations where the size of the data structure may change frequently.
- **Efficient Insertions and Deletions**: Insertions and deletions in linked lists can be performed in constant time, regardless of the size of the list.
- **Memory Efficiency**: Linked lists utilize memory more efficiently than arrays, as they only allocate memory for elements when needed.

## Disadvantage
- **Sequential Access**: Linked lists do not support random access to elements like arrays, requiring sequential traversal to access elements at specific positions.
- **Memory Overhead**: Linked lists require additional memory space for storing references to the next nodes, leading to higher memory overhead compared to arrays.
- **Complexity in Traversal**: Traversing a linked list may require more complex code compared to arrays, especially in languages without built-in iterator support.

## Application
Linked lists find applications in various scenarios, including:
- **Dynamic Memory Allocation**: Managing memory dynamically in languages like C and C++ using memory pools and free lists.
- **Implementation of Stacks and Queues**: Implementing stack and queue data structures using linked lists for efficient insertions and deletions.
- **Sparse Data Structures**: Representing sparse data structures efficiently, where most elements are empty or zero.
- **Polynomial Manipulation**: Storing and manipulating polynomial expressions in symbolic mathematics libraries.


## Example JavaScript Implementation
```javascript
class Node {
    constructor(data) {
        this.data = data;
        this.next = null;
    }
}

class LinkedList {
    constructor() {
        this.head = null;
    }

    insertAtBeginning(data) {
        const newNode = new Node(data);
        newNode.next = this.head;
        this.head = newNode;
    }

    insertAtEnd(data) {
        const newNode = new Node(data);
        if (!this.head) {
            this.head = newNode;
            return;
        }
        let current = this.head;
        while (current.next) {
            current = current.next;
        }
        current.next = newNode;
    }

    deleteNode(data) {
        if (!this.head) return;
        if (this.head.data === data) {
            this.head = this.head.next;
            return;
        }
        let current = this.head;
        while (current.next) {
            if (current.next.data === data) {
                current.next = current.next.next;
                return;
            }
            current = current.next;
        }
    }

    printList() {
        let current = this.head;
        while (current) {
            console.log(current.data);
            current = current.next;
        }
    }

    search(data) {
        let current = this.head;
        while (current) {
            if (current.data === data) {
                return true;
            }
            current = current.next;
        }
        return false;
    }
}

// Example usage
const linkedList = new LinkedList();
linkedList.insertAtEnd(3);
linkedList.insertAtEnd(7);
linkedList.insertAtEnd(11);
linkedList.insertAtEnd(5);
linkedList.insertAtEnd(9);

linkedList.insertAtBeginning(15);
linkedList.deleteNode(7);
linkedList.printList(); // Output: 15, 3, 11, 5, 9
console.log(linkedList.search(5)); // Output: true
```
