### 搜索插入位置

#### 二分查找

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        return binarysearch(0,nums.length-1,target,nums);
    }

    public int binarysearch(int left, int right,int target, int[] nums){
        int mid = left+(right-left)/2;

		//插入的值大于数组所有值的情况单独判断
        if(nums[nums.length-1] < target) return nums.length;
        while(left < right){
            if(nums[mid] == target) return mid;
            if(nums[mid] < target){
                return binarysearch(mid+1, right, target, nums);
            }
            if(nums[mid] > target){
                return binarysearch(left, mid, target, nums);
            }
            
        }
        return left;
         
    }
}
```
二分查找的重难点就是边界问题，一般分为两种情况：
- while(left<right)将区间划分为[left,mid]和[mid+1,right]
- while(left<=right)将区间划分为mid、[left,mid-1]和[mid+1,right]

最后返回left还是right就看题目要找的是刚好大于目标值的索引还是目标值