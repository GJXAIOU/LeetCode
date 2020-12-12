## 题目描述

判断给定的链表中是否有环

扩展：

你能给出空间复杂度![img](https://www.nowcoder.com/equation?tex=O(1)%5C)的解法么？

```java
package nowcoder.interview;


/**
 * @Author GJXAIOU
 * @Date 2020/9/13 21:32
 */
public class NC4 {


    class ListNode {
        int val;
        ListNode next;

        ListNode(int x) {
            val = x;
            next = null;
        }
    }

    public class Solution {
        public boolean hasCycle(ListNode head) {
            if (head == null) {
                return false;
            }
            ListNode slow = head;
            ListNode fast = head;
            // 要保证 fast.next 和 fast.next.next 均不为空
            while (fast != null && fast.next != null) {
                slow = slow.next;
                fast = fast.next.next;
                if (slow == fast) {
                    return true;
                }
            }
            return false;
        }
    }
}

```

