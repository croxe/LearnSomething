
Input: A sequence of n numbers $\langle a\_1, a\_2, \ldots, a\_n \rangle$

Output: A permutation (reordering) $\langle a'\_1, a'\_2, \ldots, a'\_n \rangle$ of the input sequence such that $ a'\_1 \le a'\_2 \le \ldots \le a'\_n $

```
INSERTION-SORT(A)
  for j = 2 to A.length
    key = A[j]
    // Insert A[j] into the sorted sequence A[1..j-1].
    i = j - 1
    while i > 0 and A[i] > key
      A[i + 1] = A[i]
      i = i - 1 
      A[i + 1] = key
```