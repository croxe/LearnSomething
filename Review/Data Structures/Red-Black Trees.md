
# Ch 13 Red-Black Trees

A red-black tree is approximately balanced. Each node of the tree contains five attributes *color, key, left, right,* and*, p*. If a child or the parent of a node does not exist, the pointer points to NIL. 

A red-black tree is a binary tree that satisfies **the red-black properties**: 
1. Every node is either red or black
2. The root is black
3. Every leaf (NIL) is black
4. If a node is red, then both its children are black.
5. For each node, all simple paths from the node to descendant leaves contain the same number of black nodes. 

We can use sentinel to represent NIL, denote T.nil. T.nil is the parent of root. By using sentinel, we can save space of creating NIL for each leaf. 

Lemma 13.1 
A red-black tree with *n* internal nodes has height at most 2 lg(n + 1).

As consequence of this lemma, the operations SEARCH, MINIMUM, MAXIMUM, SUCCESSOR, and PREDECESSOR in O(lg n) time on red-black trees. 

### Ch 13.2 Rotations

We re-balance the search-tree after operations like INSERT and DELETE by using rotation. 

```
LEFT-ROTATE(T, x)
  y = x.right
  x.right = y.left
  if y.left != T.nil
    y.left.p = x
  y.p = x.p
  if x.p == T.nil
    T.root = y
  elseif x == x.p.left
    x.p.left = y
  else x.p.right = y
  y.left = x
  x.p = y 
```

Both LEFT-ROTATE and RIGHT-ROTATE run in $O(1)$.


### Ch 13.3 Insertion


```
RB-INSERT(T, z)
  y = T.nil
  x = x.root
  while x != T.nil
    y = x
    if z.key < x.key
      x = x.left
    else x = x.right
  z.p = y
  if y == T.nil
    T.root = z
  elseif z.key = z
    y.left = z
  else y.right = z
  z.left = T.nil
  z.right = T.nil
  z.color = RED
  RB-INSERT-FIXEUP(T, z)
```

```
RB-INSERT-FIXUP(T, z)
  while z.p.color == RED
    if z.p == z.p.p.left
      y = z.p.p.left
      if y.color == RED
        z.p.color = BLACK 
        y.color = BLACK 
        z.p.p.color = RED
        z = z.p.p
      

```