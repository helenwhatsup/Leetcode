  ## 迷宫模版
  *  This function solves the Maze problem using  
          Backtracking. It mainly uses solveMazeUtil()  
          to solve the problem. It returns false if no  
          path is possible, otherwise return true and  
          prints the path in the form of 1s. Please note  
          that there may be more than one solutions, this  
          function prints one of the feasible solutions.*/
          boolean solveMaze(int maze[][]).
     
     
    	 public class RatMaze { 
          // Size of the maze 
          static int N; 

          boolean isSafe( 
              int maze[][], int x, int y) 
          { 
              // if (x, y outside maze) return false 
              return (x >= 0 && x < N && y >= 0
                      && y < N && maze[x][y] == 1); 
          } 

          
          { 
              int sol[][] = new int[N][N]; 

              if (solveMazeUtil(maze, 0, 0, sol) == false) { 
                  System.out.print("Solution doesn't exist"); 
                  return false; 
              } 

              printSolution(sol); 
              return true; 
          } 

          /* A recursive utility function to solve Maze  
          problem */
          boolean solveMazeUtil(int maze[][], int x, int y, 
                                int sol[][]) 
          { 
              // if (x, y is goal) return true 
              // 在这里这种case： GOAL是 右下角的  1  
              if (x == N - 1 && y == N - 1
                  && maze[x][y] == 1) { 
                  sol[x][y] = 1; 
                  return true; 
              } 

              // Check if maze[x][y] is valid 
              if (isSafe(maze, x, y) == true) { 
                  // mark x, y as part of solution path 
                  sol[x][y] = 1; 

                
                  if (solveMazeUtil(maze, x + 1, y, sol)) 
                      return true; 
                  if (solveMazeUtil(maze, x, y + 1, sol)) 
                      return true; 

                  /* If none of the above movements works then  
                  BACKTRACK: unmark x, y as part of solution  
                  path */
                  sol[x][y] = 0; 
                  return false; 
              } 

              return false; 
          } 

         

-----

## 吃奶酪
    public static boolean solveMaze(int maze[][]) { 
        int n=maze.length;
        return dfs(maze,0,0);

      } 
    public static boolean dfs(int[][]maze,int i,int j){
        // 如果碰到0了， return false
      if(i<0 || j<0 || i>=maze.length || j>=maze.length || maze[i][j]==0)
			return false;
         // end condition
        if(maze[i][j]==9){
            return true;
        }
        //标记 走过了，就沉岛思想，沉下去
        maze[i][j]=0;
        boolean a1,a2,a3,a4;
        a1=dfs(maze,i+1,j);
        a2= dfs(maze,i-1,j);
        a3= dfs(maze,i,j+1);
        a4= dfs(maze,i,j-1);
        //backtrack
        maze[i][j]=1;
        //如果有一条路通了，就return这个
        
        return a1|| a2|| a3|| a4;
        
    }
    
