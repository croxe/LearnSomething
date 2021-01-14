# Data Structure

## Linked lists

A linked list is a data structure in which the objects are arranged in a linear order. Unlike an array, however, in which the linear order is determined by the array indices, the order in a liked list is determined by a pointer in each object. Linked list provide a simple, flexible representation for dynamic sets, supporting all the operations on dynamic sets. 

SEARCH (S,k)

> A query that, given a set S and a key value k, returns a pointer x to an element in S such that x.key = k, or NIL if no such element belongs to S.

INSERT (S,x)

> A modifying operation that augments the set S with the element pointed to by x. We usually assume that any attributes in element x needed by the set implementation have already been initialized.

DELETE (S,x)

> A modifying operation that, given a pointer x to an element in the set S, removes x from S. (Note that this operation takes a pointer to an element x, not a key value.)

MINIMUM (S)

> A query on a totally ordered set S that returns a pointer to the element of S with the smallest key.

MAXIMUM (S)

> A query on a totally ordered set S that returns a pointer to the element of S with the largest key.

SUCCESSOR (S,x)

> A query that, given an element x whose key is from a totally ordered set S, returns a pointer to the next larger element in S, or NIL if x is the maximum element.

PREDECESSOR (S,x)

> A query that, given an element x whose key is from a totally ordered set S, returns a pointer to the next smaller element in S, or NIL if x is the minimum element.

Each element of a doubly linked list L is an object with an attribute key and two other pointer attributes: next and prev. The object may also contain other satellite data. Given an element x in the list, x.next points to its successor in the linked list, and x.prev points to its predecessor. If x.rev = NIL, the element x has no predecessor and is therefore the first element, or head of the list. If x.next = NIL, the element x has no successor and therefore the last element, or tail of the list. An attribute L.head points to the first element of the list. If L.head = NIL, the list is empty. 

A list may have one of several forms. It may be either singly linked or doubly linked, it may be sorted or not, and it may be circular or not. If a list a singly linked, we omit the prev pointer in each element. If a list is sorted, the linear order of the list corresponds to the linear order of keys stored in elements of the list; the minimum element is then the head of the list, and the maximum element is the tail. If the list is unsorted, the elements can appear in any order. In a circular list, the prev pointer of the head of the list points to the tail, and the next pointer of elements. 

(We assume the lists in the book is unsorted and doubly linked)

### Searching a linked list

The procedure LIST-SEARCH(L,k) finds the first element with key k in list L by a simply linear search, returning a pointer to this element. If no object with key k appears in the list, then the procedure returns NIL. 

```
LIST-SEARCH(L,k)
x = L.head
while x != NIL and x.key != k
    x = x.next
return x
```

To search a list of n objects, the LIST-SEARCH procedure takes $\theta (n) $ time in the worst case, since it may have to search to the entire list.

### Inserting into a linked list

Given an element x whose key attribute has already been set. the LIST-INSERT procedure "splices" x onto the front of the linked list.

```
LIST-INSERT(L,x)
x.next = L.head
if L.head != NIL
    L.head.prev = x
L.head = x
x.prev = NIL
```

The running time for LIST-INSERT on a list of n elements is O(1).

### Deleting from a linked list

The procedure LIST-DELETE removes an element x from a linked list L. It must be given a pointer to x, and it then "splices" x out of the list by updating pointers. If we wish to delete an element with a given key, we must first call LIST-SEARCH to retrieve a pointer to the element. 

```
LIST-DELETE(L,x)
if x.prev != NIL
    x.prev.next = x.next
else L.head = x.next
if x.next != NIL
    x.next.prev = x.prev
```

LIST-DELETE runs in O(1) time, but if we wish to delete an element with a given key, $\theta (n)$ time is required in the worst case because we must first call LIST-SEARCH to find the element. 

### Sentinels

The code for LIST-DELETE would be simpler if we could ignore the boundary conditions at the head and tail of the list:

```
LIST-DELETE'(L,x)
x.prev.next = x.next
x.next.prev = x.prev
```

```
LIST-SEARCH'(L,k)
x = L.nil.next
while x != L.nil and x.key != k
    x = x.next
return x
```

