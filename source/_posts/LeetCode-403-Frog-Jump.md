---
title: 'LeetCode 403: Frog Jump'
date: 2022-07-14 22:58:27
tags:
- study
- leetcode
---

## 403. Frog Jump (Hard)

### Question:
A frog is crossing a river. The river is divided into some number of units, and at each unit, there may or may not exist a stone. The frog can jump on a stone, but it must not jump into the water.

Given a list of `stones`' positions (in units) in sorted **ascending order**, determine if the frog can cross the river by landing on the last stone. Initially, the frog is on the first stone and assumes the first jump must be `1` unit.

If the frog's last jump was `k` units, its next jump must be either `k - 1`, `k`, or `k + 1` units. The frog can only jump in the forward direction.

 

### Example 1:

    Input: stones = [0,1,3,5,6,8,12,17]
    Output: true
    Explanation: The frog can jump to the last stone by jumping 1 unit to the 2nd stone, then 2 units to the 3rd stone, then 2 units to the 4th stone, then 3 units to the 6th stone, 4 units to the 7th stone, and 5 units to the 8th stone.

### Example 2:

    Input: stones = [0,1,2,3,4,8,9,11]
    Output: false
    Explanation: There is no way to jump to the last stone as the gap between the 5th and 6th stone is too large.
 

### 解法

**动态规划**

    状态转移方程：
    dp[i][k] = dp[j][k-1] || dp[j][k] || dp[j][k+1]

**解析**

1.  首先很明确每一个点由上一个点跳跃过来的有可能的最大值就是这个点的index (画一下就知道了)
2.  **!**上述方程: 第一层arr表示index (i是当前ind, j为上一个, 也可能再上一个等等), 第二层arr表示之前的**所有有可能的石头位置**跳到当前ind所用的距离. (如果是某个距离,则在该距离对应的ind下标记为true, 表明他可能是由前面的某个石头花了k个距离跳来的)
3. 从等号右边找对应, 如果`之前的(所有的可能性, 后面会用到遍历, 注意j不仅仅只是上一个)石头跳到前一个石头的距离`和`前一个石头跳到当前位置距离差距`只有1内, 那么这个可能性存在

### 上代码

```
/**
 * @param {number[]} stones
 * @return {boolean}
 */
var canCross = function(stones) {
    let n = stones.length;
    let dp = new Array(n).fill(0).map(()=>new Array(n).fill(0))
    dp[0][0] = true
    
    for (let i = 1; i < n; i++){
        if (stones[i] - stones[i-1] > i) return false
    }
    
    for (let i = 1; i < n; i++){
        for (let j = i-1; j >= 0; j--){
            console.log('新的j', j, 'i为', i)
            let diff = stones[i] - stones[j] // 当前i和之前的某一个i(j)的距离, 下一次遍历则是比较再前一个(j--), 如果再前一个也可以跳到这里, 那么这个差距也存储 (相当于把能跳到这里的所有可能的跳跃距离都存上了!)
            if (diff > j + 1) break // 如果扫描到离得很远以至于diff比ind差更远的,就直接跳过啦
            dp[i][diff] =  dp[j][diff - 1] || dp[j][diff] || dp[j][diff + 1] (注意这里不仅比较一个j,还有j--, 比较所有j能跳到这里的距离, 相当于如果前一个距离这里太近还不到diff-1(不符合), 则下一次遍历会去找到j--,相当于再前一个跳到这里的距离)
            if (dp[i][diff] && i === n-1) return true
        }
    }
    
    return false
    
};
```

