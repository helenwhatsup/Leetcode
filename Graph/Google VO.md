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


