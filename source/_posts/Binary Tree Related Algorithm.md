---
title: Binary Tree Related Algorithm
date: 2023-01-19 15:24:56
tags:
  - Binary Tree
categories:
  - Study Algorithms
lang: en
comments: false
excerpt: Here are some algorithms about binary tree.
---

Here are some algorithms about binary tree, include: traversal trees, complete trees, different types trees etc. You can direct to them by outline on the right.

## Tree Traversals

### Pre Order

```ts
const PreOrder = (node) => {
  if (node === null) return;
  console.log(node.value); // visit the node before traverse
  PreOrder(node.left);
  PreOrder(node.right);
};
```

### In Order

```ts
const InOrder = (node) => {
  if (node === null) return;
  InOrder(node.left);
  console.log(node.value); // visit the node in traverse
  InOrder(node.right);
};
```

### Post Order

```ts
const PostOrder = (node) => {
  if (node === null) return;
  PostOrder(node.left);
  PostOrder(node.right);
  console.log(node.value); // visit the node after traverse
};
```

### Level Order

```ts
function levelOrder(root: TreeNode | null): number[][] {
  let queue: (TreeNode | null)[] = [root];
  const result: number[][] = [];

  while (queue.length > 0) {
    const ans: number[] = [];
    const q: (TreeNode | null)[] = [];

    while (queue.length > 0) {
      const node = queue.shift();
      if (node) {
        ans.push(node.val);
        q.push(node.left, node.right);
      }
    }

    result.push(ans);
    queue = q;
  }

  result.pop();
  return result;
}
```

## Complete Binary Tree

Give an array and return a tree construction.

```js

```

## Maximum Depth of Binary Tree

We go deep inside it's left and it's right, compare both of them. The one has greatest value will be add to one.

```ts
function maxDepth(root: TreeNode | null): number {
  if (root === null) return 0;

  const leftLen = maxDepth(root.left);
  const rightLen = maxDepth(root.right);

  return Math.max(leftLen, rightLen) + 1;
}
```

### Minimum Depth of Binary Tree

```ts
function minDepth(root: TreeNode | null): number {
  if (root === null) return 0;

  const l = minDepth(root?.left);
  const r = minDepth(root?.right);

  // Add This Line
  if (r === 0 || l === 0) return Math.max(l, r) + 1;
  return Math.min(l, r) + 1;
}
```

### Balanced Binary Tree

A balanced binary tree, also referred to as a height-balanced binary tree, is defined as a binary tree in which the height of the left and right subtree of any node differ by not more than 1.

```ts
function isBalanced(root: TreeNode | null): boolean {
  let resp = true;
  const Depth = (node: TreeNode | null): number => {
    if (node === null || resp === false) return 0;

    const l = Depth(node.left);
    const r = Depth(node.right);

    if (Math.abs(l - r) > 1) resp = false;
    return 1 + Math.max(l, r);
  };

  Depth(root);
  return resp;
}
```

## Check If Two Binary Trees Are Equal

Given the roots of two binary trees p and q, write a function to check if they are the same or not.

We can traverse both of them at same time and find if they are equal in the same node.

```ts
const isSameNode = (p: TreeNode | null, q: TreeNode | null) => {
  if (p === null && q === null) return true;
  if (p === null || q === null) return false;

  if (p.val !== q.val) return false;

  return isSameNode(p.left, q.left) && isSameNode(p.right, q.right);
};
```

## Invert Binary Tree

```ts
function invertTree(root: TreeNode | null): TreeNode | null {
  if (root === null) return null;
  invertTree(root.left);
  invertTree(root.right);
  [root.right, root.left] = [root.left, root.right];
  return root;
}
```
