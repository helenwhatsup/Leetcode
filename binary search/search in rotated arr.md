## Q33. Search in Rotated Sorted Array
## 思路1

思路一：将 「旋转数组查找目标值」 转化成 「有序数组查找目标值」
方法一：最简单的做法, 先找index。 分成两段有序数组，接下来在有序数组中找目标值就轻车熟路了。
先找到 「153. 寻找旋转排序数组中的最小值」的索引，由此可以将数组分为升序的两段。
根据 nums[0] 与 target 的关系判断 target 在左段还是右段，再对升序数组进行二分查找即可。



## 思路2
* 1.确定中点mid。
* 2.比较nums【start】和nums【mid】，nums【mid】，nums【end】
* 3. 在区间  nums【start】<=  nums【mid】, 升序。 
       用这个区间比较target，看target是否在这个区间。如果是，end=mid-1
*  4. 在区间  nums【mid】<= nums【end】 升序。
     用这个区间比较target，看target是否在这个区间。如果是，start=mid+1

------------------------------------------------------------------

       public class Solution {
           public int search(int[] nums, int target) {
               int start = 0;
               int end = nums.length - 1;
               while (start <= end){
                   int mid = (start + end) / 2;
                   if (nums[mid] == target)
                       return mid;
                   if (nums[start] <= nums[mid]){
                        if (target < nums[mid] && target >= nums[start]) 
                           end = mid - 1;
                        else
                           start = mid + 1;
                   } 

                   if (nums[mid] <= nums[end]){
                       if (target > nums[mid] && target <= nums[end])
                           start = mid + 1;
                        else
                           end = mid - 1;
                   }
               }
               return -1;
           }
       }
