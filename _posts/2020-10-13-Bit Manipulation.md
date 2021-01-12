---
layout: post
title: Bit Manipulation
key: 20201013
tags:
  - C++
  - data structure and algorithm
  - Bit Manipulation
---

## Bit Arithmetic
* Binary Addition
```c++
string addBinary(string a, string b){
	int m=a.size(),n=b.size();
	int i=m-1,j=n-1;
	string res="";
	int temp=0;
	while(i>=0||j>=0||temp==1){
		temp+=((i>=0)?a[i]-'0':0);
		temp+=((j>=0)?b[j]-'0':0);

		res=char(temp%2+'0')+res;
		temp/=2;
		i--;j--;
	}
	return res;
}
```

* 67 Add Binary([Q](https://leetcode.com/problems/add-binary/):[A]())

## Binary, Decimal, Hexadecimal Conversion

## Power of Two
1. Get the Rightmost 1-bit
two's complement:
`-x = ~x + 1;`

``` c++
bool isPowerOfTwo(int n){
	return (n&(-n))==n;
}
```

2. Turn off the rightmost 1-bit
``` c++
bool isPowerOfTwo(int n){
	return n&(n-1)==0;
}
```

* 231 Power of Two([Q](https://leetcode.com/problems/power-of-two/):[A]())
<!--more-->
* 338 Counting Bits([Q](https://leetcode.com/problems/counting-bits/):[A]())
(Turnoff rightmost bits)
How to understand using n&(n-1) to turn off rightmost bits?
there must be only one bit that turns from 0 to 1 when adding one to any numbers, all the rest of bits that are right side of this bit will become zero, thus n&(n-1) will set all these right side of bits to be zero include this rightmost 1 bit since this rightmost bit in (n-1) must be zero.
{:.info}

## Sum using bitwise operation
* 371 Sum of two integers([Q](https://leetcode.com/problems/sum-of-two-integers/):[A]())

## XOR Operator
Imagine, you have a problem to indentify an array element (or elements), which appears exactly given number of times. Probably, the key is to build first an array bitmask using XOR operator. Examples: In-Place Swap, Single Number, Single Number II.

* 136 Single Number([Q](https://leetcode.com/problems/single-number/):[A]())
* 137 Single Number II([Q](https://leetcode.com/problems/single-number-ii/):[A]())
* 260 Single Number III([Q](https://leetcode.com/problems/single-number-iii/):[A]())



## Count set bits


## Bitwise Operation
* Bitwise And of Numbers Range([Q](https://leetcode.com/problems/bitwise-and-of-numbers-range/):[A]())
1.brute force 2.bit shift operation 3.Brian Kernighan's Algorithm
{:.info}

## Compare Strings
* 318 Maximum Product of Word Lengths([Q](https://leetcode.com/problems/maximum-product-of-word-lengths/):[A]())



