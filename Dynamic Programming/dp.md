## Q198 House Robber
思路：
* for house 0, we can only rob house 0. for house 1, we can rub just house 1 or just house 0, we take the max.    
At house i, we could rob it or not rub it
* if we rob house i (current house), we know that our previously robbed house would be i - 2 since we can not rob adjacient house
* if we do not rob house i (current house), we know that our previously robbed house would be i - 1 since the same  eason above      
* so the current accumulated sum at house i will be the max  of the two cases described above except if we rob, make sure we add the money in current house first before comparing
* so,if rob, the money will become: dp[i-2] + nums[i]. if not rob, the money will besome: dp[i-1]
 // dp[i]: robbed so far
