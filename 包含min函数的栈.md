# 包含min函数的栈

## 题目描述

定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。

注意：保证测试中不会当栈为空的时候，对栈调用pop()或者min()或者top()方法。

## 思路

看到这个问题, 我们最开始可能会想, 添加一个成员变量用于保存最小元素, 每次压栈时如果压栈元素比当前最小元素更小, 就更新最小元素. 

但是这样会有一个问题, 如果最小元素被弹出了呢, 如何获得下一个最小元素呢? 分析到这里可以发现, 仅仅添加一个成员变量存放最小元素是不够的, 我们需要在最小元素弹出后还能得到次小元素, 次小的弹出后, 还要能得到次次小的. 

因此, 用另一个栈来保存这些元素是再合适不过的了. 我们叫它最小元素栈. 

最小元素栈中元素应该是如下样子：

```javascript
let minStack = [...,'次次小元素','次小元素','最小元素']
```

每次压栈操作时, 如果压栈元素小于最小元素栈中的栈顶元素, 那就表明新压入的元素是新的最小元素，就把这个元素压入最小元素栈中, 原本的最小元素就成了次小元素. 

同理, 弹栈时, 如果弹出的元素和最小元素栈的栈顶元素相等, 那就表明栈中的最小元素被弹出了，新的最小元素应该是之前的次小元素，那就从最小元素栈中弹出一个元素，让次小元素变成最小元素栈的栈顶元素。

**总之就是始终保持最小元素栈的栈顶元素永远是当前栈中的最小元素**

## 代码

```javascript
let stack = [];
let minStack = [];  // 最小元素栈
function push(node) {
  stack.push(node);
  if (!minStack.length) {
    minStack.push(node);
  } else {
    // 压栈时, 如果压栈元素比当前最小元素更小, 就把这个元素压入最小元素栈, 
    if (node < minStack[minStack.length - 1]) {
      minStack.push(node);
    }
  }
}
function pop() {
  if (!stack.length) {
    return null;
  }
  let tmp = stack.pop();
  // 弹栈时,如果弹出的元素和最小元素栈的栈顶元素相等, 就把最小元素的栈顶弹出.
  if (tmp === minStack[minStack.length - 1]) {
    minStack.pop();
  }
  return tmp;
}
function top() {
  if (!stack.length) {
    return null;
  }
  return stack[stack.length - 1];
}
function min() {
  return minStack[minStack.length - 1];
}

```

