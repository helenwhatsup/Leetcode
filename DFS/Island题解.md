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
