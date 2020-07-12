### 股票买卖

![](/images/309.png)

#### 动态规划
一共分成三种情况讨论不同的状态转移方程
```java

class Solution {
    public int maxProfit(int[] prices) {
        if (prices.length == 0) {
            return 0;
        }

        int n = prices.length;
        // f[i][0]: 手上持有股票的最大收益
        // f[i][1]: 手上不持有股票，并且处于冷冻期中的累计最大收益
        // f[i][2]: 手上不持有股票，并且不在冷冻期中的累计最大收益
        int[][] f = new int[n][3];
        f[0][0] = -prices[0];
        for (int i = 1; i < n; ++i) {
			//手上持有股票的状态，说明昨天只能处于冷冻期或者昨天持有股票未售出
            f[i][0] = Math.max(f[i - 1][0], f[i - 1][2] - prices[i]);
、			//昨天只能处于持有股票的状态，然后今天售出后处于冷冻期
            f[i][1] = f[i - 1][0] + prices[i];
			//昨天处于冷冻期，或非冷冻期
            f[i][2] = Math.max(f[i - 1][1], f[i - 1][2]);
        }
		//持有股票时一定不是最大收益，因此不用考虑
        return Math.max(f[n - 1][1], f[n - 1][2]);
    }
}
```
- 时间复杂度：O(n)
- 空间复杂度：O(n)

#### 滚动数组
```java
class Solution {
    public int maxProfit(int[] prices) {
        int sell = 0, prev_sell = 0, buy = Integer.MIN_VALUE, prev_buy;
        for (int price : prices) {
            prev_buy = buy;
            buy = Math.max(prev_sell - price, prev_buy);
            prev_sell = sell;
            sell = Math.max(prev_buy + price, prev_sell);
        }
        return sell;
    }
}
```
- 时间复杂度：O(n)
- 空间复杂度：O(1)
