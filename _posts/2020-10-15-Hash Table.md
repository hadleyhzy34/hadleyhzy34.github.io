---
layout: post
title: Hash Table
key: 20201015
tags:
  - C++
  - data structure and algorithm
  - Hash Table
---

## String Definition

## Map
### Map Definition

```c++
//using stringstream class

//using std::stoi()
string str="45";
int num = std::stoi(str);

//int to string


```
<!--more-->

### Map Basic Operation
```c++
std::map<char,int>mymap;
//find
mymap['b']=20;
//an iterator to the element, if an element with specified key is found or map::end otherwise.
std::map<char,int>::iterator it = mymap.find('b');

//erase
mymap['c']=30;
mymap.erase('c');//erasing by key
it=mymap.find('e');
mymap.erase(it,mymap.end());//erasing by range

//loop through map
for(auto &kv:map){
	std::cout<<kv.first<<" has value "<<kv.second<<std::endl;
}

for(auto& [key,value]:map)

for(auto it=map.begin();it!=map.end();it++)

```

### std::map::lower_bound/std::map::upper_bound

```c++
std::map<char,int> mymap;
mymap['a']=10;
mymap['b']=20;
mymap['c']=30;
mymap['d']=40;
mymap['e']=50;

auto il=mymap.lower_bound('b');  //il points to b
auto iu=mymap.upper_bound('d');  //iu points to e(not)
```

## Sum
* 325 Maximum Size Subarray Sum Equals K([Q](https://leetcode.com/problems/maximum-size-subarray-sum-equals-k/):[A]())(Hash Table)


## Sort
* 274 H-Index([Q](https://leetcode.com/problems/h-index/):[A]())(hash table)
* 275 H-Index II([Q](https://leetcode.com/problems/h-index-ii/):[A]())(binary search)

## Count
* 348 Design Tic-Tac-Toe([Q](https://leetcode.com/problems/design-tic-tac-toe/):[A]())

## Design to dynamically output a range
* 362 Design Hit Counter([Q](https://leetcode.com/problems/design-hit-counter/):[A]())
