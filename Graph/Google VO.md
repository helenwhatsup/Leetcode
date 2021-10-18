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
         https://leetcode.com/problems/excel-sheet-column-title/


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

**DFS** ----------------------------------------------------------------------------------------------------------------------------------------
 1. Find the resolution of an unknown screen given getRGB(x, y). The resolution is defined as eg.(100 * 50), 其实就是一个screen的(rows * cols). 并且会提供给你一个辅助函数getRGB(x, y), if (x, y) is out of bound of the screen, it will return (-1, -1, -1), otherwise, return (R, G, B) values in each channel. 问题就是让你返回这个screen的(rows, cols). 
  
 
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
                  
                  
   2. 
input ： 1: New York 10000, 2: san fran 1000, 3: Texas 500, .... (一个index, 一个城市名，对应一个value, 总共n个城市)。
input2: {1, 2} ny <-> san fran, {1, 4} ny <-> LA, {5, 4} chicago <-> LA, ......(从一个地方到另一个地方的航班，有m 个航班)；

output：pick 4 distict cities to visit, 使得整趟旅程的的value最大，返回最大值。
eg: san fran -> ny -> LA -> Chicago = value, 找到最大的value。
  1000 + 10000 + xxxx + xxxxx               
  
