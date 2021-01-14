# Data Structure

## Hash Tables

Many applications require a dynamic set that supports only the dictionary operations INSERT, SEARCH, and DELETE. For example, a compiler that translates a programming language maintains a symbol table. A hash table is an effective data structure for implementing dictionaries. Although searching for an element in a hash table can take as long as searching for an element in a linked list - $ \theta (n) $ time in the worst case, in practice, hashing performs extremely well. Under reasonable assumptions, the average time to search for an element in a hash take is $ O(n) $.

A hash table generalizes the simpler notion of an ordinary array. Directly addressing into an ordinary position in an array makes effective use of our ability to examine an arbitrary position in an array in $ O(1) $ time. We can take advantage of direct addressing when we can afford to allocate an array that has one position for every possible key.

When the number of keys actually stored is small relative to the total number of possible keys, hash tables become an effective alternative to directly addressing an array, since a hash table typically uses an array of size proportional to the number of keys actually stored. Instead of using the key as an array index directly, the array index is computed from the key.  

### Ch 11.1 Direct-address tables

Direct addressing is a simple technique that works well when the universe U of keys is reasonably small. Suppose that an application needs a dynamic set in which each element has a key drawn from the universe $ U = \left\\{ 0, 1, \ldots, m - 1 \right\\} $, where *m* is not too large. We shall assume that no two elements have the same key. 

To represent the dynamic set, we use an array, or *direct-address table*, denoted by $T [0 .. m - 1]$, in which each position , or slot, corresponds to a key in the universe *U*. slot *k* points to an element in the set with key *k*. If the set contains no element with key *k*, then $T[k] = NIL$. 

The dictionary operations are trivial to implement:

```
DIRECT-ADDRESS-SEARCH(T,k)
	return T[k]

DIRECT-ADDRESS-INSERT(T,x)
	T[x.key] = x

DIRECT-ADDRESS-DELETE(T,x)
	T[x.key] = NIL
```
Each of these operations takes only $O(1)$ time.

![image info](./Pictures/HashTables/hashtable1.jpg )

For some applications, the direct-address table itself can hold the elements in the dynamic set. That is, rather than storing an element's key and satellite data in an object, we can store the object in the slot itself, thus saving space. We would use a special key within an object to indicate an empty slot. Moreover, it is often in the table, we have its key. If keys are not stored, however, we must have some way to tell whether the slot is empty. 

### Ch 11.2 Hash tables

The downside of direct addressing is obvious: if the universe *U* is large, storing a table T of size $|U|$ may be impractical, or even impossible, given the memory available on a typical computer. Furthermore, the set *K* of keys *actually stored* may be so small relative to *U* that most of the space allocated for *T* would be wasted. 

When the set *K* of keys stored in a dictionary is much smaller than the universe *U* of all possible keys, a hash table requires much less storage than a direct address table. Specifically, we can reduce the storage requirement to $\theta (|K|)$ while only $O(1)$ time. The catch is that this bound is for the *average-case time*, whereas for direct addressing it holds for the *worst-case time*.

With direct addressing, an element with key *K* is stored in slok *K*. With hashing, this element is stored in slot $h(K)$; that is, we use a **hash function** *h* to compute the slot from the key *k*. Here, *h* maps the universe *U* of keys into the slots of a **hash table** $T[0..m - 1]$:

$h : U \rightarrow \\{0, 1, \ldots, m - 1 \\}$,

where the size $m$ of the hash table is typically much less than $|U|$. We say that an element with key *K* hashes to slot $h(K)$; we also say that $h(K)$ is the hash value of key *K*. The hash function reduces the range of array indices and hence the size of the array. Instead of a size of $|U|$, the array can have size *m*.

There is one hitch: two keys may hash to the same slot. We call this situation a *collision*. Fortunately, we have effective techniques for resolving the conflict created by collisions. 

Of course, the ideal solution would be to avoid collisions altogether. We might try to achieve this goal by choosing a suitable hash function *h*. One idea is to make *h* appear to be "random," thus avoiding collisions or at least minimizing their number. The very term "to hash," evoking images oy random mixing and chopping , captures the spirit of this approach. 

To search for x, go to position x of A and go to the location stored there. If that location is an element of S which contains a pointer to A[x], then we know x is in A. Otherwise, $x \not\in A$


A well-designhed, "random" hash function can minimize the number of collisions. 

Collision resolution:

Chaining: put all the elements that hash to the same slot into the same linked list. 

```
CHAINED-HASH-INSERT(T,x)
	insert x at the head of list T[h(x.key)]

CHAINED-HASH-SEARCH (T,k)
	search for an element with key k in list T[h(k)]

CHAINED-HASH-DELETE(T,x)
	delete x from the list T[h(x.key)]
```

Open addressing:

