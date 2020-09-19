  ## Q494. Target Sum
       
   Time complexity : O(2^n)
       
       class Solution {
            public int findTargetSumWays(int[] nums, int S) {
                return dfs(nums,S,0);
            }
            //传进来的参数
            public int dfs(int[]nums,int target,int index){
                int ans = 0;
                //base case
                if (target == 0 && index == nums.length) return 1;
                if (index >= nums.length) return 0;
                // 逻辑

                else{
               //choose path: 不可以重复，所以index+1

                    //没有for loop的原因是只需要从第一个开始递归，不需要每一个都重新开始递归。
                    //从第二个开始就没有一个单独的path add up to target了，所有的path都必须包含第一个。

                //for(int i=index;i<nums.length;i++){
                //必须包含第一个数字，所以必须从第一个算起。，没有for loop，不需要从第二个算起

                ans += dfs(nums, target - nums[index], index+1 );
                ans += dfs(nums, target + nums[index], index+1 );
                //}
                }
                //return value
                return ans;
            }
        }