```
LIST-INSERT'(L,x)
x.next = L.nil.next
L.nil.next.prev = x
L.nil.next = x
x.prev = L.nil
```

A sentinel is a dummy object that allows us to simplify boundary conditions. For example, suppose that we provide with list L an object L.nil that represents NIL but has all the attributes of the other objects in the list. Whenever we have a reference to NIL in list code, we replace it by a reference to the sentinel L.nil. This change turns a regular doubly linked list into a circular, doubly linked list with a sentinel, in which the sentinel L.nil lies between the head and tail. The attribute L.nil.next points to the head of the list, and L.nil.prev points to the tail. Similarly, both the next attribute of the tail and the prev attribute of the head point to L.nil. Since L.nil.next points to the head, we can eliminate the attribute L.head altogether, replacing references to it by references to L.nil.next. 

Sentinels rarely reduce the asymptotic time bounds of data structure operations, but they can reduce constant factors. The gain from using sentinels within loops is usually a matter of clarity of code rather than speed. In same situations, the use of sentinels helps to tighten the code in a loop, thus reducing the coefficient of. Where there are many small lists, the extra storage used by their sentinels can represent significant wasted memory. 

## Implementing pointers and objects

### A multiple-array representation of objects

We can represent a collection of objects that have the same attributes by using an array for each attribute. We can implement the linked list with three arrays. The array key holds the values of the keys currently in the dynamic set, and the pointers reside in the arrays next and prev. For a given array index x, the array entries key[x], next[x], and prev[x] represent an object in the linked list. Under a pointer x is simply a common index into the key, next, and prev arrays. The next of tail can be represent as NIL, 0, or -1. A variable holds the index of the head of the list. 

### A single-array representation of objects

The words in a computer memory are typically addressed by integers from 0 to M - 1, where M is a suitably large integer. In many programming languages, an object occupies a contiguous set of locations in the computer memory. A pointer is simply the address of the first memory location of the object, and we can address other memory locations within the object by adding an offset to the pointer. 

We can use the same strategy for implementing objects in programming environments that do not provide explicit pointer data types. An object occupies a contiguous subarray A[j..k]. Each attribute of the object corresponds to an offset in the range from 0 to k - j, and a pointer to the object is the index j. 

The single-array representation is flexible in that it permits objects of different lengths to be stored in the same array. The problem of managing such a heterogeneous collection of objects is more difficult than the problem of managing a homogeneous collection, where all objects have the same attributes. Since most of the data structures we shall consider are composed of homogeneous elements, it will be sufficient for our purposes to use the multiple-array representation of objects. 

### Allocating and freeing objects

To insert a key into a dynamic set represented by a doubly linked list, we must allocate a pointer to a currently unused object in the linked-list representation. Thus, it is useful to manage the storage of object. In some systems, a garbage collector is responsible for determining which objects are unused. Many applications, however, are simple enough that they can bear responsibility for returning an unused object to a storage manager. 

Suppose that the arrays in the multiple-array representation have length m and that at some moment the dynamic set contains n $ \leq $ m elements. Then n objects represent elements currently in the dynamic set, and the remaining m - n objects are free. The free objects are available to represent elements inserted into the dynamic set in the future. 

We keep the free objects in a singly linked list, which we call the free list. The free list uses only the next array, which stores the next pointers within the list. The head of the free list set represented by linked list L is nonempty, the free list may be intertwined with list L. Note that each object in the representation is either in list L or in the free list, but not in both. 

The free list acts like a stack: the next object allocated is the last one freed. We can use a list implementation of the stack operations PUSH and POP to implement the procedures for allocating and freeing objects. We assume that the global variable free used in the following procedures points to the first element of the free list. 

```
ALLOCATE-OBJECT()
if free == NIL
    error "out of space"
else x = free
    free =  x.next
    return x 

FREE-OBJECT(x)
x.next = free
free = x 
```

The free list initially contains all n unallocated objects. Once the free list has been exhausted, running the ALLOCATE-OBJECT procedure signals an error. We can even service several linked lists with just a single free list. The two procedures run O(1) time, which makes them quite practical. We can modify them to work for any homogeneous collection of objects by letting any one of the attributes in the object act like a next attribute in the free list. 
