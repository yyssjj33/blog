---
title: "27 - Remove Element"
date: 2018-10-31T20:18:34-04:00
tags: ["leetcode", "array"]
categories: ["leetcode"]
---

## Description

Given an array nums and a value val, remove all instances of that value in-place and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

Example 1:
```
Given nums = [3,2,2,3], val = 3,

Your function should return length = 2, with the first two elements of nums being 2.

It doesn't matter what you leave beyond the returned length.
```

Example 2:
```
Given nums = [0,1,2,2,3,0,4,2], val = 2,

Your function should return length = 5, with the first five elements of nums containing 0, 1, 3, 0, and 4.

Note that the order of those five elements can be arbitrary.

It doesn't matter what values are set beyond the returned length.
```

## Thoughts

Use two pointers, i promotes from beginning to end, j promotes from end to beginning, if `nums[i] == val` and `nums[j] != val`, we just swap them in-place.

## Code

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int i = 0;
        int j = nums.length-1;
        
        while (i < j) {
            while(i < j && nums[i] != val) i++;
            while(i < j && nums[j] == val) j--;
            swap(nums, i, j);
        }
        i = 0;
        for (; i < nums.length; i++) {
            if (nums[i] == val) return i;
        }
        return i;
    }
    private void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
```

## Complexity

Time Complexity: `O(n)`
Space Complexity: `O(1)`

