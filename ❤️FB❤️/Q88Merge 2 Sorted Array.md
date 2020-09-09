## Q88. Merge 2 Sorted Array



### Sol1: BF Merge
* Time: O(nlogn)


        class Solution {
            public void merge(int[] nums1, int m, int[] nums2, int n) {
                for(int i=m;i<nums1.length;i++){
                    nums1[i]=nums2[i-m];
                }
                Arrays.sort(nums1);
            }
        }



### Sol2: 从后往前Two Pointers from the end: 
* 思路：
从 nums1 和 nums2 数组的末尾开始一个一个比较，把较大的数，按顺序从后往前加入混合之后的数组末尾。    
需要三个变量 i，j，k，分别指向 nums1，nums2，和混合数组的末尾。  
进行 while 循环，如果i和j都大于0，再看如果 nums1[i] > nums2[j]，说明要先把 nums1[i] 加入混合数组的末尾，加入后k和i都要自减1；反之就把 nums2[j] 加入混合数组的末尾，加入后k和j都要自减1。循环结束后，有可能i或者j还大于等于0，若j大于0，那么还需要继续循环，将 nums2 中的数字继续拷入 nums1。若是i大于等于0，那么就不用管，因为混合数组本身就放在 nums1 中

* Time: O(n+m) Space: O(1)


          class Solution {
              public void merge(int[] nums1, int m, int[] nums2, int n) {
                  int p1=m-1;
                  int p2=n-1;
                  int pos=n+m-1;
                  while((p1>=0) && (p2>=0)){
                      if(nums1[p1]<nums2[p2]){
                          nums1[pos--]=nums2[p2--];
                      }else{
                        nums1[pos--]=nums1[p1--];
                      }
                  }
                  //when nums1 1 is only[0],aka m=0, p1=-1. 
                  while(p2>=0){
                  nums1[pos--]=nums2[p2--];
                  }

              }
          }

### Sol3: 从前往后Two Pointers: 
* 需要make copy of array 1 cuz we want to return nums1. 
* 所以-- make copy，然后比较copy，然后放入nums1.
* Compare elements from nums1_copy and nums2  and add the smallest one into nums1.


        while ((p1 < m) && (p2 < n))
              nums1[p++] = (nums1_copy[p1] < nums2[p2]) ? nums1_copy[p1++] : nums2[p2++];
            // if there are still elements to add
            if (p1 < m)
              System.arraycopy(nums1_copy, p1, nums1, p1 + p2, m + n - p1 - p2);
            if (p2 < n)
              System.arraycopy(nums2, p2, nums1, p1 + p2, m + n - p1 - p2);


