# Sliding Window and Two Pointers
## subarray with length equals to K

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
