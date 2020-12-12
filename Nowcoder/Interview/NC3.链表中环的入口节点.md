##                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 题目描述

对于一个给定的链表，返回环的入口节点，如果没有环，返回null

拓展：

你能给出不利用额外空间的解法么？

## 解法

采用双指针的方法（这个方法还可以用来判断链表中有没有环），一个快指针一个慢指针，快指针一次走两步，慢指针一次走一步，如果链表中有环，那么两个指针一定就可以相遇，并且相遇的地方，一定在环的某处

设相遇的地方距环的入口点一边有a个节点，一边有b个节点，链表除环以外有x个节点，环中一共有c个节点（c=a+b）

那么可以得到如下关系式，用b = c -a表示

![图片描述](NC3.%E9%93%BE%E8%A1%A8%E4%B8%AD%E7%8E%AF%E7%9A%84%E5%85%A5%E5%8F%A3%E8%8A%82%E7%82%B9.resource/bVbuGBO)



## 证明方式二

**1、设置快慢指针，假如有环，他们最后一定相遇。**  

  **2、两个指针分别从链表头和相遇点继续出发，每次走一步，最后一定相遇与环入口。**


  **证明结论1**：设置快慢指针fast和low，fast每次走两步，low每次走一步。假如有环，两者一定会相遇（因为low一旦进环，可看作fast在后面追赶low的过程，每次两者都接近一步，最后一定能追上）。 

   **证明结论2：**


  设： 

  链表头到环入口长度为--**a**  

  环入口到相遇点长度为--**b**  

  相遇点到环入口长度为--**c**  

  **![img](https://uploadfiles.nowcoder.com/images/20180615/4240377_1529033184336_9A253E69EDBB4FD57BB16FC3A32C2756)
**   

  则：相遇时 

  **快指针路程=a+(b+c)k+b** ，k>=1 其中b+c为环的长度，k为绕环的圈数（k>=1,即最少一圈，不能是0圈，不然和慢指针走的一样长，矛盾）。 

   **慢指针路程=a+b**  

  快指针走的路程是慢指针的两倍，所以： 

   **（a+b）\*2=a+(b+c)k+b**  

  化简可得： 

  **a=(k-1)(b+c)+c**  这个式子的意思是：  **链表头到环入口的距离=相遇点到环入口的距离+（k-1）圈环长度**。其中k>=1,所以**k-1>=0**圈。所以两个指针分别从链表头和相遇点出发，最后一定相遇于环入口。

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 * int val;
 * ListNode next;
 * ListNode(int x) {
 * val = x;
 * next = null;
 * }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        if (head == null || head.next == null || head.next.next == null) {
            return null;
        }

        ListNode begin = head.next;
        ListNode end = head.next.next;
        // 当快慢指针相遇的时候停止
        while (begin != end) {
            if (end.next == null || end.next.next == null) {
                return null;
            }
            begin = begin.next;
            end = end.next.next;
        }
        
        // 快指针回到开头
        end = head;
        
        // 快指针从链表头部，慢指针继续遍历
        while (begin != end) {
            begin = begin.next;
            end = end.next;
        }
        return begin;
    }
}
```



==方法二==

```java
package nowcoder.interview;

/**
 * @Author GJXAIOU
 * @Date 2020/9/15 22:21
 */
public class NC3 {

    class ListNode {
        int val;
        ListNode next;

        ListNode(int x) {
            val = x;
            next = null;
        }
    }

    public class Solution {
        /**
         * 链表中环的入口节点
         */
        public ListNode detectCycle(ListNode head) {
            if (head == null || head.next == null || head.next.next == null) {
                return null;
            }

            ListNode slow = head;
            ListNode fast = head;
            while (fast != null && fast.next != null) {
                slow = slow.next;
                fast = fast.next.next;
                if (slow == fast) {
                    break;
                }
            }

            fast = head;

            while (slow != fast) {
                slow = slow.next;
                fast = fast.next;
                if (slow == null) {
                    return null;
                }
            }
            return slow;
        }
    }
}
```

