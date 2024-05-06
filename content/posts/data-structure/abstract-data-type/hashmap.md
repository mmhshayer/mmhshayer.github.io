---
author: "Mohammad Mustakim Hassan"
title: "Hashmap Data Structure"
date: "2023-05-06"
description: "Notes on Hashmap Data Structure"
tags: ["data structure", "hashmap"]
ShowToc: true
draft: true
---

## Introduction
A hashmap is a data structure that stores key-value pairs. It provides efficient insertion, deletion, and retrieval operations by using a hash function to map keys to indexes in an underlying array.

## Operations
Hashmaps support various operations, including:
- **Insertion**: Adding key-value pairs to the hashmap.
- **Deletion**: Removing key-value pairs from the hashmap.
- **Retrieval**: Accessing the value associated with a given key.
- **Search**: Checking if a key exists in the hashmap.

## Example
Consider a hashmap representing the ages of people:
```javascript
const ages = new Map();
```

**Insertion**: Adding key-value pairs to the hashmap:
```javascript
ages.set('Alice', 30);
ages.set('Bob', 25);
ages.set('Charlie', 35);
```

**Deletion**: Removing key-value pairs from the hashmap:
```javascript
ages.delete('Bob');
```

**Retrieval**: Accessing the value associated with a given key:
```javascript
const aliceAge = ages.get('Alice'); // Output: 30
```

**Search**: Checking if a key exists in the hashmap:
```javascript
const hasBob = ages.has('Bob'); // Output: false
```

## Advantage
- **Fast Lookup**: Hashmaps offer constant-time average-case performance for insertion, deletion, and retrieval operations, making them suitable for applications requiring fast lookups.
- **Flexible Key Types**: Hashmaps can accept a wide range of key types, including strings, integers, and objects, providing flexibility in data modeling.
- **Dynamic Size**: Hashmaps can dynamically resize to accommodate a varying number of key-value pairs, adapting to changing data requirements.

## Disadvantage
- **Space Complexity**: Hashmaps may consume more memory than other data structures, especially when dealing with collisions or underutilized capacity.
- **Unordered Output**: The order of key-value pairs in a hashmap may not be predictable or consistent, which can be undesirable in certain scenarios requiring ordered data.

## Application
Hashmaps find applications in various scenarios, including:
- **Data Caching**: Storing frequently accessed data to improve performance by avoiding redundant computations or database queries.
- **Symbol Tables**: Implementing symbol tables in compilers and interpreters to map identifiers to their corresponding attributes or memory locations.
- **Distributed Systems**: Distributing data across multiple nodes in a distributed system for efficient data retrieval and load balancing.
- **Algorithm Optimization**: Optimizing algorithms by using hashmaps to store intermediate results or to track visited states in graph traversal algorithms.

## Example JavaScript Implementation
```javascript
class HashMap {
    constructor() {
        this.size = 0;
        this.map = {};
    }

    insert(key, value) {
        this.map[key] = value;
        this.size++;
    }

    delete(key) {
        if (this.map.hasOwnProperty(key)) {
            delete this.map[key];
            this.size--;
        }
    }

    retrieve(key) {
        return this.map[key];
    }

    search(key) {
        return this.map.hasOwnProperty(key);
    }
}

// Example usage
const myMap = new HashMap();
myMap.insert("name", "John");
myMap.insert("age", 30);
myMap.insert("city", "New York");

myMap.delete("age");

console.log(myMap.retrieve("name")); // Output: John
console.log(myMap.search("age")); // Output: false
```
