---
layout: post
title: Two Pointers
key: 20201019
tags:
  - C++
  - data structure and algorithm
  - Two Pointers
---

## Two Pointers Classical Problem
* 360 sort transformed array([Q](https://leetcode.com/problems/sort-transformed-array/):[A]())

### Sum
#### Description
Given a sorted array A, having N integers, find if there exists any pair of elements such that their sum is equal to target.
``` c++
bool isPairSum(int array[], int N, int target){
    //two pointers
    int i=0,j=N-1;

    while(i<j){
        if(array[i]+array[j]==target){
            return true;
        }else if(array[i]+array[j]<target){
            i++;
        }else{
            j--;
        }
    }
    return false;
}
```

<!--more-->

#### Follow up
find numbers of pairs of elements such that their sum is less than target.
* 11 Container With Most Water([Q](https://leetcode.com/problems/container-with-most-water/):[A]())

``` c++
int twoSum(int array[], int N, int target){
    int res=0;

    int i=0,j=N-1;
    while(i<j){
        if(array[i]+array[j]<target){
            res+=j-i;
            i++;
        }else{
            j--;
        }
    }
    return res;
}
```

#### Follow up
find numbers of three elements such that their sum is less than target.
* 259 3Sum Smaller([Q](https://leetcode.com/problems/3sum-smaller/):[A]())
* 16 3Sum Closest([Q](https://leetcode.com/problems/3sum-closest/):[A]())
* 18 4Sum([Q](https://leetcode.com/problems/4sum/):[A]())

``` c++
int threeSumSmaller(vector<int>& nums, int target) {
    if(nums.size()<3)return 0;

    int n=nums.size();

    sort(nums.begin(),nums.end());
    int count=0;
    for(int z=0;z+2<n;z++){
        int i=z+1,j=n-1;
        while(i<j){
            if(nums[z]+nums[i]+nums[j]<target){
                count+=j-i;
                i++;
            }else{
                j--;
            }
        }
    }
    return count;
}
```

