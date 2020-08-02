## 除数博弈

![](/images/1025.png)

利用数学思维解题

```java
class Solution {
    public boolean divisorGame(int N) {
        if(N % 2 ==0){
            return true;
        }
        return false;
    }
}
```