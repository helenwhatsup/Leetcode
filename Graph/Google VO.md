**BQ** 
如果有teammate take all credit怎么办？最难的project？怎么处理多个deadline？etc.


**Bits**  ----------------------------------------------------------------------------------------------------------------------------------------
338. Counting Bits (with negative number) 
把负数搞成正数： (x<<1)>>1  ，算正数bits+1=负数bits

         Using two's complement for negative numbers
             Find the positive binary value for the negative number you want to represent.
             Add a 0 to the front of the number, to indicate that it is positive.
             Invert or find the complement of each bit in the number.
             Add 1 to this number.

    

Method1:

         public int[] countBits(int n) {
              //  * P(x)=P(x/2)+(xmod2) *
              int[]dp=new int[n+1];
              for(int i=1;i<=n;i++){
                  dp[i]=dp[i/2]+(i%2);
              }
              return dp;

          }
Method2:

                  //if even,那么最后一位是0，可以num >> 1去掉最后一位
                  //If it is odd, the ending bit is 1, then the number of set bits is that of num - 1 + 1, i.e. countBits(num) = countBits(num - 1) + 1


                      int[] res = new int[n + 1];
                          for(int i=0;i<=n;i++){
                              if(i%2==0){
                                  res[i]=res[i>>1];
                              }else{
                                  res[i]=res[i-1]+1;
                              }
                          }
                          return res;
                          
                          
**String** ----------------------------------------------------------------------------------------------------------------------------------------
 1.  https://leetcode.com/problems/excel-sheet-column-title/


         class Solution {
             public String convertToTitle(int columnNumber) {
                StringBuilder sb=new StringBuilder();
                 // AB -> 28 = 26^1 +2
                 //  ABZ -> (A+1)26^2 + (B+1)26^2+ (Z+1)26^0 = n
                 // n/26=  (A+1)26^1 + (B+1)26^1 
                 // n%26 =   Z+1

                while(columnNumber>0){
                     sb.append((char)('A'+(columnNumber-1)%26));
                     columnNumber=(columnNumber-1)/26;
                 }
                 return sb.reverse().toString();

             }
         }

**Graph** ----------------------------------------------------------------------------------------------------------------------------------------

*1. Build Graph*
   
         for (List<String> account : accounts) {
            String userName = account.get(0);
            for (int i = 1; i < account.size(); i++) {
                if (!graph.containsKey(account.get(i))) {
                    graph.put(account.get(i), new HashSet<>());
                }
                name.put(account.get(i), userName);
                
                if (i == 1) continue;
                graph.get(account.get(i)).add(account.get(i - 1));
                graph.get(account.get(i - 1)).add(account.get(i));
            }
        }


**BFS** ----------------------------------------------------------------------------------------------------------------------------------------
模版
Shortest Path 
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
1. *LC1091. Shortest Path in Binary Matrix* https://leetcode.com/problems/shortest-path-in-binary-matrix/discuss/312706/JAVA-BFS

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


2. *LC690, https://leetcode.com/problems/employee-importance/
  
                    Queue<Employee>queue=new LinkedList<>();
                          queue.offer(map.get(id));

                          while(!queue.isEmpty()){
                              int size=queue.size();
                              for(int i=0;i<size;i++){
                                  Employee cur=queue.poll();
                                  sum+=cur.importance;
                                  for(int sub:cur.subordinates){
                                      queue.offer(map.get(sub));
                                  }

                              }
                          }


