### 三角形最小路径和

![](/images/120.png)

#### 动态规划
```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int[] res = new int[triangle.size()+1];
        for(int i=triangle.size()-1; i>=0; i--){
            for(int j=0; j<=i; j++){
                res[j] = Math.min(res[j],res[j+1])+triangle.get(i).get(j);
            }
        }
        return res[0];
    }
}
```
利用滚动数组对空间进行优化，从三角形的底部往上进行迭代，对于res[]数组而言，最小值会不断往头部进行靠拢