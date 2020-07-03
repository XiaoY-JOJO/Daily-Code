## 有序矩阵中第K小的元素

### 题意
给定一个 n x n 矩阵，其中每行和每列元素均按升序排序，找到矩阵中第 k 小的元素。
### 题解思路
#### 一、暴力排序
直接将整个矩阵的元素存入一个一维数组，然后调用Arrays的sort()，最后输出数组的第k个元素
```
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int m = matrix.length;        
        int n = matrix[0].length;
//题目假设k值永远有效，因此不用考虑矩阵为空的情况
        int[] res = new int[m*n];
        int a = 0;
        for(int i=0; i<m; i++){
            for(int j=0; j<n; j++){
                res[a++] = matrix[i][j];
            }
        }
        Arrays.sort(res);
        return res[k-1];
    }
}
```
对于Arrays.sort()的原理，网上众说纷纭，这里提供两篇博客参考[博文1](https://www.cnblogs.com/baichunyu/p/11935995.html)、[博文2](https://blog.csdn.net/zhupanlinch/article/details/104832542?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.nonecase)。


此思路的时间复杂度主要由排序算法构成，该矩阵一共有N^2^个元素，所以时间复杂度为O(N^2^logN)。

#### 二、二分查找
二分查找有两种搜索方式：一是按索引进行搜索，二是按值的范围进行搜索。
- 按索引进行搜索适用于有序数组，比如找出一个有序数组中的某个具体值，通过
常是对半缩小索引来进行查找
- 按值的范围进行搜索适用于无序数组，找到一个特殊值作为搜索基准，例如[No.287寻找重复数](https://leetcode-cn.com/problems/find-the-duplicate-number/)用的就是这个思路

```
public class Solution {
    public int kthSmallest(int[][] matrix, int k) {

        int left = matrix[0][0], right = matrix[matrix.length - 1][matrix[0].length - 1] + 1;
        while(left < right) {
            //将基准设为最大值和最小值的均值
            int mid = left + (right - left) / 2;

            //将搜索起点设置为矩阵最右上角的元素
            int count = 0,  j = matrix[0].length - 1;

            //逐行搜索，将每一行小于基准值的个数计入count累加
            for(int i = 0; i < matrix.length; i++) {
                //大于基准值则将列向左移动
                while(j >= 0 && matrix[i][j] > mid) j--;
                count += (j + 1);
            }

            //若从右上角到左下角搜索完毕后，count小于k，则说明第k个元素大于当前的基准值
            if(count < k) left = mid + 1;
            else right = mid;
        }
        //返回left或者right皆可
        return left;
    }
}
```

#### 三、堆排序
官方题解中还有用堆排序来对排序进行优化，堆排序作为单独的模块后续讲解。
