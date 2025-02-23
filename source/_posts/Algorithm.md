---
title: 算法-链表
date: 2025-02-23 15:28:00
tags:
  - 链表
categories: 算法
photos: /tupian/Lecode01.jpg
---

# Test19 删除链表的倒数第 N 个节点

> 通过快慢指针来解决，类似于你要删除中间元素的题

## 题目

![image-20210923091350952](/tupian/Lecode19.png)

## 解题过程

### 1.初始化

```java
ListNode dummy = new ListNode(0);
dummy.next = head;
```

- 创建一个新指针，类型是 ListNode，它指向了 head 节点的地址
- head 是链表的头结点，通常在链表操作中，它是整个链表的入口节点。通过 head 我们可以访问链表中的所有元素。
- dummy 是一个新的局部变量，它的作用是作为当前节点的指针，用来在链表中进行遍历、操作或修改，而不直接修改 head
  > 这样做的好处：
  >
  > 1. 避免破坏链表的结构
  > 2. 链表头部的访问性
  > 3. 方便链表头部操作
  > 4. 保持代码的清晰和简洁
  > 5. 链表的复用和一致性

### 2.定义快慢指针:

```java
ListNode slow = dummy;
ListNode fast = dummy;
```

定义了两个指针 slow 和 fast，都从 dummy 开始。

### 3.快指针先走 n 步:

```java
while (n > 0) {
    fast = fast.next;
    n--;
}
```

- fast 指针先走 n 步，这样在后续的过程中，fast 和 slow 之间的距离始终保持为 n 步。
- 这样可以保证当 fast 到达链表的最后一个节点时，slow 恰好处在要删除节点的前一个节点。

### 4.快慢指针一起移动:

```java
while (fast.next != null) {
    slow = slow.next;
    fast = fast.next;
}
```

- fast 和 slow 同时向后移动，每次都移动一个节点，直到 fast 到达链表的最后一个节点。
- 因为 fast 已经提前走了 n 步，所以当 fast 到达链表末尾时，slow 恰好指向的是要删除节点的前一个节点。

### 5.删除节点:

```java
slow.next = slow.next.next;
```

- 此时 slow.next 就是要删除的节点，slow.next.next 是要删除节点的下一个节点。
- 通过将 slow.next 指向 slow.next.next，就跳过了要删除的节点，从而完成了删除操作。

### 6.返回新链表的头:

```java
return dummy.next;
```

最后返回 dummy.next，即新链表的头节点。如果删除的节点是头节点，dummy.next 就会指向新的头节点

---

