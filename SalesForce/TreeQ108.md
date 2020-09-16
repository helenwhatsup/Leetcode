##Q108. Convert Sorted Array to Binary Search Tree
https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/

          class Solution {
              public TreeNode sortedArrayToBST(int[] nums) {

                  return construct(0,nums.length-1,nums);

              }
              public TreeNode construct(int l,int r,int[] nums){
                  if(l>r){
                      return null;
                  }
                      int mid=l+(r-l)/2;
                      TreeNode root= new TreeNode(nums[mid]);
                       root.left=construct(l,mid-1,nums);
                       root.right=construct(mid+1,r,nums);
                      return root;

              }
          }
