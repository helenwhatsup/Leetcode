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



### Sol2: Two Pointers from the end: 
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
