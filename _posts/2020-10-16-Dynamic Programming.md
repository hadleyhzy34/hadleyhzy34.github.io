---
layout: post
title: Dynamic Programming
key: 20201015
tags:
  - C++
  - data structure and algorithm
  - Dynamic Programming
---


## Topic
### DFS/Backtracking Intuitive approach to dynamic programming
* 322 Coin Change([Q](https://leetcode.com/problems/coin-change/):[A]())
* 518 Coin Change 2([Q](https://leetcode.com/problems/coin-change-2/):[A]())  
* 343 Integer Break([Q](https://leetcode.com/problems/integer-break/):[A]())

<!--more-->
Intuitive approach using backtracking:
```c++
// index, current index of coins vector, amount: remaining sum value, subset: current combination candidate, res: final combinations
	void backtracking(vector<int>& coins, int amount, int index, vector<int>subset,vector<vector<int>>&res){
		if(amount==0){
			res.push_back(subset);
		}
		for(int i=index;i<coins.size();i++){
			if(amount-coins[i]<0)continue;
			subset.push_back(coins[i]);
			backtracking(coins,amount-coins[i],i,subset,res);
			subset.pop_back();
		}
	}
```

What's wrong with for statements like below:
```c++
        for(int i=1;i<=amount;i++){
        	for(int j=0;j<coins.size();j++){
        		if(i-coins[j]>0){
        			dp[i]+=dp[i-coins[j]];
        		}else if(i==coins[j]){
        			dp[i]++;
        		}
        	}
            cout<<i<<" "<<dp[i]<<endl;
        }
```

test case like below:
```
Input: amount = 5, coins = [1, 2, 5]
Output: 4
Explanation: there are four ways to make up the amount:
5=5
5=2+2+1
5=2+1+1+1
5=1+1+1+1+1
```

When amount == 5, dp[5]=dp[4]+dp[3]+...
since dp[4]=dp[3]+...
there's overlapped number of ways of combinations to make up amount 3 and 4.

Going back to first backtracking code, imaging coins array all elements are sorted, and we combine different value of coins in order, then if coin[j] is the last coin to make up amount i, then all other coins that makes up amount i will be smaller than coin[j]. Then we can loop through coins first from smaller to bigger one, dp[i]=dp[i-coin[j]] means that given current amount i, there are dp[i-coin[j]] ways that can make up amount i when last coin is coin[j].

For instance, 
coins: 1,2,5
//coin 1 as last coin to make up 5
5=1+1+1+1+1;
//coin 2 as last coin to make up 5
5=1+2+2;
5=1+1+1+2;
//coin 5 as last coin to make up 5
//5=5


```c++
class Solution {
public:
    int change(int amount, vector<int>& coins) {
        int dp[amount+1];
        memset(dp,0,sizeof(dp));
        dp[0]=1;
        
        for(int coin:coins){
            for(int i=coin;i<amount+1;i++){
                dp[i]+=dp[i-coin];
            }
        }
        return dp[amount];
    }
};
```

### Subarray
* 309 Best Time to buy and sell stock with cooldown(DP, multi-states)([Q](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/):[A]())

``` c++
//backtracking demo could be transformed into multiple dp arrays
void backtracking(){
	for(auto &x:{option1, option2,...}){

	}
	return;
}

void solution(){
	int dp1[n];
	int dp2[n];
	...
}
```

* 55 Jump Game([Q](https://leetcode.com/problems/jump-game/):[A]())

* 368 Largest Divisible Subset([Q](https://leetcode.com/problems/largest-divisible-subset/):[A]())(DP)

#### 2D array
* 221 Maximal Square([Q](https://leetcode.com/problems/maximal-square/):[A]())(DFS->DP)

* 256 Paint House([Q](https://leetcode.com/problems/paint-house/):[A]())(backtracking->DP)


<!--more-->


### Math 
* 279 Perfect Squares([Q](https://leetcode.com/problems/perfect-squares/):[A]())
Be carefull the limit for the inner loop to speed up running time.
{:.warning}





