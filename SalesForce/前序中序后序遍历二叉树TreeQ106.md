### Q106 Construct Binary Tree from Inorder and Postorder Traversal        

https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/solution/kan-wo-jiu-gou-liao-san-chong-bian-li-fang-shi-g-2/
          

          
          public class Solution {
              int[] inorder;
              int[] postorder;
              int postIndex;    // 在 postorder 中的 index
              HashMap<Integer, Integer> inOrderIndex = new HashMap<>();

              public TreeNode buildTree(int[] inorder, int[] postorder) {
                  this.inorder = inorder;
                  this.postorder = postorder;
                  for (int i = 0; i < inorder.length; i++) {
                      inOrderIndex.put(inorder[i], i);
                  }
                  postIndex = postorder.length - 1;
                  return buildTreeHelper(0, postorder.length - 1);
              }

              private TreeNode buildTreeHelper(int left, int right) {     // left, right：在 inorder 中的 index
                  if (left > right) {
                      return null;
                  }
                  int rootVal = postorder[postIndex--];
                  TreeNode root = new TreeNode(rootVal);
                  int i = inOrderIndex.get(rootVal);
                  // 因为采用了 postIndex 每次减一的方法，所以必须先递归生成右子树再递归生成做子树！！！
                  root.right = buildTreeHelper(i + 1, right);
                  root.left = buildTreeHelper(left, i - 1);
                  return root;
              }
          }
