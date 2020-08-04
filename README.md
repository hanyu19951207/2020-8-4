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

409. 最长回文串
    给定一个包含大写字母和小写字母的字符串，找到通过这些字母构造成的最长的回文串。
    在构造过程中，请注意区分大小写。比如 "Aa" 不能当做一个回文字符串。
    注意:
    假设字符串的长度不会超过 1010。
    示例 1:
    输入:
    "abccccdd"
    输出:
    7
    解释:
    我们可以构造的最长的回文串是"dccaccd", 它的长度是 7。
题解：
知识点：通过观察可知，在一个回文串中，只有最多一个字符出现了奇数次，其余的字符都出现偶数次。对于每个字符 ch，假设它出现了 v 次，我们可以使用该字符 v / 2 * 2 次，在回文串的左侧和右侧分别放置 
v / 2 个字符 ch。如果有任何一个字符 ch 的出现次数 v 为奇数（即 v % 2 == 1），那么可以将这个字符作为回文中心，注意只能最多有一个字符作为回文中心。
class Solution {
    public int longestPalindrome(String s) {
        int []count = new int[128];
        //count数组记录字符串中每个字符出现的次数
        for(char c : s.toCharArray()){
            count[c]++;
        }
        int ans = 0;
        for(int a : count){
            ans += a / 2 * 2;
            if(a % 2 == 1 && ans % 2 == 0){
                ans++;
            }
        }
        return ans;
    }
}
412. Fizz Buzz
    写一个程序，输出从 1 到 n 数字的字符串表示。
    1. 如果 n 是3的倍数，输出“Fizz”；
    2. 如果 n 是5的倍数，输出“Buzz”；
    3.如果 n 同时是3和5的倍数，输出 “FizzBuzz”。
题解：
//此题虽然简单，但是我在做题过程中出现了一些细节上的失误
class Solution {
    public List<String> fizzBuzz(int n) {
        List<String> ans = new ArrayList<>();
        for(int i = 1;i <= n;i++){
           //此处应该先判断是否为FizzBuzz,我在做的时候先判断了Fizz，导致本来应该是FizzBuzz结果判定成Fizz
             if(i % 3 == 0 && i % 5 == 0)  ans.add("FizzBuzz");
        else if(i % 5 == 0)  ans.add("Buzz");
        else if(i % 3 == 0)    ans.add("Fizz");
        else    ans.add(Integer.toString(i));    //此处int转化为String的方法
        }
        return ans;
    }
}
