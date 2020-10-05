## Q33. Search in Rotated Sorted Array

* 1.确定中点mid。
* 2.比较nums【start】和nums【mid】，nums【mid】，nums【end】
* 3. 在区间  nums【start】<=  nums【mid】, 升序。 
       用这个区间比较target，看target是否在这个区间。如果是，end=mid-1
*  4. 在区间  nums【mid】<= nums【end】 升序。
     用这个区间比较target，看target是否在这个区间。如果是，start=mid+1


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
