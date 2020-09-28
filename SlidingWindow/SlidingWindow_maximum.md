
## Q239. Sliding Window Maximum
* 如果queue最后一个元素小于当前nums【i】，那么不断pollLast直到queue中没有比nums【i】小的元素。加入nums【i】。
* 如果queue第一个元素（存的index）小于=i-k，要把它去掉。因为我们的sliding window size==k. 

//使用双端队列首先要搞懂一个问题，就是在双端队列中，要始终保证队头是队列中最大的值。那怎么保证呢，就是在添加一个值之前，比他小的都要被移除掉，然后再添加这个值。

//算法非常直截了当：
// 处理前 k 个元素，初始化双向队列。
// 遍历整个数组。在每一步 :

// 清理双向队列 :
//   - 只保留当前滑动窗口中有的元素的索引。
//   - 移除比当前元素小的所有元素，它们不可能是最大的。
// 将当前元素添加到双向队列中。 新的window
// 将 deque[0] 添加到输出中。
// 返回输出数组。


    class Solution {
        public int[] maxSlidingWindow(int[] nums, int k) {
            int n=nums.length;       
      ArrayDeque<Integer> queue = new ArrayDeque<Integer>();

            int[]result=new int[n-k+1];
            for(int i=0;i<nums.length;i++){  

             // 保证从大到小 如果前面数小则需要依次弹出，直至满足要求

                 //如果nums[i]大于peeklast，全部弹出比他小的
                 while(!queue.isEmpty() && nums[queue.peekLast()] <= nums[i]){
                    queue.pollLast();
                }

                //如果nums[i]小于peeklast，直接加入

                queue.addLast(i);

                 // 判断当前队列中队首的值是否有效
                if(queue.peek() <= i-k){
                    queue.pollFirst();   
                } 
                 if(i+1 >= k){
                    result[i+1-k] = nums[queue.peekFirst()];
                }
            }
            return result;

        }
    }
