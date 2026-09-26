# Leetcode_Day56
 Day 56 – Reorder List

## 🧩 Problem

**LeetCode 143 – Reorder List**  
**Difficulty:** Medium

Given a singly linked list:

```text
L0 → L1 → L2 → ... → Ln-1 → Ln

Reorder it into:

L0 → Ln → L1 → Ln-1 → L2 → Ln-2 → ...

The values of the nodes cannot be modified. Only the links between nodes can be changed.

💡 Example
Input
1 → 2 → 3 → 4
Output
1 → 4 → 2 → 3
🧠 Approach

The problem can be solved using three steps:

1. Find the Middle

Use the slow and fast pointer technique.

slow moves one step at a time.
fast moves two steps at a time.
When fast reaches the end, slow is around the middle.

This divides the list into two parts.

1 → 2 → 3 → 4
        ↑
       slow
2. Reverse the Second Half

Take the second half of the list and reverse it.

1 → 2

3 → 4

becomes:

1 → 2

4 → 3

The reversal is done using three pointers:

prev
curr
nextNode
3. Merge Both Halves

Finally, merge the two lists alternately.

First half:   1 → 2
Second half:  4 → 3

Merge them as:

1 → 4 → 2 → 3
💻 Java Solution
class Solution {

    ListNode reverse(ListNode h) {
        ListNode prev = null;
        ListNode curr = h;

        while (curr != null) {
            ListNode nextNode = curr.next;
            curr.next = prev;
            prev = curr;
            curr = nextNode;
        }

        return prev;
    }

    ListNode findMid(ListNode h) {
        ListNode slow = h;
        ListNode fast = h;

        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        if (fast.next == null)
            return slow;

        return slow.next;
    }

    public void reorderList(ListNode h) {

        ListNode m = findMid(h);
        ListNode h2 = m.next;

        m.next = null;

        h2 = reverse(h2);

        join(h, h2);
    }

    ListNode join(ListNode h, ListNode h2) {

        ListNode p1 = h;
        ListNode p2 = h2;

        while (p1 != null && p2 != null) {

            ListNode t1 = p1.next;
            p1.next = p2;
            p1 = t1;

            ListNode t2 = p2.next;
            p2.next = p1;
            p2 = t2;
        }

        return h;
    }
}
⏱️ Complexity
Time Complexity
O(n)

The list is traversed a constant number of times.

Space Complexity
O(1)

Only a few pointers are used, so no extra list or array is created.

📚 What I Learned
How to find the middle of a linked list using slow and fast pointers.
How to reverse a linked list using pointer manipulation.
How to merge two linked lists alternately.
How multiple basic linked-list techniques can be combined to solve a more complex problem.
Most importantly, how careful pointer management is when modifying linked-list connections.
🔑 Key Takeaway

A difficult problem does not always require a completely new concept.

Sometimes, the solution is simply combining the concepts you already know in the right order.

🚀 Day 56 Complete

Another day of solving, debugging, and learning.

One problem at a time. One step closer to becoming a better problem solver.
