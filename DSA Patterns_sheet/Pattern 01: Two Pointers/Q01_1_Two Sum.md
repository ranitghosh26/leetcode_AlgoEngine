# 🔥 LeetCode 1. Two Sum

<p align="center">
  <a href="https://leetcode.com/problems/two-sum/" target="_blank">
    <img src="https://img.shields.io/badge/LeetCode-Two%20Sum-orange?style=for-the-badge&logo=leetcode" alt="LeetCode Two Sum">
  </a>
</p>

## 📌 Problem Link

🔗 https://leetcode.com/problems/two-sum/

## 📝 Problem Statement

Given an array of integers `nums` and an integer `target`, return the indices of the two numbers such that they add up to `target`.

### Example

```text
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
```

Explanation:

```text
nums[0] + nums[1] = 2 + 7 = 9
```

---

# Solution 1: Brute Force

## Java Code

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {

        for (int i = 0; i < nums.length; i++) {

            for (int j = i + 1; j < nums.length; j++) {

                if (nums[i] + nums[j] == target) {
                    return new int[]{i, j};
                }
            }
        }

        return new int[0];
    }
}
```

### Complexity Analysis

| Complexity | Value |
| ---------- | ----- |
| Time       | O(n²) |
| Space      | O(1)  |

---

# Solution 2: Two Pointer Approach

> Note: Since the problem requires original indices, we must store values along with their indices before sorting.

## Java Code

```java
import java.util.*;

class Solution {

    static class Pair {
        int value;
        int index;

        Pair(int value, int index) {
            this.value = value;
            this.index = index;
        }
    }

    public int[] twoSum(int[] nums, int target) {

        Pair[] arr = new Pair[nums.length];

        for (int i = 0; i < nums.length; i++) {
            arr[i] = new Pair(nums[i], i);
        }

        Arrays.sort(arr, (a, b) -> Integer.compare(a.value, b.value));

        int left = 0;
        int right = arr.length - 1;

        while (left < right) {

            int sum = arr[left].value + arr[right].value;

            if (sum == target) {
                return new int[]{
                    arr[left].index,
                    arr[right].index
                };
            }

            if (sum < target) {
                left++;
            } else {
                right--;
            }
        }

        return new int[0];
    }
}
```

### Complexity Analysis

| Complexity | Value      |
| ---------- | ---------- |
| Time       | O(n log n) |
| Space      | O(n)       |

---

# 🚀 Optimal Solution (HashMap)

LeetCode's most efficient solution uses a HashMap.

### Complexity

| Complexity | Value |
| ---------- | ----- |
| Time       | O(n)  |
| Space      | O(n)  |

```java
import java.util.*;

class Solution {
    public int[] twoSum(int[] nums, int target) {

        HashMap<Integer, Integer> map = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {

            int complement = target - nums[i];

            if (map.containsKey(complement)) {
                return new int[]{
                    map.get(complement),
                    i
                };
            }

            map.put(nums[i], i);
        }

        return new int[0];
    }
}
```

---

⭐ If this helped, give the repository a star.

