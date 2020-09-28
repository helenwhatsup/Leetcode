## Q257. Binary Tree Paths
Share
Given a binary tree, return all root-to-leaf paths.

Note: A leaf is a node with no children.
*思路： 前序遍历。根左右。如果满了就加入res。思路跟backtrack有点像。 过程:   左： " "   "1->" "1->2"   "1->2->5"  右： "1->" "1->3" （3是leaf）   res: "1->2->5" “1->3"


        Example:

              Input:

                 1
               /   \
              2     3
               \
                5

              Output: ["1->2->5", "1->3"]



        class Solution {
            public List<String> binaryTreePaths(TreeNode root) {
                // If node is not a leaf, one extends the current path by a node value and calls recursively the path construction for its children. 
                // end条件：If node is a leaf, one closes the current path and adds it into the list of paths.
                     List<String> res= new ArrayList<>();
                     String path="";
                     dfs(root,path,res);
                     return res;


            }
            //过程:
            //" "   "1->" "1->2"   "1->2->5"  res: "1->2->5" 
            public void dfs(TreeNode root,String path,List<String> res){
               if(root==null) return;
              //end条件是什么。终止条件是：加入leaf节点为一条完整的路。路完整了就要嫁到res中。
                if(root.left==null && root.right==null){
                    path+=root.val;
                    res.add(path);
                }else{
                    //not leaf
                path=path + root.val + "->";
                dfs(root.left, path, res);
                dfs(root.right, path, res);


                }




            }


        }
