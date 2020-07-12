### 地下城游戏

![](/images/174.png)

#### 动态规划
思路是从右下角转移到左上角，dp存的是当前坐标到右下角最小初始值
```java
class Solution {
    public int calculateMinimumHP(int[][] dungeon) {
        int n = dungeon.length, m = dungeon[0].length;
        int[][] dp = new int[n + 1][m + 1];
        for (int i = 0; i <= n; ++i) {
			//将Integer.MAX_VALUE赋给数组dp[i]的每一个元素
            Arrays.fill(dp[i], Integer.MAX_VALUE);
        }
		
		//初始化为1，因为骑士最少需要一点生命值
        dp[n][m - 1] = dp[n - 1][m] = 1;

        for (int i = n - 1; i >= 0; --i) {
            for (int j = m - 1; j >= 0; --j) {
                int minn = Math.min(dp[i + 1][j], dp[i][j + 1]);
                dp[i][j] = Math.max(minn - dungeon[i][j], 1);
            }
        }
        return dp[0][0];
    }
}

```

