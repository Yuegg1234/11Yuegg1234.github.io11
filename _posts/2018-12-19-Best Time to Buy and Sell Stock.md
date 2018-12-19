---
layout:     post
title:      Best Time to Buy and Sell Stock
date:       2018-12-19
author:     Yuegg
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - leetcode
---
# 121. Best Time to Buy and Sell Stock

  给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。
如果你最多只允许完成一笔交易（即买入和卖出一支股票），设计一个算法来计算你所能获取的最大利润。
注意你不能在买入股票前卖出股票。

示例 1:
```
输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。
```

示例 2:
```
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

解答：
动态规划，转移方程为max(前一天的最大利润，今天的股票价格减去之前股票价格的最小值)

```java
class Solution {
    public int maxProfit(int[] prices) {
        if(prices.length == 0){
            return 0;
        }
        int[] dp = new int[prices.length];
        int[] mins = new int[prices.length];
        mins[0] = prices[0];
        for (int i=1; i<mins.length; i++){
           mins[i] = Math.min(prices[i], mins[i-1]);
        }
        
        for(int i=1; i<dp.length; i++){
            dp[i] = Math.max(dp[i-1], prices[i]-mins[i]);
        }
        return dp[dp.length-1];
    }
}
```
