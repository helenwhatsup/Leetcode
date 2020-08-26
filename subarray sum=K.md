# Sliding Window and Two Pointers
## subarray with length equals to K

* 1. HASHMAP
本题的主要思路：
计算出每个索引的前缀和，利用一个数组sum保存，利用一个max储存最长子数组长度；       

利用HashMap储存每个前缀和和对应的索引，如果出现前缀和相同的情况，则储存较小的索引（因为要求最长子数组）
；        
利用一个指针i作为子数组的结尾从后向前遍历，寻找map中是否储存有key为sum[i] - k的索引，如果有则更新max；

当指针的值小于等于max的值后，则无需再继续遍历；     

返回max则为最终结果。        

          class Solution {
              public int maxSubArrayLen(int[] nums, int k) {
                  HashMap<Integer, Integer> maps = new HashMap<>();
                  int ans = 0;
                  int cur = 0;
                  maps.put(0, -1);

                  for(int i=0; i<nums.length; i++){
                      cur += nums[i];
                      if(!maps.containsKey(cur)) maps.put(cur, i);
                      if(maps.containsKey(cur-k)){
                          ans = Math.max(ans, i - maps.get(cur-k));
                      }
                  }

                  return ans;
              }
          }
* 2. Two Pointers

                    public static int smallestSubarray(int[] A, int k)
                    {
                          // stores the current window sum
                        int windowSum = 0;
                      // stores the result
                      int len = Integer.MAX_VALUE;

                      // stores window's starting index
                      int left = 0;

                      // maintain a sliding window [left..right]
                      for (int right = 0; right < A.length; right++)
                      {
                        // include current element in the window
                        windowSum += A[right];

                        // window becomes unstable if its sum becomes more than k
                        while (windowSum > k && left <= right)
                        {
                          // update the result if current window's length is less
                          // than minimum found so far
                                                          left++;
                          len = Integer.min(len, right - left + 1);

                          // remove elements from the window's left side till window
                          // becomes stable again
                          windowSum -= A[left];

                        }
                      }

                      // return result
                      return len;
                    }

	
}
