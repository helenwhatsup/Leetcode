# DFS 

## 1. DFS在二叉树
          void traverse(TreeNode root) {
              // 判断 base case
              if (root == null) {
                  return;
              }
              // 访问两个相邻结点：左子结点、右子结点
              traverse(root.left);
              traverse(root.right);
              }
* 第一个要素是访问相邻结点。二叉树的相邻结点非常简单，只有左子结点和右子结点两个。
二叉树本身就是一个递归定义的结构：一棵二叉树，它的左子树和右子树也是一棵二叉树。那么我们的 DFS 遍历只需要递归调用左子树和右子树即可。

* 第二个要素是 判断 base case。一般来说，二叉树遍历的 base case 是 root == null。
这样一个条件判断其实有两个含义：一方面，这表示 root 指向的子树为空，不需要再往下遍历了。
另一方面，在 root == null 的时候及时返回，可以让后面的 root.left 和 root.right 操作不会出现空指针异常。

## 网格DFS
所以，网格 DFS 的两个要素：
* 1. 首先，网格结构中的格子有多少相邻结点？答案是上下左右四个。对于格子 (r, c) 来说（r 和 c 分别代表行坐标和列坐标），
四个相邻的格子分别是 (r-1, c)、(r+1, c)、(r, c-1)、(r, c+1)。换句话说，网格结构是「四叉」的。
* 2. 其次，网格 DFS 中的 base case 是什么？从二叉树的 base case 对应过来，应该是网格中不需要继续遍历、grid[r][c] 会出现数组下标越界异常的格子，也就是那些超出网格范围的格子。
* 3. 网格DFS的框架代码： 

          void dfs(int[][] grid, int r, int c) {
              // 判断 base case
              // 如果坐标 (r, c) 超出了网格范围，直接返回
              if (!inArea(grid, r, c)) {
                  return;
              }
              // 访问上、下、左、右四个相邻结点
              dfs(grid, r - 1, c);
              dfs(grid, r + 1, c);
              dfs(grid, r, c - 1);
              dfs(grid, r, c + 1);
          }

          // 判断坐标 (r, c) 是否在网格中
          boolean inArea(int[][] grid, int r, int c) {
              return 0 <= r && r < grid.length 
                    && 0 <= c && c < grid[0].length;
          }
## 如何避免重复遍历
如何避免这样的重复遍历呢？答案是标记已经遍历过的格子。 代码如下： 

          void dfs(int[][] grid, int r, int c) {
              // 判断 base case
              if (!inArea(grid, r, c)) {
                  return;
              }
              // 如果这个格子不是岛屿，直接返回
              if (grid[r][c] != 1) {
                  return;
              }
              grid[r][c] = 2; // 将格子标记为「已遍历过」

              // 访问上、下、左、右四个相邻结点
              dfs(grid, r - 1, c);
              dfs(grid, r + 1, c);
              dfs(grid, r, c - 1);
              dfs(grid, r, c + 1);
          }

          // 判断坐标 (r, c) 是否在网格中
          boolean inArea(int[][] grid, int r, int c) {
              return 0 <= r && r < grid.length 
                    && 0 <= c && c < grid[0].length;
          }

            private void dfs(char[][] grid, int i, int j, boolean[][] used) {
                  if(i < 0 || j < 0 || i >= grid.length || j >= grid[0].length || grid[i][j] == '0' || used[i][j])
                      return;

                  used[i][j] = true;

                  dfs(grid, i+1, j, used);
                  dfs(grid, i, j+1, used);
                  dfs(grid, i-1, j, used);
                  dfs(grid, i, j-1, used);
              }

