---
title: candy
date: 2018-11-24 23:53:58
tags: leetcode
---

## LeetCode 题目：candy 难度：hard
There are N children standing in a line. Each child is assigned a rating value.

You are giving candies to these children subjected to the following requirements:

Each child must have at least one candy.
Children with a higher rating get more candies than their neighbors.
What is the minimum candies you must give?

时间复杂度O(n)： 空间复杂度： O(1)

```C++
class Solution {
public:
    int candy(vector<int> &ratings) {
        if(ratings.size() <=1) return ratings.size();
        int index = 0;
        int pre = 1;
        int sum = 1;
        int gap = 0;
        for(int i = 1; i< ratings.size(); i++){
            if(ratings[i] < ratings[i-1]){
                if(pre <= 1){
                    if(gap > 1){
                        sum -= 1;
                        gap--;
                    }
                    sum += i - index;
                }
                if(pre > 2)
                    gap = pre -1;
                pre = 1;
                sum += pre;
            } else if(ratings[i] == ratings[i-1]){
                index = i;
                pre = 1;
                sum+=pre;
                gap = 0;
            }else {
                pre += 1;
                sum += pre;
                index = i;
                gap = 0;
            }
        }
        return sum;
    }
};
```
