
# Ch 12 Binary Search Trees

### 12.1 What is a binary search tree ?

The binary search tree satisfy the binary search tree property:

 Let x be a node in a binary search tree. If y is a node in the left subtree of x, then y.key $\leq$ x.key. If y is a node in the right subtree of x, then y.key $\geq$ x.key.


```
INORDER-TREE-WALK(x)
  if x != NIL
    INORDER-TREE-WALK(x.left)
    print x.key
    INORDER-TREE-WALK(x.right)
```

**Theorem 12.1**
If x is the root of an *n*-node subtree, then the call INORDER-TREE-WALK(x) takes $\theta(n)$ time.


**Proof**
Let $T(n)$ denote the time taken by INORDER-TREE-WALK when it is called on the root of an *n*-node subtree. Since INORDER-TREE-WALK visits all *n* nodes of the subtree, we have $T(n) = \Omega(n)$. It remains to show that $T(n) = O(n)$.

Since INORDER-TREE-WALK takes a small, constant amount of time on an empty subtree (for the test x $\neq$ NIL), we have $T(0) = c$ for some constant $c > 0$. 

For $n > 0$, suppose that INORDER-TREE-WALK is called on a node x whose left subtree has k nodes and whose right subtree has $n - k  - 1$ nodes. The time to perform INORDER-TREE-WALK(x) is bounded by $T(n) \leq T(k) + T(n - k - 1) + d$ for some constantt $d > 0$ that reflects run upper bound bound on the time to execute the body of INORDER-TREE-WALK(x), exclusive of the time spent in recursive calls. 

We use the substitution method to show that $T(n) = O(n)$ by proving that $T(n) \leq (c + d) n + c$. For $n = 0$, we have $(c + d)*0 + c = c = T(0)$. For $n > 0$, we have

$$
\begin{align}
T(n) & \leq T(k) + T(n - k - 1) + d \\\\
& = ((c + d)k + c) + ((c + d)(n - k - 1) + c) + d \\\\
& = ck + dk + c + cn - ck - c + dn - dk - d + c + d \\\\
& = cn + dn + c \\\\
& = (c + d)n + c \\\\
\end{align}
$$

### 12.2 Querying a binary search tree

##### Searching

```
TREE-SEARCH(x,k)
  if x == NIL or k == x.key
    return x
  if k k < x.key
    return TREE-SEARCH(x.left, k)
  else return TREE-SEARCH(x.right, k)
```

The running time of TREE-SEARCH is $O(h)$.

```
ITERATIVE-TREE-SEARCH(x,k)
  while x != NIL and k != x.key
    if k < x.key
      x = x.left
    else x = x.right
  return x
```

##### Minimum and maximum

```
TREE-MINIMUM(x)
  while x.left != NIL
    x = x.left
  return x

TREE-MAXIMUM(x)
  while x.right != NIL
    x = x.right
  return x 
```

##### Successor and predecessor

```
TREE-SUCCESSOR(x)
  if x.right != NIL
    return TREE-MINIMUM(x.right)
  y = x.p
  while y != NIL and x == y.right
    x = y
    y = y.p
  return y
```
Let h be the height of the tree, the time complexity is $O(h)$

Theorem 12.2
We can implement the dynamic-set operations SEARCH, MINIMUM, MAXIMUM, SUCCESSOR, and PREDECESSOR so that each one runs in $O(h)$ time on a binary search tree of height h.

### 13.3 Insertion and deletion

z is a node with z.key = v, z.left = NIL, and z.right = NIL
```
TREE-INSERT(T, z)
  y = NIL
  x = T.root
  while x != NIL
    y = x
    if z.key < x.key
      x = x.left
    else x = x.right
  z.p = y
  if y == NIL
    T.root = z
  elseif z.key < y.key
    y.left = z
  else y.right = z
```

##### Deletion

There is three cases for deleting a node z from a binary search tree T.
 
1. If z has no children, modify the parent of z to replace z with NIL. 
2. If z has one children, modify the parent of z to replace z with z's child.
3. If z has two children, then there are two cases:

3a. If z's right child doesn't have a left child, modify the parent of z to replace z with z's right child. Then set new z's left child (NIL) to the original left child.

3b. If z's right child has a left child, replace z with z's right child's leftest child, name it as minimum. Need to update minimum's right child and z's left child.  

TRANSPLANT: replace one subtree as a child of its parent with another subtree.
```
TRANSPLANT
  if u.p == NIL
    T.root = v
  elseif u == u.p.left
    u.p.left = v
  else u.p.right = v
  if v != NIL
    v.p = u.p
```

```
TREE-DELETE(T, z)
  if z.left = NIL
    TRANSPLANT(T, z, z.right)
  elseif z.right == NIL
    TRANSPLANT(T, z, z.left)
  else y = TREE-MINIMUM(z.right)
    if y.p != z
      TRANSPLANT(T, y,y.right)
      y.right = z.right
      y.right.p = y
    TRANSPLANT(T, z, y)
    y.left = z.left
    y.left.p = y
```

Theorem 12.3

We can implement the dynamic-set operations INSERT and DELETE so that each one runs in O(h) time on a binary search tree of heigh t h. 

