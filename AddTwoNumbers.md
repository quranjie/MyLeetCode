# 题目：
You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8

# 我的解题思路：
这道题我想的太简单了，以为直接把l2的数值加到l1上就可以了。next的指向也有问题

# 标准答案是这样的：

给你两个表示两个非负数字的链表。数字以相反的顺序存储，其节点包含单个数字。将这两个数字相加并将其作为一个链表返回。

输入: (2 -> 4 -> 3) + (5 -> 6 -> 4)
输出: 7 -> 0 -> 8

```
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    int carry=0;
    ListNode listNode=new ListNode(0);
    ListNode p1=l1,p2=l2,p3=listNode;
    while(p1!=null||p2!=null){
        if(p1!=null){
            carry+=p1.val;
            p1=p1.next;
        }
        if(p2!=null){
            carry+=p2.val;
            p2=p2.next;
        }
        p3.next=new ListNode(carry%10);
        p3=p3.next;
        carry/=10;
    }
    if(carry==1)
        p3.next=new ListNode(1);
    return listNode.next;
}

public class ListNode {
    int val;
    ListNode next;
    ListNode(int x) { val = x; }
}
```

我写的程序问题所在：   
* 没有好好读题，忽略了carry的因素
* 没有将结果存放到第三个变量里，以后这种类似的问题要注意
* 对链表的操作不是很熟悉，应该自己实现一下单链表、双链表的操作
  

