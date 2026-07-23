# Minimum Sum Subarray (Kadane's Algorithm - Minimum Variant)

---
Problem Link
GeeksforGeeks: https://www.geeksforgeeks.org/problems/smallest-sum-contiguous-subarray/1
---
Problem Statement
Given an integer array `arr[]`, find the contiguous subarray containing at least one element that has the minimum sum, and return that sum.
Example 1
Input:
```text
arr = [3, -4, 2, -3, -1, 7, -5]
```
Output:
```text
-6
```
Explanation:
```text
Subarray = [-4, 2, -3, -1]
Sum = -6
```
Example 2
Input:
```text
arr = [2, 6, 8, 1, 4]
```
Output:
```text
1
```
Explanation:
```text
Subarray = [1]
```
---
Approach
This problem is the minimum-sum version of Kadane's Algorithm.
For every element, there are two choices:
Start a new subarray from the current element.
Extend the previous subarray.
Choose the smaller sum.
Formula:
```java
currSum = Math.min(a[i], currSum + a[i]);
```
Update the global minimum:
```java
minSum = Math.min(minSum, currSum);
```
---
Java Solution
```java
class Solution {
    static int smallestSumSubarray(int a[], int size) {

        int minSum = a[0];
        int currSum = a[0];

        for (int i = 1; i < size; i++) {

            int v1 = currSum + a[i];
            int v2 = a[i];

            currSum = Math.min(v1, v2);
            minSum = Math.min(minSum, currSum);
        }

        return minSum;
    }
}
```
---
Dry Run
Input
```text
[3, -4, 2, -3, -1, 7, -5]
```
Index	Value	Extend	Start New	currSum	minSum
0	3	-	3	3	3
1	-4	-1	-4	-4	-4
2	2	-2	2	-2	-4
3	-3	-5	-3	-5	-5
4	-1	-6	-1	-6	-6
5	7	1	7	1	-6
6	-5	-4	-5	-5	-6
Final Answer:
```text
-6
```
Subarray:
```text
[-4, 2, -3, -1]
```
---
Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
---
Kadane's Algorithm Cheat Sheet
Maximum Sum Subarray
```java
currSum = Math.max(a[i], currSum + a[i]);
maxSum = Math.max(maxSum, currSum);
```
Minimum Sum Subarray
```java
currSum = Math.min(a[i], currSum + a[i]);
minSum = Math.min(minSum, currSum);
```
---
Key Takeaways
`currSum` stores the minimum subarray sum ending at the current index.
`minSum` stores the overall minimum subarray sum.
At each step, either start a new subarray or extend the previous one.
This is the reverse of Kadane's Algorithm for Maximum Subarray.
