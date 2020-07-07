## 最长有效括号


![](https://github.com/XiaoY-JOJO/ImageRepository/blob/master/32.png)

### 1.动态规划
```
public class Solution {
    public int longestValidParentheses(String s) {
        int maxans = 0;
        int dp[] = new int[s.length()];
        for (int i = 1; i < s.length(); i++) {
            if (s.charAt(i) == ')') {
                if (s.charAt(i - 1) == '(') {
                    dp[i] = (i >= 2 ? dp[i - 2] : 0) + 2;
                } else if (i - dp[i - 1] > 0 && s.charAt(i - dp[i - 1] - 1) == '(') {
                    dp[i] = dp[i - 1] + ((i - dp[i - 1]) >= 2 ? dp[i - dp[i - 1] - 2] : 0) + 2;
                }
                maxans = Math.max(maxans, dp[i]);
            }
        }
        return maxans;
    }
}
```

### 2.利用栈
利用栈来存储括号在字符串中对应的下标
```
public class Solution {
    public int longestValidParentheses(String s) {
        Stack<Integer> stack = new Stack<Integer>();
        int max=0;
		//left用来存储上一个未被匹配的")"的下标
        int left = -1;
        for(int j=0;j<s.length();j++){

			//只要是"("，就将其下标push进栈
            if(s.charAt(j)=='(') stack.push(j);            
            else {
				//栈为空，则更新left
                if (stack.isEmpty()) left=j;
                else{
					//将对应的"("的下标pop出来
                    stack.pop();
                    if(stack.isEmpty()) max=Math.max(max,j-left);
					//此时stack.peek()返回的元素是未被匹配的右括号的下标
                    else max=Math.max(max,j-stack.peek());
                }
            }
        }
        return max;
    }
}
```
- 时间复杂度为o(n)，由字符串的长度决定
- 空间复杂度为o(n)，栈的大小最坏需要存储整个字符串