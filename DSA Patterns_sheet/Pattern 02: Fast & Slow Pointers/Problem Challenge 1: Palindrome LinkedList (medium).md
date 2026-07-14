# 234. Palindrome Linked List

- **Difficulty:** Easy
- **Topic:** Linked List, Two Pointers
- **LeetCode:** https://leetcode.com/problems/palindrome-linked-list/

---

# Problem Statement

Given the head of a singly linked list, return **true** if it is a palindrome or **false** otherwise.

A palindrome is a sequence that reads the same forward and backward.

---

## Example 1

```
Input:
head = [1,2,2,1]

Output:
true
```

### Visualization

```
1 → 2 → 2 → 1
↑           ↑
Same      Same

2 → 2
↑     ↑
Same
```

The linked list reads the same from both directions.

Answer:

```
true
```

---

## Example 2

```
Input:
head = [1,2]

Output:
false
```

Visualization

```
1 → 2

Forward : 1 2
Backward: 2 1
```

Not equal.

Answer:

```
false
```

---

# Constraints

```
1 <= Number of Nodes <= 100000

0 <= Node.val <= 9
```

---

# Approach 1 : Using Array

## Idea

Store all node values into an ArrayList.

Then compare

- First element
- Last element

using two pointers.

---

## Algorithm

### Step 1

Traverse linked list.

```
1 → 2 → 2 → 1
```

Store into array.

```
[1,2,2,1]
```

---

### Step 2

Take two pointers.

```
left = 0
right = 3
```

Compare

```
1 == 1 ✔
```

Move pointers.

```
left++
right--
```

Now

```
2 == 2 ✔
```

Everything matches.

Return true.

---

## Java Code (Array)

```java
class Solution {

    public boolean isPalindrome(ListNode head) {

        List<Integer> list = new ArrayList<>();

        while(head != null){
            list.add(head.val);
            head = head.next;
        }

        int left = 0;
        int right = list.size() - 1;

        while(left < right){

            if(!list.get(left).equals(list.get(right)))
                return false;

            left++;
            right--;
        }

        return true;
    }
}
```

---

## Complexity

Time

```
O(n)
```

Space

```
O(n)
```

---

# Approach 2 (Optimal)

This is the solution interviewers expect.

Instead of storing values in an array,

we

1. Find middle
2. Reverse second half
3. Compare halves

No extra memory required.

---

# Step 1 : Find Middle

Use Fast and Slow pointers.

Initially

```
Slow
 ↓

1 → 2 → 2 → 1

 ↑
Fast
```

Iteration 1

```
1 → 2 → 2 → 1
    ↑
   Slow

        ↑
       Fast
```

Loop ends.

Middle is

```
1 → 2 → 2 → 1
        ↑
      Slow
```

---

# Why Fast Pointer Works?

Fast moves

```
2 steps
```

Slow moves

```
1 step
```

So when Fast reaches end,

Slow automatically reaches middle.

---

# Step 2 : Reverse Second Half

Current second half

```
2 → 1
```

Reverse it.

Result

```
1 → 2
```

Now imagine

```
First Half

1 → 2

Second Half

1 → 2
```

---

# Reverse Process

Initially

```
prev = null

curr

2 → 1
```

Iteration 1

```
next = 1

2 → null

prev

2

curr

1
```

Iteration 2

```
1 → 2 → null

prev

1
```

Done.

---

# Step 3 : Compare

Compare

```
1 == 1 ✔

2 == 2 ✔
```

Everything matched.

Return true.

---

# Dry Run

Input

```
1 → 2 → 2 → 1
```

Find middle

```
Slow

↓

2
```

Reverse

Before

```
2 → 1
```

After

```
1 → 2
```

Compare

```
1 == 1 ✔

2 == 2 ✔
```

Answer

```
true
```

---

# Dry Run 2

Input

```
1 → 2
```

Middle

```
2
```

Reverse

```
2
```

Compare

```
1 != 2
```

Answer

```
false
```

---

# Java Code (Optimal)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *
 *     ListNode() {}
 *
 *     ListNode(int val) {
 *         this.val = val;
 *     }
 *
 *     ListNode(int val, ListNode next) {
 *         this.val = val;
 *         this.next = next;
 *     }
 * }
 */

class Solution {

    public boolean isPalindrome(ListNode head) {

        // Empty list or single node
        if (head == null || head.next == null)
            return true;

        // Step 1: Find the middle
        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        // Step 2: Reverse second half
        ListNode prev = null;

        while (slow != null) {

            ListNode next = slow.next;

            slow.next = prev;

            prev = slow;

            slow = next;
        }

        // Step 3: Compare both halves
        ListNode first = head;
        ListNode second = prev;

        while (second != null) {

            if (first.val != second.val)
                return false;

            first = first.next;
            second = second.next;
        }

        return true;
    }
}
```

---

# Code Walkthrough

## Finding Middle

```java
while(fast != null && fast.next != null){

    slow = slow.next;

    fast = fast.next.next;
}
```

Slow moves one step.

Fast moves two steps.

Slow reaches middle.

---

## Reversing

```java
while(slow != null){

    ListNode next = slow.next;

    slow.next = prev;

    prev = slow;

    slow = next;
}
```

Classic linked list reversal.

---

## Comparing

```java
while(second != null){

    if(first.val != second.val)
        return false;

    first = first.next;
    second = second.next;
}
```

If every node matches,

return true.

---

# Complexity Analysis

## Time Complexity

Finding middle

```
O(n)
```

Reverse second half

```
O(n)
```

Compare halves

```
O(n)
```

Overall

```
O(n)
```

---

## Space Complexity

Only a few pointers are used.

```
O(1)
```

---

# Why This Solution is Optimal

✅ One traversal to find the middle.

✅ In-place reversal.

✅ No extra array.

✅ Constant memory.

✅ Linear time.

---

# Interview Questions

### Q1. Why use Fast and Slow pointers?

To find the middle in one traversal.

---

### Q2. Why reverse only the second half?

We only need to compare mirrored nodes. Reversing half the list is enough.

---

### Q3. Why compare until `second != null`?

The reversed second half is never longer than the first half, so comparing until the second pointer ends covers all required nodes.

---

### Q4. Can we restore the original linked list?

Yes. Reverse the second half again after comparison if preserving the original list is required.

---

# Key Takeaways

- Fast & Slow Pointer → Find middle.
- Reverse Linked List → Reverse second half.
- Two Pointer Comparison → Check palindrome.
- Time Complexity → **O(n)**
- Space Complexity → **O(1)**
- This is the most commonly expected interview solution for LeetCode 234.
