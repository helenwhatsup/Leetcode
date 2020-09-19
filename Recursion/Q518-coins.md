## Q518. Coin Change 2 递归做+Memo
https://leetcode.com/problems/coin-change-2/

* for each coin (for each index 'idx') we can memorize the amount of money we have processed and the number of possible changes we can get starting from this coin (this index 'idx') for that amount of money. 
     


     class Solution {
          public int change(int amount, int[] coins) {
              return helper(0,coins,amount);   
          }

      public static int helper(int index,int[]coins,int sum){
          //base conditon
          int res=0;
          if(sum==0){
            return 1;
          }
          else if(sum<0){
            return 0;
          }

          else{ //for loop是后面每个数字都有单独的path add up to 5
              for(int i=index;i<coins.length;i++){
                  res+=helper(i,coins,sum-coins[i]);   
              }
          }
               return res;                 

      }
