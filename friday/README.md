给你一个房屋数组houses 和一个整数 k ，其中 houses[i] 是第 i 栋房子在一条街上的位置，现需要在这条街上安排 k 个邮筒。

请你返回每栋房子与离它最近的邮筒之间的距离的 最小 总和。

答案保证在 32 位有符号整数范围以内。

==================
动态规划。给定一个数组，如果安排一个邮局的话，那么将这个邮箱放到这个数组的中位数的位置上，所有的距离之和是最小的。(绝对值不等式)

当给了K个邮局的话，可以使用动态规划来求解。

按照最后一个邮箱的覆盖范围来划分。dp[i][j] 表示i个数，j个邮局，的最小划分方法。

那么枚举最后一个邮箱负责的范围，最大的范围是，前j - 1 个邮箱各自负责一个房子，那么最后一个就负责了j - 1到i的所有房子
最小的范围就是只负责第i个房子。

所以有dp[i][j] = min(dp[k - 1][j - 1] + rec[k][i], dp[i][j]) 对于k >= j - 1 && k <= i

rec[i][j] 表示从第i个房子到第j个房子，用一个邮箱最小的花费。可以提前预处理好所有的情况。

=================
```java
// time complexity O(n ^ 3 + n ^ 2 * k)
class Solution {
    public int minDistance(int[] houses, int k) {
        int n = houses.length;
        Arrays.sort(houses);
        // dp[i][j]表示前i个房子摆j个邮筒时的最短距离
        int[][] dp = new int[n + 1][k + 1];
        for (int i = 0; i <= n; i++) {
          Arrays.fill(dp[i], -1);
        }
        // dis[i][j] 表示范围[i,j]的房子共用一个邮筒时的最短距离
        int[][] dis = new int[n + 1][n + 1];
        for (int i = 1; i <= n; i++) {
          for (int j = i; j <= n; j++) {
            for (int x = i, y = j; x < y; x++, y--) {
              dis[i][j] += houses[y - 1] - houses[x - 1];
            }
          }
        }
        dp[0][0] = 0;
        // 求解DP，进行状态转移
        for (int i = 1; i <= n; i++) {
          for (int j = 1; j <= i && j <= k; j++) {
            for (int p = i; p >= 1; p--) {
              if (dp[p - 1][j - 1] != -1 && (dp[i][j] == -1 || dp[i][j] > dp[p - 1][j - 1] + dis[p][i])) {
                dp[i][j] = dp[p - 1][j - 1] + dis[p][i];
              }
            }
          }
        }
        return dp[n][k];
      }
}
```
