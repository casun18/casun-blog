---
title: "Hot01 两数之和"
subtitle: ""
date: 2022-07-25T18:16:09+08:00
draft: true
author: "casun"
authorLink: ""
description: ""
keywords: "easy"
license: ""
comment: false
weight: 0

tags: ["Easy","数组"]
categories: ["HOT100"]

hiddenFromHomePage: false
hiddenFromSearch: false

summary: ""

toc:
  enable: true
math:
  enable: false
lightgallery: false
seo:
  images: []

# See details front matter: /theme-documentation-content/#front-matter
---

### 1. 两数之和

<!--more-->

给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。 

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer,Integer> map = new HashMap<>();
        for(int i = 0;i < nums.length;i++) {
            if(map.containsKey(target-nums[i])){
                return new int[]{i,map.get(target-nums[i])};
            }
            map.put(nums[i],i);
        }
        return new int[]{0,0};
    }
}
```



```go
func twoSum(nums []int, target int) []int {
    numsMap := make(map[int]int)
    for i,num := range nums {
        if idx, ok := numsMap[target-num];ok{
            res := []int{i,idx}
            return res
        }
        numsMap[num] = i
    }

    return []int{0,0}
}
```

