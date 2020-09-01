## Q200 Number of Island Time:O(MN) Space:O(MN)

       public int numIslands(char[][] grid) {
              rows = grid.length;
              if (rows == 0) {
                  return 0;
              }
              cols = grid[0].length;
              this.grid = grid;
              used = new boolean[rows][cols];
              int count = 0;
              for (int i = 0; i < rows; i++) {
                  for (int j = 0; j < cols; j++) {
                      //1.  如果是岛屿中的一个点，并且没有被访问过
                      //2.  就进行深度优先遍历
                      if (!used[i][j] && grid[i][j] == '1') {
                          count++;
                         dfs(grid, i, j, used);
                      }
                  }
              }
              return count;
          }

          //在边界里，上下左右四个方向递归。 
           private void dfs(char[][] grid, int i, int j, boolean[][] used) {
              if(i < 0 || j < 0 || i >= grid.length || j >= grid[0].length || grid[i][j] == '0' || used[i][j])
                  return;

              used[i][j] = true;

              dfs(grid, i+1, j, used);
              dfs(grid, i, j+1, used);
              dfs(grid, i-1, j, used);
              dfs(grid, i, j-1, used);
          }

    
## Q695 Max Area of Island Time:O(MN) Space:O(MN)
每走到一个island，area+1

       public int maxAreaOfIsland(int[][] grid) {
                if (grid.length == 0 || grid[0].length == 0) {
               return 0;
           }
               int row=grid.length;
               int col=grid[0].length;

               int res=0;
               used = new boolean[row][col];
               for(int i=0;i<row;i++){
                   for(int j=0;j<col;j++){
                       if(grid[i][j]==1){
                          res = Math.max(res, dfs(grid,i, j));

                       }
                   }
               }
               return res;
           }
           private int dfs(int[][]grid,int i,int j){
       if(i < 0 || j < 0 || i >= grid.length || j >= grid[0].length || grid[i][j] == '0') return 0;

               if(grid[i][j]!=1){
                   return 0;
               }
               // set it to used island
               grid[i][j] = 0;

              // used[i][j]=true;

               return 1+dfs(grid, i - 1, j)
               + dfs(grid, i + 1, j)
               + dfs(grid, i, j - 1)
               + dfs(grid, i, j + 1);


           }


## Q463. Island Perimeter
思路：如果越界：边长+1；如果是水，边长+1 最后返回边长

       public int dfs(int[][]grid,int i,int j, boolean[][]used){
               // 如果越界：边长+1
           if (i < 0 || i >= grid.length || j < 0 || j >= grid[0].length) {return 1;}
               //  如果是水，边长+1 ：
               if(grid[i][j]==0){
                   return 1;
               } 

               if(grid[i][j]!=1){
                   return 0;
               }
               used[i][j]=true;
             //// 将方格标记为"已遍历"
               grid[i][j] = -1;

               return dfs(grid, i - 1, j,used)
               + dfs(grid, i + 1, j,used)
               + dfs(grid, i, j - 1,used)
               + dfs(grid, i, j + 1,used);


           }


## Q733 FloodFill Time：O（N）N：number of pixel

* 这道题和*“Surround Regin”*很像很像，也是对图的搜索标记相连区域，然后改变标记. 
* 首先,从sr，sc的位置开始，对图——一个二维矩阵进行DFS搜索，找到从给定位置出发所有和给的值相同的位置，标记为-1。(search every element connected to the starting pixel)
* 全部标记完成之后dfs会返回。
* DFS的返回条件是行列范围跳出，或值跟【sr】【sc】不相等，或已被标记。 所以我们就找到了所有值相等的路径。全部标记为-1.
* 之后再对图进行遍历，找到所有标记为-1的位置，改成newColor完成渲染。 

        public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
               int oldColor=image[sr][sc];
                 for(int i=0;i<image.length;i++){
                 for(int j=0;j<image[0].length;j++){
                     if(image[i][j]==oldColor){
                   //every element connected to the starting pixel  
                      DFS(image,sr,sc,oldColor,newColor);
                     }
                     if(image[i][j]==-1){
                         image[i][j]=newColor;
                     }
                 }
             }
               return image;

           }

           public void DFS(int[][] image, int x, int y, int oldColor, int newColor) {
               if (x < 0 || x >= image.length || y < 0 || y >= image[0].length || image[x][y] != oldColor) { // 越界 或 非渲染格
                   return;
               }
               image[x][y] = -1;     // 换色
               DFS(image, x - 1, y, oldColor, newColor);   // 上
               DFS(image, x + 1, y, oldColor, newColor);   // 下
               DFS(image, x, y - 1, oldColor, newColor);   // 左
               DFS(image, x, y + 1, oldColor, newColor);   // 右
           }


## Q130 Surrounded Regions
https://leetcode.com/problems/surrounded-regions/

* 思路： 如何寻找和边界联通的 O。 
* 为了记录这种状态，我们把这种情况下的 O 换成 # 作为占位符，待搜索结束之后，遇到 O 替换为 X（和边界不连通的 O）；
* 遇到 #，表示这个位置与边缘O联通，替换回 O(和边界连通的 O)。


       public void solve(char[][] board) {
           if(board==null || board.length==0){
               return;
           }  
           int m = board.length;
           int n = board[0].length;
               for (int i = 0; i < m; i++) {
                   for (int j = 0; j < n; j++) {
                       // 从边缘 o 开始搜索
                       boolean isEdge = i == 0 || j == 0 || i == m - 1 || j == n - 1;
                       if (isEdge && board[i][j] == 'O') {
                           dfs(board, i, j);
                       }
                   }
               }

               for(int k=0;k<board.length;k++){
                   for(int p=0;p<board[0].length;p++){
                       if(board[k][p]=='O'){
                           board[k][p]='X';
                       }
                       if(board[k][p]=='#'){
                          board[k][p]='O';
                       }

                   }
        }
        
    }

       // funciton dfs里，#只是标记了所有与边界联通的O，所以我们用#来做占位符，最后在替换回去。

         public void dfs(char[][] board, int i, int j) {
               if (i < 0 || j < 0 || i >= board.length  || j >= board[0].length || board[i][j] == 'X' || board[i][j] == '#') {
                   // board[i][j] == '#' 说明已经搜索过了. 
                   return;
               }
               board[i][j] = '#';
               dfs(board, i - 1, j); // 上
               dfs(board, i + 1, j); // 下
               dfs(board, i, j - 1); // 左
               dfs(board, i, j + 1); // 右
           }


