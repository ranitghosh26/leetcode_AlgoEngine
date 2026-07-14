# 457. Circular Array Loop

**Difficulty:** Medium  
**Topics:** Array, Two Pointers, Fast & Slow Pointers, Graph, Cycle Detection

## 🔗 Question Link

https://leetcode.com/problems/circular-array-loop/

---

# Problem Statement

You are given a **circular array** `nums` containing **non-zero integers**.

Each value tells you how many steps to move.

- Positive value → Move **forward**
- Negative value → Move **backward**

Since the array is circular:

- Moving forward from the last index goes to the first index.
- Moving backward from the first index goes to the last index.

Return **true** if there exists a **valid cycle**, otherwise return **false**.

---

## Example 1

**Input**

```text
nums = [2,-1,1,2,2]
```

**Output**

```text
true
```

**Explanation**

```
0 → 2 → 3 → 0
```

All movements are positive.

Cycle length = 3

Valid cycle.

---

## Example 2

**Input**

```text
nums = [-1,-2,-3,-4,-5,6]
```

**Output**

```text
false
```

**Explanation**

There is no valid cycle because

- direction changes
- self-loop exists

---

## Example 3

**Input**

```text
nums = [1,-1,5,1,4]
```

**Output**

```text
true
```

**Explanation**

```
0 → 1 → 0
```

Not valid because directions change.

But

```
3 → 4 → 3
```

is a valid cycle.

---

# Constraints

```
1 <= nums.length <= 5000

-1000 <= nums[i] <= 1000

nums[i] != 0
```

---

# Understanding the Problem

Think of every index as a node.

Each node points to exactly one next node.

Example

```
nums = [2,-1,1,2,2]

Index

0 1 2 3 4
```

Connections

```
0 → 2
2 → 3
3 → 0
1 → 0
4 → 1
```

We need to determine whether there is a valid cycle.

---

# Conditions of a Valid Cycle

A cycle is valid only when all three conditions are satisfied.

## Condition 1

Cycle length must be greater than 1.

Valid

```
0 → 2 → 3 → 0
```

Invalid

```
2 → 2
```

because it contains only one node.

---

## Condition 2

Every movement must be in the same direction.

Valid

```
+ + + +
```

Valid

```
- - - -
```

Invalid

```
+ - +
```

---

## Condition 3

The cycle must repeat forever.

```
0 → 2 → 3 → 0
```

---

# Brute Force Idea

Start from every index.

Move continuously.

Store visited nodes.

If

- repeated node found
- direction never changes
- size > 1

return true.

Otherwise continue.

---

## Complexity

Time

```
O(N²)
```

Space

```
O(N)
```

Too slow.

---

# Optimized Idea

Notice that every index points to exactly one next index.

This is exactly like a linked list.

```
0 → 2 → 3 → 0
```

Whenever we have a linked list cycle,

the best algorithm is

# Floyd Cycle Detection

also called

**Fast & Slow Pointer Algorithm**

---

# Floyd Algorithm

Use

```
slow
```

moves

```
1 step
```

Use

```
fast
```

moves

```
2 steps
```

If they meet,

there is a cycle.

---

# But We Need Extra Checks

Unlike a linked list,

here

- direction must remain same
- self-loop is not allowed

So before moving,

we verify direction.

---

# Finding Next Index

Suppose

```
nums = [2,-1,1,2,2]
```

Current index

```
3
```

Jump

```
3 + 2 = 5
```

Array size

```
5
```

```
5 % 5 = 0
```

Next index

```
0
```

---

Suppose

```
current = 1

nums[1] = -2
```

```
1 - 2 = -1
```

Negative index.

We convert using

```java
((current + nums[current]) % n + n) % n
```

```
(-1 % 5 + 5) % 5

4
```

Next index

```
4
```

This formula works for

- positive jumps
- negative jumps

---

# Dry Run

```
nums = [2,-1,1,2,2]
```

