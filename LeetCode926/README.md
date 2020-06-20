# 926. 将字符串翻转到单调递增

如果一个由 '0' 和 '1' 组成的字符串，是以一些 '0'（可能没有 '0'）后面跟着一些 '1'（也可能没有 '1'）的形式组成的，那么该字符串是单调递增的。

我们给出一个由字符 '0' 和 '1' 组成的字符串 S，我们可以将任何 '0' 翻转为 '1' 或者将 '1' 翻转为 '0'。

返回使 S 单调递增的最小翻转次数。

## 题解1——动态规划 (PiggerZZM 2020-6-20)

用数学的语言来说，此题是在求01字符串S到"01单调递增字符串集合"的Hamming距离。

固定长度的01单调递增字符串可以用"01分割点"来唯一确定，比如长度为3的"01单调递增字符串集合"就是"111","011","001","000"，它们的"01分割点"的位置分别是0,1,2,3。(01分割点位置为i意思是在第i-1和第i个字符分割)

定义`dp[i]`为当01分割点位置为i时，字符串S的翻转次数。

如果`S[i-1] == 0`，算`dp[i-1]`时`S[i-1]`需要翻转，而算`dp[i]`时不需要翻转。如果`S[i-1] == 1`，算`dp[i-1]`时`S[i-1]`不需要翻转，而算`dp[i]`时需要翻转。由此可得状态转移方程为:

`dp[i] = dp[i-1] - 1` if `S[i-1] == '0'`
`dp[i] = dp[i-1] + 1` if `S[i-1] == '1'`

`dp[0]`为字符串S里`'0'`的个数。

这个dp数组同样也可以不需要一直维护，去掉dp数组后可以达到空间复杂度O(1)。

时间复杂度O(n)，空间复杂度O(1)。