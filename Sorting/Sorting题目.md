
## Find Kth element
* 1. 暴力 Arrays.sort O（nlogn）
* 2. QuickSelect: O(n)
* 3. Min heap: O(Nlogk) heap of size l




## Q215. Kth Largest Element in an Array

# 解法2 Quick Select:
* https://www.youtube.com/watch?v=cnzIChso3cc

            class Solution {
                public int findKthLargest(int[] nums, int k) {
                    int n=nums.length;
                    int left=0;
                    int right=n-1;
                    int target=n-k;

                    while (true) {
                        int index = partition(nums, left, right);
                        if (index == target) {
                            return nums[index];
                        } else if (index < target) {
                            left = index + 1;
                        } else {
                            right = index - 1;
                        }
                    }
                }
                public int partition(int[]nums,int left,int right){
                    int pivot=nums[left];
                    int j=left; //j 是要return的位置
                    for(int i=left+1;i<=right;i++){
                        if(nums[i]<pivot){
                            j++;
                            //放到pivot左边
                    //[left + 1, j] < pivot，并且 (j, i] >= pivot
                            swap(nums,j,i);
                        }
                    }
             // 交换以后放pivot。
            //  [left, j - 1] < pivot, nums[j] = pivot, [j + 1, right] >= pivot
                    swap(nums,j,left);
                    return j;
                }
                private void swap(int[] nums, int index1, int index2) {
                    int temp = nums[index1];
                    nums[index1] = nums[index2];
                    nums[index2] = temp;
                }
