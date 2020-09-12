## Q31 next permutation.md
### 解题思路
以[5,6,11,9,7,5,3,1]举例吧

1.首先从尾部查找，直到找到当前元素大于前一个元素为止，记录该位置；
对于[5,6,11,9,7,5,3,1]，即查找到11>6，此时位置索引为2；
2.从该位置到数组尾部的子序列中，找到一个比前一位置的大且最接近的数；
对于[5,6,11,9,7,5,3,1]，即在[11,9,7,5,3,1]找到7，7是比6大且最接近6的，从尾部开始遍历，遍历到大于6的索引即可；
3.将找到的数与前一位置的数交换；
对于[5,6,11,9,7,5,3,1]，交换后变为[5,7,11,9,6,5,3,1]；
4.将该位置到数组尾部的子序列进行升序排列，因为已经为降序，故首尾两两交换即可；
对于步骤3中的[5,7,11,9,6,5,3,1],交换后为[5,7,1,3,5,6,9,11]；


### 算法过程
* 标准的“下一个排列”算法可以描述为：

1. 从后往前找到第一个【相邻升序对】，即A[i]<A[i+1]。此时A[i+1,end)为降序。
2. 在区间[i+1,end)中，从后往前找到第一个大于A[i]的元素A[j]
3. 交换A[i]和A[j]，此时A[i+1,end)一定还是降序，因为A[j]是从右侧起第一个大于A[i]的值
4. 反转A[i+1,end)，变成升序



              class Solution {
                  public void nextPermutation(int[] nums) {
                      // Possible: next greater permutation.
                      // not possible: ascending order.
                  int n=nums.length;
                  int i=0;
                      for(i=n-2;i>=0;i--){
                  //1. 从后往前找到第一个【相邻升序对】，即A[i]<A[i+1]。此时A[i+1,end)为降序。
                      if(nums[i]<nums[i+1]){
                          break;
                      }
                      }
                      if(i==-1){
                      Arrays.sort(nums);
                      }else{
                  // 2.在区间[i+1,end)中，从后往前找到第一个大于A[i]的元素A[j]  
                          int j=0;
                        for(j=n-1;j>i;j--){
                            if(nums[j]>nums[i]){
                                //找到j了。交换A[i]和A[j]，此时A[i+1,end)一定还是降序，因为A[j]是从右侧起第一个大于A[i]的值
                                swap(nums,i,j);
                                Arrays.sort(nums, i + 1, nums.length);  ; // 反转[i+1,end)，变成升序
                                  break;
                            }              
                        }  

                      }    
                      }

                  public void swap(int[]nums,int i,int j){
                      int tmp=nums[i];
                      nums[i]=nums[j];
                      nums[j]=tmp;
                  }
              }