Initially

```
slow = 0

fast = 0
```

Move

```
slow

0 → 2
```

Move fast twice

```
0 → 2 → 3
```

Now

```
slow = 2

fast = 3
```

Again

Slow

```
2 → 3
```

Fast

```
3 → 0 → 2
```

Again

Slow

```
3 → 0
```

Fast

```
2 → 3 → 0
```

Now

```
slow == fast
```

Cycle detected.

Return

```
true
```

---

# Why Self Loop Is Invalid

Example

```
nums = [5]
```

```
0 → 0
```

Only one node.

Question clearly says

```
k > 1
```

Therefore

invalid.

---

# Why Mark Visited Nodes as Zero

Suppose

```
0 → 3 → 4
```

Already checked.

Later,

starting from

```
3
```

would repeat the same work.

Instead,

mark

```
nums[0] = 0

nums[3] = 0

nums[4] = 0
```

Now future iterations skip them.

This makes total complexity

```
O(N)
```

---

# Algorithm

For every index

If already visited

skip.

Otherwise

Choose direction.

```
Positive?

Negative?
```

Initialize

```
slow

fast
```

Move

```
slow

1 step

fast

2 steps
```

If

- direction changes
- self-loop

Stop.

If

```
slow == fast
```

Return true.

Otherwise

mark entire path visited.

Continue.

Finally

return false.

---

# Java Solution

```java
class Solution {

    public boolean circularArrayLoop(int[] nums) {

        int n = nums.length;

        for (int i = 0; i < n; i++) {

            if (nums[i] == 0)
                continue;

            boolean forward = nums[i] > 0;

            int slow = i;
            int fast = i;

            while (true) {

                slow = next(nums, forward, slow);

                if (slow == -1)
                    break;

                fast = next(nums, forward, fast);

                if (fast == -1)
                    break;

                fast = next(nums, forward, fast);

                if (fast == -1)
                    break;

                if (slow == fast)
                    return true;
            }

            int index = i;

            while (true) {

                int nextIndex = next(nums, forward, index);

                nums[index] = 0;

                if (nextIndex == -1)
                    break;

                index = nextIndex;
            }
        }

        return false;
    }

    private int next(int[] nums, boolean forward, int current) {

        boolean direction = nums[current] > 0;

        if (direction != forward)
            return -1;

        int n = nums.length;

        int next = ((current + nums[current]) % n + n) % n;

        if (next == current)
            return -1;

        return next;
    }
}
```

---

# Code Explanation

### Step 1

Ignore already visited nodes.

```java
if(nums[i]==0)
    continue;
```

---

### Step 2

Remember current direction.

```java
boolean forward = nums[i] > 0;
```

---

### Step 3

Initialize two pointers.

```java
slow = i;

fast = i;
```

---

### Step 4

Move pointers.

```java
slow

1 step
```

```java
fast

2 steps
```

If

```
slow == fast
```

Cycle found.

---

### Step 5

If traversal fails,

mark every node

```java
nums[index]=0;
```

so we never process them again.

---

# Time Complexity

Each element becomes zero only once.

```
O(N)
```

---

# Space Complexity

No extra memory used.

```
O(1)
```

---

# Why This Approach Works

- Every index behaves like a node in a linked list.
- Floyd's Cycle Detection efficiently detects cycles.
- Direction validation ensures only valid cycles are considered.
- Self-loop detection removes cycles of length 1.
- Marking visited nodes prevents repeated traversals, giving **O(N)** time.

---

# Interview Tips

**Why use Floyd's Algorithm?**

Because every index points to exactly one next index, forming a functional graph similar to a linked list.

**Why check direction?**

The problem requires all elements in a cycle to move either forward or backward, never both.

**Why reject self-loops?**

The problem states that the cycle length must be greater than 1.

**Why mark visited nodes as 0?**

It avoids revisiting the same path, ensuring linear time complexity.

---