3. *Follow-up: 若開車從A到B，油箱一開始有V單位油，每走一個邊就用掉一單位，用完就不能再前進，在‍‌‌‍‍‍‍‌‍‌‌‌‍‌‍‌‌‍‍‌這之前有經過加油站的話可以把油加滿，一樣求最短路徑

                           Class Node{
                               //Int OilLeft// A以某个path走到当前点还剩的油量
                               //Int Distance // 这个path的距离
                           HashMap<OilLeft,Distance>map=new HashMap<>();
                                       map.put(OilLeft,Distance); // 如果oilLeft到这个点用了同样的oil，那么选短的path
                           }

                           Queue<Node>queue=new LinkedList<>();
                           queue.offer(A);

                           while(!queue.isEmpty()){
                                 Int size=queue.size();
                               for(int i=0;i<size;i++){
                                   Node cur=queue.poll();
                                       for(Node nei:cur){
                                           if(nei.isGasStation)  {
                                               Int updateddist=cur.get(1+nei.OilLeft); // is oil.left=V, 
                           nei.OilLeft()=V;
                           // 上一步的ValueSet 的minimum
                           map.put(nei.OilLeft, 上一步的ValueSet 的minimum)；
                           }

                                           Else:{
                                               for(int oilLeft:cur.map.keySet()){
                                                   nei.update(oilLeft-1, cur.get(oilLeft)+1);
                           // small就更新，如果不small直接放新的                

                           }

                                       visited.add(nei,OilLeft);
                                       queue.offer(nei);
                           }

                           }
                           }
                           Return min(B.valueSet())

4. *LC1293 

                           class Solution {
                               public int shortestPath(int[][] grid, int k) {
                                   //coordinates and the remaining quota.
                           // At each iteration of the loop, we pop out one element from the queue. The element contains the distance from the starting point as well as the current state which includes the current coordinate and the remaining quotas to eliminate obstacles.
                                   //到了一个点，有很多路线到一个点。 so that we can revisit the same cell with different quotas.
                           //一个grid--有一个state. A state refers to a unique combination of coordinates and the remaining quota.
                                   Queue<int[]>queue=new LinkedList<>();
                                   int m=grid.length;
                                   int n=grid[0].length;
                                   int[] dirs = {0, 1, 0, -1, 0};
                                   boolean[][][] visited = new boolean[m][n][k+1]; // keep track of state
                                   queue.offer(new int[]{0, 0, k, 0}); // row, col, k, distance
                                   visited[0][0][k] = true;


                                   while(!queue.isEmpty()){
                                       int[]cur=queue.poll();
                                       int x=cur[0];
                                       int y=cur[1];
                                       int quota=cur[2];
                                       int dist=cur[3];
                                       if(x==m-1 && y==n-1) return dist; // found result
                                      for(int i=0;i<4;i++){
                                          int nextx=x+dirs[i];
                                          int nexty=y+dirs[i+1];
                                          if(nextx<0 ||nexty<0 ||nextx>=m|| nexty>=n) continue;
                                          // out of bound,skip
                                           int newQuota=quota-grid[nextx][nexty];
                                          if(newQuota>=0 && !visited[nextx][nexty][newQuota]){
                                              queue.add(new int[]{nextx,nexty,newQuota,dist+1});
                                              visited[nextx][nexty][newQuota]=true;
                                          }
                                      }      
                                   }
                               return -1;


                               }
                           }

         
                                                   
**DFS** ----------------------------------------------------------------------------------------------------------------------------------------
 1.*  Find the resolution of an unknown screen given getRGB(x, y). The resolution is defined as eg.(100 * 50), 其实就是一个screen的(rows * cols). 并且会提供给你一个辅助函数getRGB(x, y), if (x, y) is out of bound of the screen, it will return (-1, -1, -1), otherwise, return (R, G, B) values in each channel. 问题就是让你返回这个screen的(rows, cols). 
  
 
                  pubic int[] findRes(Board board){
                           int[]res=new int[2];
                           Boolean visited[]=new Boolean[2];
                           dfs(0,0); 
                           for(tuple a:List){
                                    int maxX=Math.max(maxX,a.get(0));
                                    int maxY=Math.max(maxY,a.get(1));
                           }
                           return new int[]{maxY,maxY};

                  }
                  public void dfs(int x, int y,list<tuple[]>list){
                         // return condition, out of  bound or visited
                        if(visited.contains(x,y)) return;
                        if(getRGB(x, y)==(-1, -1, -1)) {
                           list.add(x,y);
                           return;
                        }
                        visited.add(x,y);
                        dfs(x-1,y,list);
                        dfs(x,y-1,list);
                        dfs(x+1,y,list);
                        dfs(x,y+1,list);

                  }
                  
                  
   2.  还没做，讨论！！
input ： 1: New York 10000, 2: san fran 1000, 3: Texas 500, .... (一个index, 一个城市名，对应一个value, 总共n个城市)。
input2: {1, 2} ny <-> san fran, {1, 4} ny <-> LA, {5, 4} chicago <-> LA, ......(从一个地方到另一个地方的航班，有m 个航班)；

output：pick 4 distict cities to visit, 使得整趟旅程的的value最大，返回最大值。
eg: san fran -> ny -> LA -> Chicago = value, 找到最大的value。
  1000 + 10000 + xxxx + xxxxx               
  
  * maximum spanning tree* 用‎Kruskal's algorithm。设置每个航线edge weight是链接的两个城市的value和。从最大的edge开始union。不需要找到maximum spanning tree, 只要有一个connection graph包含四个城市就可以停止了。 返回经过这四个城市的最大航线。主要排除掉有些城市value重复计算和4个城市不能用一条航线通过（三个城市经过同一个城市链接

          // adj list
          Queue<String>queue=new LinkedList<>();
          HashSet<String>visited=new HashSet<>();
          int step=0;
          int sum=0;
          int res=0;
          for (String key: HashMap.keySet()){  // for every city
               queue.offer(key);
               while(!queue.isEmpty()){
                  int size=queue.size();
                  for(int i=0;i<size;i++){
                           String currentCity=queue.poll();
                           sum+=currentCity.values;
                           res=Math.max(sum,res);
                           List<String>neigibors=adjList.get(currentCity);
                           for(String nei:neigibors){
                                queue.offer(nei);
                                visited.add(nei);
                           }
                  }
                  steps++;
                  if(steps==k) return res;

               }
                   
          }
         


3.
*394.* Decode String  https://leetcode.com/problems/decode-string/

                  class Solution {
                      public String decodeString(String s) {
                          Queue<Character> q = new LinkedList();
                          for(Character c:s.toCharArray()){
                              q.offer(c);
                          }
                          return dfs(q);

                      }

                      public String dfs(Queue<Character> q){
                          int num=0;
                          StringBuilder sb=new StringBuilder();
                         while(!q.isEmpty()){
                             Character c=q.poll();
                             if(Character.isDigit(c)){
                                 num=num*10+c-'0';
                             }
                             // not digit
                             else if(c=='['){
                                 String sub=dfs(q);
                                 for(int i=0;i<num;i++){
                                     sb.append(sub);
                                 }
                                 num=0;
                             }
                            else if(c==']'){
                                 break;
                             }
                             else sb.append(c);// append not digit 
                         }
                          return sb.toString();
                      }

                  }
4.   Longest Increasing Path  https://leetcode.com/problems/longest-increasing-path-in-a-matrix/



                       int visited[][]=new int[m][n];
                          for (int i = 0; i < m; i++) {
                              for(int j=0;j<n;j++){
                                  res=Math.max(res,dfs(matrix,i,j,visited));
                              }
                          }
                          return res;
                      }
                      public int dfs(int[][]matrix,int i,int j, int[][]visited){
                          // base case

                          if(visited[i][j]>0){
                              return visited[i][j];
                          }
                          int cur=matrix[i][j];
                          int max=1;
                                   四个方向
                          if (i-1 >= 0 && matrix[i][j] < matrix[i-1][j]) {//如上面可以走，就是当前路径+1
                              max = Math.max(max, dfs(matrix, i-1, j, visited)+1);
                          }
                         
                          visited[i][j]=max;
                          return max;
                      }

    
