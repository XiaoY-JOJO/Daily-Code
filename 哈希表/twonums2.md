### 两数之和

![](/images/167.png)

#### 哈希表
```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        HashMap<Integer,Integer> map = new HashMap<>();
        int[] res = new int[2];
        for(int i=0; i<numbers.length; i++){
            int key = numbers[i];
            if(map.containsKey(target-key)){
                res[0] = map.get(target-key);
                res[1] = i+1;
            }
            map.put(key,i+1);
        }
        return res;
    }
}
```

#### 双指针
```java
class Solution{
    public int[] twoSum(int[] numbers, int target) {
        if (numbers == null) return null;
        int i = 0, j = numbers.length - 1;
        while (i < j) {
            int sum = numbers[i] + numbers[j];
            if (sum == target) {
                return new int[]{i + 1, j + 1};
            } else if (sum < target) {
                i++;
            } else {
                j--;
            }
        }
        throw new NullPointerException("null");
    }
}
```

哈希表运算出来的用时比双指针高了很多，但两者的时间复杂度都是O(n)
![](/images/res.png)
