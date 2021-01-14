# Data Structure

## Stacks and queues

**Def:** Stacks and queues are dynamic sets in which the element removed from the set by the *DELETE* operation is prespecified. 

The stack implements a last-in, first-out, LIFO. The queue implements first-in, first-out, FIFO. 

### Stacks

The *INSERT* operation on a stack is often called *PUSH*, and *DELETE* operation is called *POP*.

For a stack S[1..n], the array has n attribute S.top that indexes the most recently insert element. The stack consists of elements S[1..S.top], where S[1] is the element at the bottom of the stack and S[S.top] is the element at the top. When S.top = 0, the stack contains no elements and is empty. We use *STACK-EMPTY* to check whether the stack is empty. If we attempt to pop an empty stack, we say stack underflows, which is normally an error. If S.top exceeds n, the stack overflows. 

```
STACK-EMPTY(S)
if S.top == 0
    return True
else return False
```

```
PUSH(S,x)
S.top = S.top + 1
S[S.top] = x
```

```
POP(S)
if STACK-EMPTY(S)
    error "underflow"
else S.top = S.top - 1
    return S[S.top + 1]
```

All three stack operation takes O(1) time.



### Queues

We call the *INSERT* operation ENQUEUE, and we call the *DELETE* operation *DEQUEUE*, like the stack operation POP, DEQUEUE takes no element argument. The queue has a head and a tail. One way to implement a queue of at most n - 1 elements using an array Q[1..n]. The queue has an attribute Q.head that indexes, or points to, its head. The attribute Q.tail indexes next location at which a newly arriving element will be inserted into the queue. The elements in the queue reside in locations Q.head, Q.head + 1, ... , Q.tail - 1, where we “wrap around” in the sense that location 1 immediately follows location n in a circular order. Initially, we have Q.head = Q.tail = 1. If we attempt to dequeue an element from an empty queue, the queue underflows. When Q.head = Q.tail + 1, the queue is full, and if we attempt to enqueue an element, then the queue overflows.

```
ENQUEUE(Q,x)
if Q.tail == Q.length
    if Q.head == 1
        error "overflow"
else if Q.head = Q.tail + 1
    error "overflow"
Q[Q.tail] = x
if Q.tail == Q.length
    Q.tail = 1
else Q.tail = Q.tail + 1
```

```
DEQUEUE(Q)
if Q.head == Q.tail
    error "underflow"
x = Q[Q.head]
if Q.head == Q.length
    Q.head = 1
else Q.head = Q.head + 1
return x
```

10.1-5
Whereas a stack allows insertion and deletion of elements at only one end, and a queue allows insertion at one end and deletion at the other end, a deque allows insertion and deletion at both ends. Write four O(1)-time procedures to insert elements into and delete elements from both ends of a deque implemented by an array.

```
ENQUE_HEAD(Q)
if Q.tail == Q.length
    if Q.head == 1
        error "overflow"
else if Q.head = Q.tail + 1
    error "overflow"
Q[Q.tail] = x
if Q.tail == Q.length
    Q.tail = 1
else Q.tail = Q.tail + 1

DEQUE_HEAD(Q)
if Q.tail == Q.head
    error "underflow"
x = Q[Q.tail]
if Q.tail == Q.length
    Q.tail = Q.length
else Q.tail = Q.tail - 1
return x

ENQUE_TAIL(Q)
if Q.tail == Q.length
    if Q.head == Q.length
        error "overflow"
else if Q.tail = Q.head - 1
    error "overflow"
Q[Q.head] = x
if Q.head == Q.length
    Q.head = Q.length
else Q.head = Q.head - 1

DEQUE_TAIL(Q)
if Q.head == Q.tail
    error "underflow"
x = Q[Q.head]
if Q.head == Q.length
    Q.head = 1
else Q.head = Q.head + 1
return x

ALL O(1)
```

10.1-6
Show how to implement a queue using two stacks. 

| Stack1 |
| ------ |
| 3      |
| 2      |
| 1      |

Pop, push, and swap order

| Stack2 |
| ------ |
| 1      |
| 2      |
| 3      |

```
ENQUEUE(S1,x)
PUSH(S1,x)

O(1)

DEQUEUE(S1,S2,x)
if STACK-EMPTY(S2)
    for i in 0..S1.length-1
        push(S2,pop(S1))
else x = pop(S1)
return x

O(n)
```

10.1-7

| Queue1 | 1    | 2   | 3    |
| ------ | ---- | --- | ---- |
| -      | head | -   | tail |

| Queue2 | Null | 2   | 1    |
| ------ | ---- | --- | ---- |
| -      | head | -   | tail |

```

```


## Representing rooted trees

The methods for representing lists given in the previous section extend to any homogeneous data structure. We look specifically at the problem of representing rooted trees by linked data structures. We first look at binary trees and then we present a method for trees in which nodes can have an arbitrary number of children. We represent each node of a tree by an object. As with linked lists, we assume that each node contains a key attribute. The remaining attributes of interest are pointers to other nodes, and they vary according to the type of tree. 

### Binary trees

p, left, and right to store pointers to the parent, left child, and right child of each node in a binary tree T. If x.p = NIL, then x is the root. If node x has no left child, then x.left = NIL, and similarly for the right child. The root of the entire tree T is pointed to by the attribute T.root. If T.root = NIL, then the tree is empty. 

### Rooted trees with unbounded branching

We can extend the scheme for representing a binary tree to any class of trees in which the number of children of each node is at most some constant k: we replace the left and right attributes by $child\_1, child\_2, \ldots, child\_k$. This scheme no longer works when the number of children of a node is unbounded, since we do not know how many attributes to allocate in advance. Moreover, even if the number of children *k* is bounded by a large constant but most nodes have a small number of children, we may waste a lot of memory. 

We can take the advantage of using only $O(n)$ space for any *n*-node rooted tree. The left-child, right-sibling representation. As before, each node contains a parent pointer *p*, and *T.root* points to the root of tree *T*. Instead of having a pointer to each of its children, however, each node x has only two pointers:

1. x.left-child points to the leftmost child of node x, and
2. x.right-sibling points to the sibling of x immediately to its right. 

If node x has no children, then x.left-child = NIL, and if node x is the rightmost child of its parent, then x.right-sibling = NIL.

### Other tree representation

We sometimes represent rooted trees in other ways. We can represent a heap, which is based on a complete binary tree, by a single array plus the index of the last node in the heap. Some trees can only traverse toward the root, and only the parent pointers are present; there are no pointers to children. Many other schemes are possible. Which scheme is best depends on the application. 




