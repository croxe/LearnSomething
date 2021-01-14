
# 算法 - 双指针总结

双指针是一种思想，一种技巧或一种方法，并不是什么特别具体的算法，在**二分查找**等算法中经常用到这个技巧。具体就是用两个变量动态存储两个或多个结点，来方便我们进行一些操作。通常用在**线性的数据结构**中，比如**链表和数组**，有时候也会用在**图算法**中。特别是链表类的题目，经常需要用到两个或多个指针配合来记忆链表上的节点，完成某些操作。链表这种数据结构也是树形结构和图的原型，所以有时候在关于图和树形结构的算法题目中也会用到双指针。

### 快慢指针
类似于龟兔赛跑，两个链表上的指针从同一节点出发，其中一个指针前进速度是另一个指针的两倍。利用快慢指针可以用来解决某些算法问题，比如

1. 计算链表的中点：快慢指针从头节点出发，每轮迭代中，快指针向前移动两个节点，慢指针向前移动一个节点，最终当快指针到达终点的时候，慢指针刚好在中间的节点。
2. 判断链表是否有环：如果链表中存在环，则在链表上不断前进的指针会一直在环里绕圈子，且不能知道链表是否有环。使用快慢指针，当链表中存在环时，两个指针最终会在环中相遇。
3. 判断链表中环的起点：当我们判断出链表中存在环，并且知道了两个指针相遇的节点，我们可以让其中任一个指针指向头节点，然后让它俩以相同速度前进，再次相遇时所在的节点位置就是环开始的位置。
4. 求链表中环的长度：只要相遇后一个不动，另一个前进直到相遇算一下走了多少步就好了
5. 求链表倒数第k个元素：先让其中一个指针向前走k步，接着两个指针以同样的速度一起向前进，直到前面的指针走到尽头了，则后面的指针即为倒数第k个元素。（严格来说应该叫先后指针而非快慢指针）
如果有其它的想法，可以评论区评论一下~

伪代码:
```
l = 0
r = 0
while 没有遍历完
  if 一定条件
    l += 1
  r += 1
return 合适的值
```

> ~~26.Remove Duplicates from Sorted Array（Easy)~~
> 141.Linked List Cycle (Easy)
> 142.Linked List Cycle II（Medium）
> 287.Find the Duplicate Number（Medium）
> 202.Happy Number (Easy)

[**26. Remove Duplicates from Sorted Array（Easy）**](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)

给定一个排序数组，你需要在 **原地** 删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在 **原地** 修改输入数组 并在使用 O(1) 额外空间的条件下完成。

伪代码:
```
l = 0
r = 0
while 没有遍历完
  if 比较两个指针的元素，如果不一样，则需要删除重复元素。
	需要一个额外的指针去指向新数组。
    l += 1
  r += 1
return 新数组的长度
```

```java
public int removeDuplicates(int[] nums) {
    int l = 0;
    int r = 0;
    if (nums.length == 0){return 0;}
    int temp = 1;
    while(r < nums.length){
        if(nums[l] != nums[r]){
            nums[temp] = nums[r];
            l = r;
            temp += 1;
        }
        r += 1;
    }
    return temp;
}
```

优化后

```
public int removeDuplicates(int[] nums) {
    int l = 0;
    int r = 1;
	//去除空数组检查，题目貌似不考这
	//去除temp，“l”即可替代temp，并且 l == temp + 1
    while(r < nums.length){
        if(nums[l] != nums[r]){
            l++;
            nums[l] = nums[r];
        }
        r++;
    }
    return l+1;
}
```

### 碰撞指针
一般都是排好序的数组或链表，否则无序的话这两个指针的位置也没有什么意义。特别注意两个指针的循环条件在循环体中的变化，小心右指针跑到左指针左边去了。常用来解决的问题有

1. 二分查找问题
	```java
	int binarySearch(int[] nums, int target) {
	    int left = 0;
	    int right = nums.length - 1;
	    while(left <= right) {
	        int mid = (right + left) / 2;
	        if (nums[mid] == target)
	            return mid;
	        else if (nums[mid] < target)
	            left = mid + 1;
	        else if (nums[mid] target)
	            right = mid - 1;
	    }
	}
	```

2. n数之和问题：比如两数之和问题，先对数组排序然后左右指针找到满足条件的两个数。如果是三数问题就转化为一个数和另外两个数的两数问题。以此类推。

伪代码:
```
l = 0
r = n - 1
while l < r
  if 找到了
    return 找到的值
  if 一定条件1
    l += 1
  else if  一定条件2
    r -= 1
return 没找到
```

> 16.3 Sum Closest (Medium)
> ~~167. Two Sum II - Input array is sorted (Easy)~~
> ~~345. Reverse Vowels of a String~~
> ~~633. Sum of Square Numbers (Medium)~~
> 713.Subarray Product Less Than K (Medium)
> 977.Squares of a Sorted Array (Easy)
> Dutch National Flag Problem

下面是二分类型

> 33.Search in Rotated Sorted Array (Medium)
> 875.Koko Eating Bananas（Medium）
> 881.Boats to Save People（Medium）


[**167. Two Sum II - Input array is sorted**](https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/)

```
public int[] twoSum(int[] numbers, int target) {
    int l = 0;
    int r = numbers.length - 1;
    while(l < r){
        if(numbers[l] + numbers[r] == target){
            return new int[]{l+1, r+1};
        }
        if(numbers[l] + numbers[r] > target){
            r--;
        }else{
            l++;
        }
    }
    return new int[]{};
}
```

[**633. Sum of Square Numbers**](https://leetcode-cn.com/problems/sum-of-square-numbers/)

```
public boolean judgeSquareSum(int c) {
    int l = 0;
    int r = (int)(Math.sqrt(c));
    while(l <= r){
        if(l*l + r*r == c){
            return true;
        }
        if(l*l + r*r > c){
            r--;
        }else{
            l++;
        }
    }
    return false;
}
```

[**345. Reverse Vowels of a String**](https://leetcode-cn.com/problems/reverse-vowels-of-a-string/)

```
public String reverseVowels(String s) {
    int l = 0;
    char[] charArr = s.toCharArray();
    int r = charArr.length - 1;
    while(r > l){
        if(!isVowel(charArr[l])){
            l++;
        }
        if(!isVowel(charArr[r])){
            r--;
        }else if(isVowel(charArr[l])){
            char temp = charArr[l];
            charArr[l] = charArr[r];
            charArr[r] = temp;
            l++;
            r--;
        }
    }
    return String.valueOf(charArr);
}

public Boolean isVowel(char temp) {
    return temp == 'e' || temp == 'i' || temp == 'a' || temp == 'o' || temp == 'u' ||
        temp == 'E' || temp == 'I' || temp == 'A' || temp == 'O' || temp == 'U';
}
```

### 滑动窗口法
两个指针，一前一后组成滑动窗口，并计算滑动窗口中的元素的问题。

这类问题一般包括

1. 字符串匹配问题

2. 子数组问题

伪代码:
```
l = 0
r = k
while 没有遍历完
  自定义逻辑
  l += 1
  r += 1
return 合适的值
```

> 1456.Maximum Number of Vowels in a Substring of Given Length（Medium）