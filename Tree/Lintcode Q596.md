  $$ Q596 Minimum Subtree 给一棵二叉树, 找到和为最小的子树, 返回其根节点。输入输出数据范围都在int内
   
   思路：   
  Divide and merge + recursion. 创建两个全局变量，一个记录当前sum，另一个记录当前node。我们要返回的是当前node with minimal value。
  在-5 node的时候我们的sum是-2， node为5. min更新为-2. 在2 node的时候我们的sum是-7， -7<-2, 小的就要更新。更新为min为-7，更新最小node为2. 
  然后最后来到1.1左边sum是 -2，右边sum是-7.  全局val为-8. -8小于min现在存储的值-7. 更新min为-8. node为1. 
  在main method 里call helper。return curnode。
  
  这棵树如下所示：  
     1
   /   \
 -5     2
 / \   /  \
1   2 -4  -5 

整颗树的和是最小的，所以返回根节点1.  

    
    
    
              
          public class Solution {
             /**
           * @param root: the root of binary tree
           * @return: the root of the minimum subtree
           */
           private int min=Integer.MAX_VALUE;
           private TreeNode curnode=null;
          public TreeNode findSubtree(TreeNode root) {
              // write your code here
           sum(root);
           return curnode;

          }
          //helper function 来算sum
          //在-5这个节点上 max=-2，node= -5.

          private int sum(TreeNode root){
              int res=0;
              if(root==null){
                  return 0;
              }
              if(root.left==null&&root.right==null){
                   res=root.val;
              }
              int left=sum(root.left);
              int right=sum(root.right);
              res=left+right+root.val;
              //只有得出的value < min的时候才会更新res 和node。不然不更新。 
              if(res<min){
                  min=res;
                  curnode=root;
              }
              return res;
          }
      }
