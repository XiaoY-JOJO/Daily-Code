### 数组转换

将一个按照升序排列的有序数组，转换为一棵高度平衡二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1。

示例:

给定有序数组: [-10,-3,0,5,9],

一个可能的答案是：[0,-3,9,-10,null,5]，它可以表示下面这个高度平衡二叉搜索树：

      0
     / \
   -3   9
   /   /
 -10  5

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