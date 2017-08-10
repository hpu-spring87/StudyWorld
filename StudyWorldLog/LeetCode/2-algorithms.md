# 2. Add Two Numbers

## 问题描述

>You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example:**

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
```

## 代码实现

```
package me.chunsheng.leetcode;

import java.util.LinkedList;

/**
 * Created by wei_spring on 2017/8/3.
 */
public class Problems2 {

    static LinkNode head1, head2;

    public static void main(String[] args) {
        Problems2 list = new Problems2();
        // creating first list
        list.head1 = new LinkNode(3);
        list.head1.next = new LinkNode(4);
        list.head1.next.next = new LinkNode(2);

        // creating seconnd list
        list.head2 = new LinkNode(4);
        list.head2.next = new LinkNode(6);
        list.head2.next.next = new LinkNode(5);

        // add the two lists and see the result
        LinkNode rs = list.addTwoList(head1, head2);
        System.out.println("Resultant List is ");
        list.printLink(rs);

    }

    public LinkNode addTwoList(LinkNode first, LinkNode second) {

        //存储计算结果,因为初始化为null,不能直接next拼接结果
        LinkNode result = null;
        //是result拼接temp的纽带
        LinkNode prev = null;
        //每次相加一位临时的结果
        LinkNode temp = null;
        int carray = 0,sum = 0;

        while(first != null || second != null){

            sum = carray + (first != null ? first.data : 0) + (second != null ? second.data : 0);

            carray = sum >= 10 ? 1: 0;

            sum = sum % 10;

            temp = new LinkNode(sum);

            if(result == null){
                result = temp;
            }else{
                prev.next = temp;
            }
            prev = temp;
            if(first != null){
                first = first.next;
            }

            if(second != null){
                second = second.next;
            }
        }
        //最后一位相加,可能进1,要做判断
        if(carray > 0){
            temp.next = new LinkNode(carray);
        }
        return result;
    }


    static class LinkNode {
        int data;
        LinkNode next;
        LinkNode(int data) {
            this.data = data;
            next = null;
        }
    }

    public void printLink(LinkNode linkNode) {
        while (linkNode != null) {
            System.out.println("[" + linkNode.data + "]");
            linkNode = linkNode.next;
        }
    }

}

时间复制度: O(m + n)  m 和 n 分别两个list node数量
```

```
  另外一种实现方式：

  public LinkNode addTwoNumbers(LinkNode l1, LinkNode l2) {
        LinkNode dummyHead = new LinkNode(0);
        LinkNode p = l1, q = l2, curr = dummyHead;
        int carry = 0;
        while (p != null || q != null) {
            int x = (p != null) ? p.data : 0;
            int y = (q != null) ? q.data : 0;
            int sum = carry + x + y;
            carry = sum / 10;
            curr.next = new LinkNode(sum % 10);
            curr = curr.next;
            if (p != null) p = p.next;
            if (q != null) q = q.next;
        }
        if (carry > 0) {
            curr.next = new LinkNode(carry);
        }
        return dummyHead.next;
    }
时间复杂度：O(max(m,n)). 
空间复杂度：O(max(m,n)). 新生成的列表长度为max(m,n)+1.
```



