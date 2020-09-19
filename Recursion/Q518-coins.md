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
-----------------------------------------------------


          // DFS Time Limit Exceeded
          func changeBFS(amount int, coins []int) int {
              return coinCombination(coins, 0, amount)
          }
          // 辅助递归函数,coins:面值数组,sum:目标值,start:每次从第几个面值开始拿起,避免拿以前的面值而出现重复组合
          func coinCombination(coins []int, start, sum int) int {
              if sum == 0 { // 递归终止条件
                  return 1 // 找到一个组合返回1
              }
              if sum < 0 { // 递归终止条件
                  return 0 // 当前组合无效返回0
              }
              result := 0                           // 初始化组合数量为0
              for i := start; i < len(coins); i++ { // 从下标start开始遍历面值数组
                  result += coinCombination(coins, i, sum-coins[i])
              } // 下一轮是从第i个面值开始拿，并且总值为sum-coins[i]
              return result
          }。
