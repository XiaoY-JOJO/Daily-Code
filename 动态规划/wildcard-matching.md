### 通配符匹配

![](https://github.com/XiaoY-JOJO/ImageRepository/blob/master/44.png)

#### 1.动态规划
通过一个m*n的二维矩阵来存储状态，状态dp[i][j]存储的是字符串s的前i个字符和模式p的前j个字符是否能匹配。
一共分成三种情况讨论状态转移方程：
1. Si与Pj相同或者Pj是问号
2. Pj是星号
3. 其他情况


```
class Solution {
    public boolean isMatch(String s, String p) {
        int m = s.length();
        int n = p.length();
        boolean[][] dp = new boolean[m + 1][n + 1];
        dp[0][0] = true;
        for (int i = 1; i <= n; ++i) {
            if (p.charAt(i - 1) == '*') {
                dp[0][i] = true;
            } else {
                break;
            }
        }
        for (int i = 1; i <= m; ++i) {
            for (int j = 1; j <= n; ++j) {
                if (p.charAt(j - 1) == '*') {
				//Pj为*时，分成使用或不使用*两种情况，只要一种可以匹配即可
                    dp[i][j] = dp[i][j - 1] || dp[i - 1][j];
                } else if (p.charAt(j - 1) == '?' || s.charAt(i - 1) == p.charAt(j - 1)) {
				//Si与Pj相同或者Pj是问号
                    dp[i][j] = dp[i - 1][j - 1];
                }
				//其他情况默认为false
            }
        }
        return dp[m][n];
    }
}
```
- 时间复杂度：O(mn)
- 空间复杂度：O(mn)

#### 2.贪心算法+DFS

```
class Solution {
    public boolean isMatch(String str, String pattern) {

		//s为指向字符串的指针，p为指向模式的指针
		//match用来存储字符串中*匹配的子串后一个字符的位置
		//starIdx用来存储模式中最后一个*的位置
        int s = 0, p = 0, match = 0, starIdx = -1;  
		//e.g. s: a c d s c d  p: * c d
        //starIdx = 0; match = 1;即*只匹配第一个字符a，但是这是错误的分支
		//重置match = 2,依次尝试之后，match=4时为正确分支

        while (s < str.length()){
            // advancing both pointers
            if (p < pattern.length()  && (pattern.charAt(p) == '?' || str.charAt(s) == pattern.charAt(p))){
                s++;
                p++;
            }else if (p < pattern.length() && pattern.charAt(p) == '*'){
                starIdx = p;
                match = s;
                p++;
            }else if (starIdx != -1){
                p = starIdx + 1;
                match++;
                s = match;
            }else return false;
        }
        
        //check for remaining characters in pattern
        while (p < pattern.length() && pattern.charAt(p) == '*')
            p++;
        
        return p == pattern.length();
    }
}
```
- 时间复杂度：O(mn)
- 空间复杂度：O(1)