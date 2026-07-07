# 26. Remove Duplicates from Sorted Array

[![LeetCode](https://img.shields.io/badge/LeetCode-Problem%2026-orange?style=for-the-badge&logo=leetcode)](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

<p align="center">
  <a href="https://leetcode.com/problems/remove-duplicates-from-sorted-array/">
    <img src="https://img.shields.io/badge/Solve%20on-LeetCode-orange?style=for-the-badge&logo=leetcode" alt="LeetCode Button">
  </a>
</p>

## Problem Statement

Given an integer array `nums` sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once.

The relative order of the elements should be kept the same.

Return the number of unique elements `k`.

The first `k` elements of `nums` should contain the unique elements in sorted order.

### Example 1

```text
Input: nums = [1,1,2]

Output: 2

nums = [1,2,_]
```

### Example 2

```text
Input: nums = [0,0,1,1,1,2,2,3,3,4]

Output: 5

nums = [0,1,2,3,4,_,_,_,_,_]
```

---

## Approach

Use the **Two Pointer Technique**:

- Since the array is already sorted, duplicates are adjacent.
- Maintain a pointer `res` to track the position where the next unique element should be placed.
- Traverse the array from index `1`.
- Whenever a new unique element is found, place it at `nums[res]` and increment `res`.
- At the end, `res` represents the count of unique elements.

---

## Java Solution

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length == 0) return 0;

        int res = 1;

        for (int i = 1; i < nums.length; i++) {
            if (nums[i] != nums[i - 1]) {
                nums[res] = nums[i];
                res++;
            }
        }

        return res;
    }
}
```

---

## Complexity Analysis

| Complexity | Value |
|------------|--------|
| Time Complexity | O(n) |
| Space Complexity | O(1) |

---

## Key Takeaways

✅ Sorted array allows easy duplicate detection.

✅ In-place modification without extra memory.

✅ Efficient two-pointer approach.

---

### Question Link

🔗 https://leetcode.com/problems/remove-duplicates-from-sorted-array/
