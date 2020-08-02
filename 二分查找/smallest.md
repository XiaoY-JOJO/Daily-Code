## 旋转数组的最小值

![](/images/routeint.png)

### 直接搜索
```java
class Solution {
    public int minArray(int[] numbers) {
        for(int i=0; i<numbers.length-1; i++){
            if(numbers[i]<=numbers[i+1]){
                continue;
            }
            return numbers[i+1];
        }
        return numbers[0];
    }
}
```

### 二分优化

```java
class Solution {
    public int minArray(int[] numbers) {
        int i = 0, j = numbers.length - 1;
        while (i < j) {
            int m = (i + j) / 2;
            if (numbers[m] > numbers[j]) i = m + 1;
            else if (numbers[m] < numbers[j]) j = m;
            else j--;
        }
        return numbers[i];
    }
}
```