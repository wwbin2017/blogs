---
title: regular_expression_matching
date: 2018-12-01 11:01:36
tags: leetcode
---

## LeetCode 题目：Regular Expression Matching 难度：hard

Given an input string (s) and a pattern (p), implement regular expression matching with support for '.' and '*'.

> '.' Matches any single character.
> '*' Matches zero or more of the preceding element.

The matching should cover the entire input string (not partial).

Note:

s could be empty and contains only lowercase letters a-z.
p could be empty and contains only lowercase letters a-z, and characters like . or *.

这初见这个完全不知道怎么做，看了讨论能，发现暴力法就可以过，记录下，后面在思考下DP方法。

```C++
class Solution {
public:
    bool isMatch(string s, string p) {
        return isMatch(0,s,0,p);    
    }
    bool isMatch(int i, string& s, int j, string &p) {
        int sn = s.size(), pn = p.size();
        if(j == pn) return i == sn;
        if(j < pn -1 && p[j+1]=='*') {
            // 当出现*的时候，选择不匹配
            if(isMatch(i, s, j+2, p))return true;
            // 当出现*的时候，选择匹配
            if(i < sn && (s[i] == p[j] || p[j] == '.')) {
                if(isMatch(++i, s, j, p))return true;
            }
        } else {
            if(i < sn && (s[i] == p[j] || p[j] == '.')) {
                if(isMatch(++i, s, ++j, p))return true;
            }
        }
        return false;
    }
};
```
