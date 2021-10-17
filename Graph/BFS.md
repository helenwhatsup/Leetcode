**BFS**
模版
1. Shortest Path 
从源点出发，BFS 首先遍历到第一层结点，到源点的距离为 1，然后遍历到第二层结点，到源点的距离为 2…… 可以看到，用 BFS 的话，距离源点更近的点会先被遍历到，这样就能找到到某个点的最短路径了。


                        level = 0
                        while queue is not empty：
                           int size = queue.size()
                           for(int i=0;i<size;i++)(
                                cur = queue.pop()
                                for node in cur 's neighbors ：
                                    if node is not visited ：
                                        queue.push(node)
                            }
                           distance/level ++; // 当前层都被遍历完毕，distance ++


-------------------------------------------------------------------------------------------------------------------------------------------------------
*LC1091*

       Queue<int[]>queue=new LinkedList<>();
              queue.offer(new int[]{0,0});
              int distance=1;
             int[][] dirs = new int[][]{{1, 0}, {-1, 0}, {0, 1}, {0, -1}, {1, 1}, {-1, 1}, {1, -1}, {-1, -1}};
              HashSet<String>visited=new HashSet<>();

              while(!queue.isEmpty()){
                    int size = queue.size();
                  for(int i=0;i<size;i++){
                      int[]cur=queue.poll();
                      int x=cur[0];
                      int y=cur[1];
                       if (x == rows - 1 && y == cols - 1) return distance;

                      for(int[]dir:dirs){  // for neighbors 
                          int nextX=x+dir[0];
                          int nextY=y+dir[1];
                          String key=nextX+""+nextY;
                          // if not visited and in boundry
                          if(nextX>=0 && nextX<rows&& nextY>=0 && nextY<cols){
                              if(grid[nextX][nextY]==0 && !visited.contains(key)){
                                  queue.offer(new int[]{nextX,nextY});
                                  visited.add(key);
                                  }
                              }
                      }
                  }
                   distance++;     
              }
