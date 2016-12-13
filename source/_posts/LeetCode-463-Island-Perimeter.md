---
title: '[LeetCode]463. Island Perimeter'
date: 2016-11-23 10:01:55
categories: "Algorithms"
tags:
- 学习
---

### 问题描述 ###
给定一个二维地图，1表示陆地，0表示水域。每一个陆地
是边长为1的正方形。求岛屿的周长。
<!-- more -->

### 解题思路 ###
每个格子周长为4，两个格子相邻时周长-2
### 具体代码 ###
**python**
```python
class Solution(object):
    def islandPerimeter(self, grid):
        ans = 0
        h = len(grid)
        w = len(grid[0]) if h else 0
        for x in range(h):
            for y in range(w):
                if grid[x][y] == 1:
                    ans += 4
                    if x > 0 and grid[x-1][y]:
                        ans -= 2
                    if y > 0 and grid[x][y-1]:
                        ans -= 2
        return ans
```

**Java**
```java
public class Solution {
    public int islandPerimeter(int[][] grid) {
        int ans = 0;
        int h = g.length;
        int w = g[0].length;
        for(int i=0;i<h;i++){
            for (int j=0;j<w;j++){
                if (g[i][j] == 1){
                    ans += 4;
                    if(i > 0 && g[i-1][j] == 1) ans -= 2;
                    if(j > 0 && g[i][j-1] == 1) ans -= 2;
                }
            }
        }
        return ans
    }
}
```
