##Q236 . Lowest Common Ancestor of a Binary Tree

https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/


        class Solution {
            public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {

              //check p q是否在root两侧，如果是，那么root就是common ancestor
               //特殊情况 - root=p, root=q. 
                //pq都在左侧同侧，那么ancestor在左边
                //右侧同侧，在右边。


            // 1.终止条件： 当越过叶节点，则直接返回 null ；当 root 等于 p, q ，则直接返回 root；    
              // eg。 比如当右子tree为null，我们遍历左子树，如果左边有一个root是p或者q，那我直接return root。
                // 右子树同理。
                if(root==null){
                    return root;
                }      
                if(root==p || root == q){
                    return root;
                }
                //递推工作：
        //开启递归左子节点，返回值记为 left ；
        //开启递归右子节点，返回值记为 right；
            //如果 root 等于 p 或者 q ，那这棵树一定返回 p 或者 q 
              TreeNode left=lowestCommonAncestor(root.left,p,q);
                //递归的时候，root.left就变成root了，如果这个==p，那就return了
              TreeNode right=lowestCommonAncestor(root.right,p,q);
                if(left==null && right==null){
                    //都没找到。
                    return null;
                }
                if(left==null){
                    //都在右边
                    return right;
                }
                if(right==null){
                    //都在左边
                    return left;
                }
                // left right都不为空，说明一边一个，因此 root是他们的最近公共祖先

                return root;

            }
        }
