### 跳水板

![](/images/0708.png)

#### 题解
```
class Solution {
    public int[] divingBoard(int shorter, int longer, int k) {
        if(k==0) return new int[0];
        if(shorter == longer) return new int[]{k*shorter};
        int[] res = new int[k+1];
        for(int i=0; i<k+1; i++){
            res[i] = shorter*(k-i) + longer*i;
        }
        return res;
    }
}
```
题目可能是目前做到最简单的一道，但是有几个细节要注意：
1. shorter = longer的情况要考虑进去;
2. k = 0的情况应该返回一个空的int数组;
3. 生成的数组大小应该为k+1才不会越界。