# 2020-8-4
404. 左叶子之和
    计算给定二叉树的所有左叶子之和。
    示例：
          3
         / \
        9  20
          /  \
         15   7
     在这个二叉树中，有两个左叶子，分别是 9 和 15，所以返回 24
     
题解：
本题使用递归的先序遍历
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int sumOfLeftLeaves(TreeNode root) {
        return helper(root);
    }
    //创建helper函数用来递归运算
    public int helper(TreeNode node){
        int sum = 0;
        if(node == null)    //递归结束条件
            return 0;
        if(node.left != null && (node.left.left == null && node.left.right == null)){     //判断条件为此节点是否为左叶子节点
            sum += node.left.val;
        }
        sum += helper(node.left) + helper(node.right);  //递归遍历树
        return sum;
    }
}
