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


不同之处二 左右遍历范围
这一部分运用了一个技巧是 “两种遍历中，同一子树的节点数目是相同的”
需要说明的是在"前+后","前+中"我们都运用到了“右子树起始位置为左子树终止位置+1”，其实这个也可以运用上面这个技巧来计算出起始位置

前+后
后序遍历中，我们知道 左子树：[post_start,index], 右子树：[index+1, post_end-1]
在前序遍历中，左子树起始位置为pre_start+1,左子树个数一共有(index - post_start)个，因此左子树：[pre_start+1, pre_start+1 + (index - post_start)]
右子树起始位置为左子树终止位置+1，终止位置为pre_end，因此右子树：[ pre_start+1 + (index - post_start) + 1, pre_end]
前+中
中序遍历中，我们知道 左子树：[inorder_start,index-1], 右子树：[index+1, inorder_end]
在前序遍历中，左子树起始位置为pre_start+1,左子树一共有(index-1 - inorder_start)个，因此左子树：[pre_start+1, pre_start+1 + (index-1 - inorder_start)]
右子树起始位置为左子树终止位置+1，终止位置为pre_end，因此右子树：[ pre_start+1 + (index-1 - inorder_start) + 1, pre_end]
中+后
中序遍历中，我们知道 左子树：[inorder_start,index-1], 右子树：[index+1, inorder_end]
在后序遍历中，左子树起始位置为post_start，左子树一共有(index-1 - inorder_start)个，因此左子树：[post_start, post_start + (index-1 - inorder_start)]
右子树的终止位置为post_end - 1,右子树一共有(inorder_end - (index+1))个,因此右子树:[post_end - 1 - (inorder_end - (index+1)), post_end - 1]

