## Q200 Number of Island Time:O(M*N) Space:O(M*N)

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

    
