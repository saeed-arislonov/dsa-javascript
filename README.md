# Searching an Ordered Array

A concise guide to linear search, early stopping, and binary search in sorted arrays.

---

## 📘 Overview

This document explains how searching works in:

- Classic (unsorted) arrays
- Ordered (sorted) arrays

and how sorting enables a much faster algorithm: **Binary Search**.

---

# 1. 🔍 Linear Search (Classic Array)

In a classic array, the only way to find a value is to:

1. Start from the left
2. Check each element one by one
3. Stop when you find the value or reach the end

Example array:

    [17, 3, 75, 202, 80]

Searching for `22` requires checking all elements because the array is not sorted.

### ⏱ Time Complexity

- **Best case:** O(1)
- **Worst case:** O(N)

---

# 2. 🔍 Linear Search in an Ordered Array

When an array is sorted, linear search can be optimized using **early stopping**.

Example:

    [3, 17, 75, 80, 202]

Searching for `22`:

- 3 → too small
- 17 → too small
- 75 → **STOP!** (75 > 22, so 22 cannot appear after)

This reduces unnecessary comparisons.

---

## JavaScript Implementation

```js
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
```

# 3. Binary Search — The True Advantage of Ordered Arrays

Binary search is a divide-and-conquer strategy that repeatedly halves the search range.

How it works:

1. Look at the middle element

2. If it matches → return it

3. If smaller → search left half

4. If larger → search right half

5. Repeat until found or empty

```js
[3, 17, 75, 80, 202];
```

Searching for 22:

75 → too big
Search left → [3, 17]

17 → too small
Search right → empty → not found

```js
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
```

# 4. ⏱ Performance Comparison

| Algorithm              | Best Case | Worst Case   | Requires Sorted Array? |
| ---------------------- | --------- | ------------ | ---------------------- |
| Linear Search          | O(1)      | O(N)         | No                     |
| Linear Search (sorted) | O(1)      | O(N)         | Yes                    |
| **Binary Search**      | O(1)      | **O(log N)** | Yes                    |

### 🚀 Why Binary Search Is So Fast

Binary search repeatedly divides the search space by 2.

Example:  
For an array with **1,000,000 elements**:

- Linear search worst case → **1,000,000 comparisons**
- Binary search worst case → **about 20 comparisons**

Because:

    log2(1,000,000) ≈ 20

This is why sorted arrays are so powerful — they unlock logarithmic-time searches.

---

# 5. 📁 Summary

- **Linear Search (unsorted)** searches each item one by one and may require scanning the entire array.
- **Linear Search (sorted)** can stop early if the current element becomes larger than the target.
- **Binary Search** is the main advantage of sorted arrays → it runs in **O(log N)** time.
- As arrays grow larger, binary search becomes dramatically faster than any linear approach.
- Sorting a dataset enables more efficient algorithms and better scalability.

---
