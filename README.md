# dsa-javascript

Notes taken on book "Data structures and algorithms in Javascript" by Jay Wengrow
Searching an Ordered Array

A concise guide to linear search, early stopping, and binary search in sorted arrays.

📘 Overview

This document explains how searching works in:

Classic (unsorted) arrays

Ordered (sorted) arrays

and how ordering allows us to use a dramatically faster algorithm: Binary Search.

1. 🔍 Linear Search (Classic Array)

In a classic array, the only way to find a value is to:

Start from the left

Check each element one by one

Stop when you find the value or reach the end

Example:

[17, 3, 75, 202, 80]

Searching for 22 requires checking all elements, because there’s no guaranteed order.

⏱ Time Complexity

Worst case: O(N)

Best case: O(1) (found at index 0)

2. 🔍 Linear Search (Ordered Array)

When the array is sorted, linear search can be optimized.

Example:

[3, 17, 75, 80, 202]

Searching for 22:

Check 3 → too small

Check 17 → too small

Check 75 → STOP! 75 > 22

Because the array is sorted, we know 22 cannot appear after a number larger than itself.

👉 This early-exit optimization reduces the number of comparisons.
JavaScript Implementation
function linearSearch(array, searchValue) {
for (const [index, element] of array.entries()) {
if (element === searchValue) {
return index;
} else if (element > searchValue) {
break;
}
}
return null;
}

console.log(linearSearch([3, 17, 75, 80, 202], 22));

⏱ Time Complexity

Worst-case: O(N)
Best-case (early stop): Much faster, often O(1) – O(N/2)

But still slower than binary search.

3. ⚡ Binary Search (The Real Advantage of Ordered Arrays)

Binary Search is a divide-and-conquer algorithm that takes full advantage of sorting.

How it works:

Look at the middle of the array

If the middle value is the target → return it

If the target is smaller → search the left half

If the target is larger → search the right half

Repeat until found or the search space is empty

🔎 Visual Example

Searching 22 in:

[3, 17, 75, 80, 202]

Steps:

Middle → 75 → too big

Look left → [3, 17]

Middle → 17 → too small

Look right → [ ] → empty

Not found

Binary search eliminates half the array at every step.

JavaScript Implementation

Iterative version:

function binarySearch(array, searchValue) {
let left = 0;
let right = array.length - 1;

while (left <= right) {
const mid = Math.floor((left + right) / 2);
const value = array[mid];

    if (value === searchValue) {
      return mid;
    }

    if (value < searchValue) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }

}

return null;
}

console.log(binarySearch([3, 17, 75, 80, 202], 22));

⏱ Time Complexity Comparison
Algorithm Best Case Worst Case Works on Unsorted?
Linear Search O(1) O(N) ✅ Yes
Linear Search (ordered) O(1) O(N) ❌ No
Binary Search O(1) O(log N) ❌ No
🚀 Why Binary Search is Better

If an array has:

1,000,000 elements

Linear search worst case → 1,000,000 checks

Binary search → 20 checks

Because:

log2(1,000,000) ≈ 20

4. 📌 Summary

Linear search checks each element in order.

Ordered arrays allow early stopping, making linear search slightly faster.

Binary search is much faster (O(log N)) and is the real reason ordered arrays are powerful.

Sorting enables efficient search algorithms.