**DP** -------------------------------------------------------------------------------------------------------------------------------------------
LC 1048  https://leetcode.com/problems/longest-string-chain/
       
       
                          Arrays.sort(words,(a,b)->a.length()-b.length());
                          int maxLen=0;
                         int[]dp=new int[words.length];
                          for(int i=0;i<words.length;i++){ 
                              dp[i]=1;
                              //判断是否当前word是前面的所有string 的 predecessor
                              for(int j=i-1;j>=0 && words[i].length() - words[j].length() <= 1;j--){
                                  if(isPredecessor2(words[j],words[i])){
                                      dp[i] = Math.max(dp[i], dp[j] + 1);
                                  }
                              }
                               maxLen=Math.max(maxLen,dp[i]);
                          }
                          return maxLen;

                      }
    
 LC 1277 https://leetcode.com/problems/count-square-submatrices-with-all-ones/   
 
 
                              for(int i=0;i<m;i++){
                                       for(int j=0;j<n;j++){
                                           if(matrix[i][j]==1){
                                               if(i>0 && j>0){ 
                                                dp[i][j]=1+Math.min(Math.min(dp[i-1][j],dp[i-1][j-1]), dp[i][j-1]);
                                               }
                                                else if(i==0 || j==0){  // 1st col 1st row
                                                   dp[i][j] = 1; 
                                               }
                                           }

                                       }
                                   }

    
  300. Longest Increasing Subsequence  https://leetcode.com/problems/longest-increasing-subsequence/



                                    class Solution {
                                        public int lengthOfLIS(int[] nums) {
                                            int n=nums.length;
                                            int[]dp=new int[n];
                                            Arrays.fill(dp,1);


                                            for(int i=0;i<nums.length;i++){
                                                 // for every num we seem, check back for previous ones
                                                for(int j=0;j<i;j++){
                                                    if(nums[j]<nums[i]){
                                                       dp[i]=Math.max(dp[j]+1, dp[i]);

                                                    }
                                                }

                                            }
                                            int finalres=0;
                                            for(int i=0;i<dp.length;i++){
                                                finalres=Math.max(dp[i],finalres);
                                            }
                                            // iterate and find max of dp[i]
                                            return finalres;

                                                          }
                                                      }

 
