# 链表中倒数第k个结点

## 题目描述

输入一个链表，输出该链表中倒数第k个结点。

## 思路

准备两个指针：`p1`和`p2`，初始时让`p1`和`p2`都指向链表头部，然后让`p1`不动，让`p2`往前走`K`步，这样`p1`和`p2`就相差了`K`个结点，然后让`p1`和`p2`同时向前走，当`p2`走到链表最后一个节点`null`时，此时`p1`所在的节点即为链表中倒数第k个结点，如图：

![1587008108668](E:\swordOffer-by-JavaScript\1587008108668.png)

## 代码

```javascript
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/
function FindKthToTail(head, k) {
  let p1 = head;
  let p2 = head;
  // 让p1先走k步
  // 此处包含处理一种边界情况：当链表只有5个结点而要求倒数第6个结点时
  // 要求倒数第6个结点，则p1应向前走6步，而p1走到第5步时已经走到链表末尾null了，
  // 此时循环如果还未结束，那就说明是出现了这种边界情况，返回null即可
  for (let i = 0; i < k; i++) {
    if (p1) {
      p1 = p1.next;
    } else {
      return null;
    }
  }
  while (p1) {
    p1 = p1.next;
    p2 = p2.next;
  }
  return p2;
}
```

