---
title: "Hot03 无重复字符的最长子串"
subtitle: ""
date: 2022-07-25T18:16:32+08:00
draft: true
author: ""
authorLink: ""
description: ""
keywords: ""
license: ""
comment: false
weight: 0

tags: ["Mid","字符串"]
categories:
- Hot100

hiddenFromHomePage: false
hiddenFromSearch: false


toc:
  enable: true
math:
  enable: true
lightgallery: false


# See details front matter: /theme-documentation-content/#front-matter
---

给定一个字符串 `s` ，请你找出其中不含有重复字符的 **最长子串** 的长度

<!--more-->

## 1、题目

[3. 无重复字符的最长子串](https://leetcode.cn/problems/longest-substring-without-repeating-characters/)

给定一个字符串 `s` ，请你找出其中不含有重复字符的 **最长子串** 的长度

## 2、解析

滑动窗口

+ 我们使用两个指针表示字符串中的某个子串（或窗口）的左右边界，其中左指针代表着上文中「枚举子串的起始位置」，而右指针即为上文中的；

+ 在每一步的操作中，我们会将左指针向右移动一格，表示**我们开始枚举下一个字符作为起始位置**，然后我们可以不断地向右移动右指针，但需要保证这两个指针对应的子串中没有重复的字符。在移动结束后，这个子串就对应着 **以左指针开始的，不包含重复字符的最长子串**。我们记录下这个子串的长度；

+ 在枚举结束后，我们找到的最长的子串的长度即为答案。

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        HashMap<Character,Integer> map = new HashMap<>();
        int left = 0;
        if(s.length() < 1) {
            return 0;
        }
        map.put(s.charAt(0),0);
        int ans = 1;
        for(int i = 1;i < s.length();i++) {
            if(map.containsKey(s.charAt(i))) {
                left = Math.max(left,map.get(s.charAt(i)) + 1);
            }
            map.put(s.charAt(i),i);
            ans = Math.max(ans,i - left + 1);
        }
        return ans;
    }
}
```



```go
func lengthOfLongestSubstring(s string) int {
    if(len(s) <= 1){
        return len(s)
    }
    left := 0
    ans := 0
    byteMap := make(map[byte]int) 
    for i,ch := range s {
        if index,ok := byteMap[byte(ch)];ok{
            left = max(left,index+1)
        }
        byteMap[byte(ch)] = i
        ans = max(ans,i - left + 1)
    }
    return ans
}

func max(a int,b int) int {
    if a > b {
        return a
    }
    return b
}
```

