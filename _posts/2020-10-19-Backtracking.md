---
layout: post
title: Backtracking and DFS
key: 20201019
tags:
  - C++
  - data structure and algorithm
  - Backtracking
  - DFS
---

## String Definition

### Standard Backtracking
* 294 Flip Game II([Q](https://leetcode.com/problems/flip-game-ii/):[A]())
* 320 Generalized Abbreviation([Q](https://leetcode.com/problems/generalized-abbreviation/):[A]())

## Permutations
### Permutations for dictinct data variables
```c++
void permutation(vector<int> &num, int l, vector<vector<int> > &res) {
    if (l == num.size()-1) {
        res.push_back(num);
        return;
    }
        
    for (int i = l; i < num.size(); i++) {
        swap(num[i], num[l]);
        permutation(num, l+1, res);
        swap(num[i], num[l]);
    }
}
```
<!--more-->


### Permutations for duplicated data variables
```c++
void permu(vector<int> nums, int l, vector<vector<int>>&res){
    if(l==nums.size()-1){
        res.push_back(nums);
    }
    for(int i=l;i<nums.size();i++){
        if(i==l||nums[i]!=nums[l]){
            swap(nums[l],nums[i]);
            permu(nums, l+1, res);
        }
    }
}
```

* 276 Palindrome Permutation II([Q](https://leetcode.com/problems/palindrome-permutation-ii/):[A]())

## Combinations


# DFS

* 364 Nested List Weight Sum II([Q](https://leetcode.com/problems/nested-list-weight-sum-ii/):[A]())

Note that when reversely assigning or returning depth of nested list, using hash table as global variable to store value then loop through.  
{:.info}

* 341 Flatten Nested List Iterator([Q](https://leetcode.com/problems/flatten-nested-list-iterator/):[A]())



