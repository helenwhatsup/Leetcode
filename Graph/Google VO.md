338. Counting Bits (with negative number)

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