1027*https://leetcode.com/problems/longest-arithmetic-subsequence/ 


                  class Solution {
                      public int longestArithSeqLength(int[] nums) {
                        //  [9,4,7,2,10]
                      //    [0,0,1,0,2] 这题和LIS的区别是对于index，我们加了一个difference
                  //dp[index][diff] equals to the length of arithmetic sequence at index with difference diff.


                 
                  // For each pair of indices (i,j) and difference d = A[i]-A[j] considered, we check if there was an existing chain at the index j with difference d already.
    If yes, we can then extend the existing chain length by 1.
                  //     Else, if not, then we can start a new chain of length 2 with this new difference d and (A[j], A[i]) as its elements.



                          int n=nums.length;   
                         HashMap<Integer, Integer>[] dp = new HashMap[n];
                          // 0 -diff-occurance   1-diff-occurance      2-diff-occurance 
                          // [hashmap1, hashmap2,hashmap3]

                      int res=0;
                          for(int i=0;i<n;i++){
                               dp[i] = new HashMap<>();
                              for(int j=0;j<i;j++){
                                  int difference=nums[i]-nums[j];
                                  dp[i].put(difference,dp[j].getOrDefault(difference,1)+1);
                                  res=Math.max(res,dp[i].get(difference));
                              }
                          }
                          return res;
                      }
                  }
  
**Stack** -------------------------------------------------------------------------------------------------------------------------------------------
  LC735 https://leetcode.com/problems/asteroid-collision/
  
       for(int a:asteroids){
                     if(a>0) stack.push(a);
                     else{ // negative 
                         while(!stack.isEmpty() && stack.peek()>0 && stack.peek()<Math.abs(a)){
                             stack.pop();
                         }// 如果stakc的top小，说明能撞，撞出去了，pop

                         if(stack.isEmpty()|| stack.peek()<0) stack.push(a);// 反方向或空
                         else if(a+stack.peek()==0) stack.pop();
                         // 如果stack里面的大，就不pull出来，也不把a放进去因为撞不了。

                     }
                 }
                 
 ***Tree:***------------------------------------------------------------------------------------------------------------------------------------------
 366. Find Leaves of Binary Tree https://leetcode.com/problems/find-leaves-of-binary-tree/

1110 https://leetcode.com/problems/delete-nodes-and-return-forest/

 */
                                    class Solution {
                                    ///如果一个node，他的parent被删了，且自己不再todelet list里，说明我们可以加他.

                                        HashSet<Integer>deleteList;
                                        List<TreeNode>list=new ArrayList<>();
                                        public List<TreeNode> delNodes(TreeNode root, int[] to_delete) {
                                            deleteList=new HashSet<>();
                                            for(int i:to_delete){
                                                deleteList.add(i);
                                            }
                                            dfs(root,true);

                                            return list;
                                        }
                                        public TreeNode dfs(TreeNode root, boolean isRoot){
                                            // isroot 说明没有parent，说明要么没有parent， 要么parent被删了自己没被删
                                            if(root==null) return null;
                                            boolean isDeleted=deleteList.contains(root.val);

                                            if(!isDeleted && isRoot){
                                                list.add(root);
                                            }
                                           root.left= dfs(root.left,isDeleted); //如果parent是deleted，说明下面的就是root。。 isDeleted 是parent的state
                                        root.right= dfs(root.right,isDeleted);
                                            if(isDeleted) return null;
                                            else return root;

                                        }
                                    }



 ***Topo Sorting***---------------------------------------------------------------------------------------------------------------------------------------
 
 269: https://leetcode.com/problems/alien-dictionary/
 207: https://leetcode.com/problems/course-schedule/
 
 
           for(int i=0;i<numCourses;i++){
                       map.put(i,new ArrayList<>());
                       degreeCount.put(i,0);
                  }

                 for(int[]pre:prerequisites){    
                     int beforeCourse=pre[1];
                     int afterCourse=pre[0];
                     map.get(beforeCourse).add(afterCourse);
                     degreeCount.put(afterCourse,degreeCount.get(afterCourse)+1);
                 }
                for(int i:degreeCount.keySet()){
                    if(degreeCount.get(i)==0){
                        q.offer(i);
                    }
                }

                 while(!q.isEmpty()){
                     int s=q.size();
                     for(int i=0;i<s;i++){
                         int curCourse=q.poll();
                         count++;
                         for(int adj:map.get(curCourse)){
                             degreeCount.put(adj,degreeCount.get(adj)-1);
                             if(degreeCount.get(adj)==0){
                                 q.offer(adj);
                             }
                         }

                     }

                 }
                 return count==numCourses;
             }
         }

