### 数组转换

![](https://github.com/XiaoY-JOJO/ImageRepository/blob/master/108.png)

```
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        TreeNode root = binaryTree(nums,0,nums.length-1);
        return root;
    }

    public TreeNode binaryTree(int[] nums, int left, int right){
        if(left>right) return null;
        int mid =  (right + left)/2;
        TreeNode root = new TreeNode(nums[mid]);
        root.left = binaryTree(nums, left, mid-1);
        root.right = binaryTree(nums, mid+1, right);
        return root;
    }
}
```
- 升序的有序数组恰好是二叉搜索树的中序遍历结果，因此只要利用二分的思路，每次都将中间节点作为子树的根节点，最后构建的二叉搜索树一定是高度平衡的。
- 注意：一个有序数组能构建的平衡二叉搜索树不唯一。