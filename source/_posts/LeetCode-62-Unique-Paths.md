---
title: 'LeetCode 62: Unique Paths'
date: 2022-07-12 00:01:18
tags:
- study
- leetcode
---

## 62. Unique Paths

###Question: 
-There is a robot on an `m x n` grid. The robot is initially located at the top-left corner (i.e., `grid[0][0]`). The robot tries to move to the bottom-right corner (i.e., `grid[m - 1][n - 1]`). The robot can only move either down or right at any point in time.

Given the two integers `m` and `n`, return the number of possible unique paths that the robot can take to reach the bottom-right corner.

The test cases are generated so that the answer will be less than or equal to 2 * 10<sup>9</sup>.

### Example 1:

![](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

    Input: m = 3, n = 7
    Output: 28

### Example 2:
    Input: m = 3, n = 2
    Output: 3
    Explanation: From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
    1. Right -> Down -> Down
    2. Down -> Down -> Right
    3. Down -> Right -> Down


### 解法:

1. **理解:** 不难发现，机器人从左上角走到右下角，需要向下走`m - 1`步，向右走`n - 1`步

2. **动态规划:** 
- 建立二维数组dp，令`dp[i][j]`表示到达 i, j的最多路径数。 
- 初始化：对于第一行 `dp[0][j]`，或者第一列 `dp[i][0]`，都只有一条路径。 
- 机器人到达位置`(i, j)`有两种方式：从`(i - 1, j)`下移和从`(i, j - 1)`右移。状态转移方程为： 

    `d p [ i ] [ j ] = d p [ i − 1 ] [ j ] + d p [ i ] [ j − 1 ]`

3. **复杂度分析:**
- 时间复杂度：*O(mn)*。遍历dp数组进行动态规划。
- 空间复杂度：*O(mn)*。创建的dp数组的大小。 

* ### 好理解版本

```
/**
 * @param {number} m
 * @param {number} n
 * @return {number}
 */
var uniquePaths = function(m, n) {
    // 创建容器数组
    let dp = Array(m).fill(0).map(() => Array(n).fill(0))

    // 最上一行和最下一行初始值为1
    for (let i = 0; i < m; i++){
        for (let j = 0; j < n; j++){
            if (i === 0 | j === 0) dp[i][j] = 1
            else{
                dp[i][j] = dp[i-1][j] + dp[i][j-1]
            }
        }
    }
    return dp[m-1][n-1]
};

// 速度 > 80%, 空间 > 40%
```

- ***接下来，还可以将时间复杂度由O(n^2)优化为O(n)，主要由于状态转移方程中，当前状态主要取决于(i - 1)行和(j - 1)列，所以并不需要保存每一行的状态***

- ***dp可以优化为一维滚动数组。当第i次遍历到dp[j]时，dp[j]表示到达(i, j)最多的路径数。递推公式为： d p [ j ] + = d p [ j − 1 ]***

```
var uniquePaths = function(m, n) {
    // 创建容器数组
    let dp = Array(n).fill(0)
    dp[0] = 1

    // 最上一行和最下一行初始值为1
    for (let i = 0; i < m; i++){
        for (let j = 1; j < n; j++){
            dp[j] += dp[j-1]
        }
    }
    return dp[n-1]
};

// 速度 > 95%, 空间 > 90%
```





