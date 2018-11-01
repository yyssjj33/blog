---
title: "113-Path Sum II"
date: 2018-10-31T22:35:21-04:00
tags: ["leetcode", "tree"]
categories: ["leetcode"]
---

## Description

Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

Note: A leaf is a node with no children.

Example:
```
Given the below binary tree and sum = 22,

      5
     / \
    4   8
   /   / \
  11  13  4
 /  \    / \
7    2  5   1
Return:

[
   [5,4,11,2],
   [5,8,4,5]
]
```

## Thoughts

Use DFS to traverse from root to leaf, when we visit one node, subtract `node.val` from the sum, when we meet the leaf and the sum is 0, we find on path.

## Code

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) return res;
        dfs(root, sum, new ArrayList<Integer>(), res);
        return res;
    }
  
    void dfs(TreeNode node, int sum, List<Integer> cur, List<List<Integer>> res) {
        if (node.left == null && node.right == null && sum == node.val) {
            cur.add(node.val);
            res.add(new ArrayList(cur));
            cur.remove(cur.size()-1);
            return;
        }    
        cur.add(node.val);
        if (node.left != null) dfs(node.left, sum-node.val, cur, res);
        if (node.right != null) dfs(node.right, sum-node.val, cur, res);
        cur.remove(cur.size()-1);
    }
}
```

## Complexity

Time Complexity: `O(n)`
Space Complexity: `O(lg(n))` (stack space)