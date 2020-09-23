      ##Q322 CoinChange
      https://leetcode.com/problems/coin-change/
      
      
      class Solution {
          public int coinChange(int[] coins, int amount) {
      //凑成面值为 11 的最小***数可以由以下 33 者的最小值得到：
      // 1、凑成面值为 10 的最小数 + 面值为 1 的这一枚；
      // 2、凑成面值为 9 的最小数 + 面值为 2 的这一枚；
      // 3、凑成面值为 6 的最小数 + 面值为 5 的这一枚；

      // 即 dp[11] = min (dp[10] + 1, dp[9] + 1, dp[6] + 1)

              //dp[i][j] 前i种硬币来达到amount j 的min ways
              //dp[i][j]=min(dp[i][j],dp[i][j-coin]+1)
              //当前组合j-coin种情况再加1就是我们需要的dp[i][j]

          // memo[i]有两种实现的方式，
          // 一种是包含当前的coins[i],那么剩余钱就是 i-coins[i],这种操作要兑换的硬币数是 memo[i-coins[j]] + 1
          // 另一种就是不包含，要兑换的硬币数是memo[i]

      //如果当前硬币的值> amount,就是剩余钱是负数，不行
          // 外层 for 循环在遍历所有amount状态的所有取值
          // for (int i = 0; i < dp.size(); i++) {
          //     // 内层 for 循环在求所有选择的最小值
          //     for (int coin : coins) {

      //         dp[2]=1
      //         dp[3]=Math.min(dp[3],dp[3-coins[j]]+1)=2
      //         dp[4]=Math.min(dp[4],dp[4-coins[j]+1])=2=dp[2]+1
      //         dp[5]=Math.min(dp[5],dp[5-coins[j]]+1)=1


              int[]dp=new int[amount+1];
              Arrays.fill(dp,amount+1);
              dp[0]=0;
              //对于每个amount都要loop一次来找最小的值
              /// 1d的时候只能amount做dp[i]!!!

              for(int i=0;i<=amount;i++){
                  for(int coin:coins){
                      if(coin<=i){
                      dp[i]=Math.min(dp[i],1+dp[i-coin]);
                      }
                  }
              }

      return dp[amount]>amount ? -1 : dp[amount];



      }

    }
