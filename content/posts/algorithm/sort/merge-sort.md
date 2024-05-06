---
author: "Mohammad Mustakim Hassan"
title: "Merge Sort"
date: "2023-05-06"
description: "Notes on Merge Sort"
tags: ["algorithm", "sort", "recursive"]
ShowToc: true
---

## Introduction
Merge Sort is a divide-and-conquer sorting algorithm that divides the input array into two halves, recursively sorts the halves, and then merges them to produce a sorted array.

## Algorithm
1. Divide the unsorted array into two halves.
2. Recursively sort each half.
3. Merge the sorted halves to produce a single sorted array.

## Example
Suppose we have an unsorted array: [5, 3, 8, 2, 7].
1. Start with the second element (3) and compare it with the first element (5). Since 3 < 5, shift 5 to the right.
   Result: [3, 5, 8, 2, 7]
2. Compare 3 with the previous elements (none) and insert it at the beginning.
   Result: [3, 5, 8, 2, 7]
3. Move to the next element (8) and insert it into its correct position among the sorted elements.
   Result: [3, 5, 8, 2, 7]
4. Repeat the process for the remaining elements (2 and 7) to obtain the sorted array: [2, 3, 5, 7, 8].

## JavaScript Implementation
```javascript
function mergeSort(arr) {
    if (arr.length <= 1) {
        return arr;
    }
    
    const mid = Math.floor(arr.length / 2);
    const leftHalf = arr.slice(0, mid);
    const rightHalf = arr.slice(mid);
    
    return merge(mergeSort(leftHalf), mergeSort(rightHalf));
}

function merge(left, right) {
    let result = [];
    let leftIndex = 0;
    let rightIndex = 0;
    
    while (leftIndex < left.length && rightIndex < right.length) {
        if (left[leftIndex] < right[rightIndex]) {
            result.push(left[leftIndex]);
            leftIndex++;
        } else {
            result.push(right[rightIndex]);
            rightIndex++;
        }
    }
    
    return result.concat(left.slice(leftIndex)).concat(right.slice(rightIndex));
}

// Example usage
const unsortedArray = [5, 3, 8, 2, 7];
const sortedArray = mergeSort(unsortedArray);
console.log('Sorted Array:', sortedArray);
// Sorted Array: [2, 3, 5, 7, 8]
```

## Complexity Analysis
The time complexity of Merge Sort is O(n log n) for all cases, where n is the number of elements in the array. 
The space complexity is O(n) due to the additional space required for merging.

## Advantage and Disadvantage

### Advantage:
- **Efficient for Large Data Sets**: Merge Sort is highly efficient and performs well for large datasets due to its O(n log n) time complexity.
- **Stable Sorting**: Merge Sort is a stable sorting algorithm, preserving the relative order of equal elements.
- **Divide-and-Conquer Strategy**: Its divide-and-conquer strategy allows parallelization and efficient memory usage.

### Disadvantage:
- **Additional Memory Usage**: Merge Sort requires additional memory space for the merging process, leading to higher space complexity.
- **Not In-Place Sorting**: Merge Sort does not sort the array in-place, requiring additional memory space for the merging process.
- **Complexity in Linked Lists**: In linked lists, merge operations may require extra care, affecting the overall efficiency.

## Application
Merge Sort finds applications in various scenarios where stable and efficient sorting of large datasets is required. Some common applications include:
- **External Sorting**: Sorting large datasets that cannot fit into main memory.
- **Sorting Linked Lists**: Sorting linked lists efficiently where random access is not efficient.
- **Parallel Computing**: Merge Sort's divide-and-conquer strategy allows for parallel implementations, making it suitable for parallel computing environments.
- **Inversion Counting**: Merge Sort is used in counting inversions in an array, which is useful in various applications like computational biology and data analysis.
