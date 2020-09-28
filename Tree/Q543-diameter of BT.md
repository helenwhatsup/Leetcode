## Q543. Diameter of Binary Tree

Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

        Example:
        Given a binary tree
                  1
                 / \
                2   3
               / \     
              4   5    
        Return 3, which is the length of the path [4,2,1,3] or [5,2,1,3].

        class Solution {
            //思路： 求depth 1，必求depth2，depth3
            // 求depth2，  必须求depth4， depth5
            //depth2的深度： max左右+1
            // 4节点的深度为1 （左右儿子都是0）

            //用一个global sum都存一下当前节点的最大值，如果碰到不穿过root节点的时候，我们返回的是最大值（不一定包括跟节点）。 


            int sum=0;
            public int diameterOfBinaryTree(TreeNode root) {
                 helper(root);
                return sum;
            }
            public int helper(TreeNode root){

                if(root==null) return 0;

                    int l=helper(root.left);       
                    int r=helper(root.right);
                   //用一个global sum都存一下当前节点的最大值。
                sum=Math.max(sum,l+r);
                //4节点深度return的1，5节点深度return的1
                return Math.max(l,r)+1;

                //找出以 root 为根节点的二叉树的最大深度
                //递归return出来： 返回当前子树的最长深度
                // 该节点为根的子树的深度即为max(L,R)+1




            }
        }