### cod

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        // 定义伪指针，用来返回结果
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        // 定义一个慢指针和一个快指针
        ListNode slow = dummy;
        ListNode fast = dummy;
        // 快指针先走n步
        while (n > 0) {
            fast = fast.next;
            n--;
        }
        // 快慢指针同时走，直到快指针走到最后一个节点
        while (fast.next != null) {
            slow = slow.next;
            fast = fast.next;
        }
        // 此时慢指针的下一个节点就是要删除的节点
        slow.next = slow.next.next;
        return dummy.next;
    }
}
```

---

# Test21 合并两个有序链表

## 题目

![image-20210923091350952](/tupian/Lecode21.png)

## 解题思路

> 这道题类似于衣服上的拉链一样，有序插入

## 解体过程

### 1.创建虚拟头结点：

```java
ListNode dummy = new ListNode(-1);
ListNode p = dummy;
```

dummy 是一个虚拟头结点，p 是指向当前合并链表末尾的指针。使用虚拟头结点可以简化链表操作，避免处理头结点为空的特殊情况。

### 2.初始化指针：

```java
ListNode p1 = list1, p2 = list2;
```

p1 和 p2 分别是指向 list1 和 list2 的指针，用于遍历两个输入链表。

### 3.遍历并合并链表：

```java
while (p1 != null && p2 != null) {
    if (p1.val > p2.val) {
        p.next = p2;
        p2 = p2.next;
    } else {
        p.next = p1;
        p1 = p1.next;
    }
    p = p.next;
}
```

在这个循环中，p1 和 p2 同时遍历两个链表，比较当前节点的值：

> 如果 p1 的值大于 p2 的值，将 p2 的节点连接到合并链表的末尾，并移动 p2 指针。
> 否则，将 p1 的节点连接到合并链表的末尾，并移动 p1 指针。 每次连接后，p 指针向后移动，指向合并链表的最新末尾节点。

### 4.处理剩余节点：

```java
if (p1 != null) {
    p.next = p1;
}
if (p2 != null) {
    p.next = p2;
}
```

当其中一个链表遍历完毕后，另一个链表可能还有剩余节点。由于两个链表都是升序的，剩余的节点已经是有序的，因此可以直接将剩余的节点连接到合并链表的末尾。

### 5.返回合并后的链表：

```java
return dummy.next;
```

dummy.next 即为合并后的链表头节点。

## 实例

假设输入链表为 list1 = [1, 2, 4] 和 list2 = [1, 3, 4]，经过上述操作，合并后的链表为 [1, 1, 2, 3, 4, 4]。

---

## code

```java
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode dummy = new ListNode(-1);
        ListNode p = dummy;
        ListNode p1 = list1, p2 = list2;
        while (p1 != null && p2 != null) {
            if (p1.val > p2.val) {
                p.next = p2;
                p2 = p2.next;
            } else {
                p.next = p1;
                p1 = p1.next;
            }
            p = p.next;
        }
        if (p1 != null) {
            p.next = p1;
        }
        if (p2 != null) {
            p.next = p2;
        }
        return dummy.next;
    }
}
```

---

# Test24 两两交换链表中的节点

## 题目

![image-20210923091350952](/tupian/Lecode24.png)

> 这段代码是一个链表题目的迭代解法，旨在交换链表中每一对相邻的节点。与递归方法不同，使用了一个哨兵节点和迭代方式，避免了递归调用栈的额外开销。

## 解题过程

### 1.初始化哨兵节点：

```java
ListNode dummy = new ListNode(0, head);
```

创建一个哨兵节点(虚拟节点) dummy，它的 next 指向链表的头节点 head。使用虚拟头节点的好处是可以方便地处理链表头部的交换（如果不使用虚拟头结点，链表头部交换会非常麻烦，因为需要额外的判断）。

### 2.定义两个指针：

```java
ListNode node0 = dummy;
ListNode node1 = head;
```

- node0 指向哨兵节点，它始终保持指向当前交换对的前一个节点，负责连接交换后的节点。
- node1 指向当前交换对的第一个节点（即需要交换的节点的第一个节点），用于每次交换节点。

### 3.迭代交换每对节点：

```java
while (node1 != null && node1.next != null) {
    ListNode node2 = node1.next;  // 第二个节点
    ListNode node3 = node2.next;  // 第三个节点

    node0.next = node2;           // 让 node0 指向第二个节点
    node2.next = node1;           // 第二个节点指向第一个节点（交换）
    node1.next = node3;           // 第一个节点指向第三个节点（继续链表）

    node0 = node1;                // 让 node0 向前移动，指向当前交换对的第一个节点
    node1 = node3;                // 让 node1 向前移动，指向下一个交换对的第一个节点
}
```

每轮交换：交换 node1 和 node2 两个节点，并调整指针

> 交换步骤： 1.获取节点：
> node2 = node1.next：获取 node1 的下一个节点（即第二个节点）。
> node3 = node2.next：获取 node2 的下一个节点（即第三个节点）。 2.交换相邻节点：
> node0.next = node2;：将 node0 的 next 指针指向 node2，使得 node2 成为当前子链表的头节点。
> node2.next = node1;：将 node2 的 next 指针指向 node1，将 node1 移到 node2 的后面。
> node1.next = node3;：将 node1 的 next 指针指向 node3，保证交换后的链表依然保持连接。 3.更新指针：
> node0 = node1;：将 node0 更新为 node1，因为下一次交换要从 node1 开始。
> node1 = node3;：将 node1 更新为 node3，因为下一次交换要从 node3 开始。

### 4.返回结果：

```java
return dummy.next; // 返回新链表的头节点
```

最后返回 dummy.next，即链表的新的头节点。由于哨兵节点 dummy 是在原始头节点之前创建的，因此 dummy.next 就是链表经过交换后的新的头节点。

---

## code

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode swapPairs(ListNode head) {
        ListNode dummy = new ListNode(0, head);
        ListNode node0 = dummy;
        ListNode node1 = head;
        while (node1 != null && node1.next != null) {
            ListNode node2 = node1.next;
            ListNode node3 = node2.next;

            node0.next = node2;
            node2.next = node1;
            node1.next = node3;

            node0 = node1;
            node1 = node3;
        }
        return dummy.next;
    }
}
```
