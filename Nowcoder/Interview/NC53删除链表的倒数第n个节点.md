## 题目描述

给定一个链表，删除链表的倒数第n个节点并返回链表的头指针
例如，

```
 给出的链表为:1->2->3->4->5, n= 2.
 删除了链表的倒数第n个节点之后,链表变为1->2->3->5.
```

备注：

题目保证n一定是有效的
请给出请给出时间复杂度为 O(n) 的算法



### 示例1

输入

```
{1,2},2
```

输出

```
{2}
```





```java
package nowcoder.interview;

/**
 * @Author GJXAIOU
 * @Date 2020/10/5 15:57
 */
public class NC53 {
    static class ListNode{
        int val;
        ListNode next = null;
        ListNode(int val){
            this.val = val;
        }
    }

    public class Solution {
        public ListNode removeNthFromEnd (ListNode head, int n) {
            if (head == null){
                 return head;
            }

            ListNode begin = new ListNode(0);
            begin.next = head;
            ListNode slow = begin;
            ListNode fast = begin;
            // 因为前面加了一个结点，所以是 n + 1 步
            while (n-- >= 0){
                fast = fast.next;
            }

            // 结束之后 fast 指向 null
            while (fast != null){
                fast = fast.next;
                slow =slow.next;
            }

            slow.next = slow.next.next;
            return begin.next;
        }
    }
}
```

