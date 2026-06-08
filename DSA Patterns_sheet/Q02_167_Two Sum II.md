# 167. Two Sum II - Input Array Is Sorted

<p align="center">
  <a href="https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/">
    <img src="https://img.shields.io/badge/LeetCode-167%20Two%20Sum%20II-orange?style=for-the-badge&logo=leetcode" alt="LeetCode Problem">
  </a>
</p>

## 🔗 Problem Link

➡️ https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/

## 📝 Problem Statement

Given a **1-indexed sorted array** `numbers` and a target value `target`, find two numbers such that they add up to the target.

Return the indices of the two numbers as:

```text
[index1, index2]
```

where:

* `1 <= index1 < index2 <= numbers.length`
* Exactly one valid solution exists.
* Constant extra space must be used.

---

## 💡 Approach: Two Pointers

Since the array is already sorted:

1. Initialize two pointers:

   * `left = 0`
   * `right = n - 1`

2. Calculate:

```java
sum = numbers[left] + numbers[right]
```

3. If:

   * `sum == target` → return indices.
   * `sum < target` → move `left++` to increase sum.
   * `sum > target` → move `right--` to decrease sum.

This works because the array is sorted.

---

## ✅ Java Solution

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int left = 0;
        int right = numbers.length - 1;

        while (left < right) {
            int total = numbers[left] + numbers[right];

            if (total == target) {
                return new int[]{left + 1, right + 1};
            } else if (total < target) {
                left++;
            } else {
                right--;
            }
        }

        return new int[]{};
    }
}
```

---

## 🔍 Dry Run

### Input

```java
numbers = [2,7,11,15]
target = 9
```

### Steps

| Left | Right | Sum | Action  |
| ---- | ----- | --- | ------- |
| 2    | 15    | 17  | right-- |
| 2    | 11    | 13  | right-- |
| 2    | 7     | 9   | Found   |

### Output

```java
[1,2]
```

---

## ⏱ Complexity Analysis

| Complexity | Value |
| ---------- | ----- |
| Time       | O(n)  |
| Space      | O(1)  |

* Each pointer moves at most `n` times.
* No extra data structure is used.

---

## 🚀 Key Takeaway

Whenever you see:

* Sorted Array
* Pair Sum
* Constant Space Requirement

Think of the **Two Pointer Technique** before using HashMap.

