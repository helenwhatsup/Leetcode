	class Solution {
	//
	    //方法1: Recursion+memo
	//      static HashMap<Integer,Boolean>memo= new HashMap<>();

	//     public boolean canJump(int[] nums) {
	//         return help(0,nums);

	//     }
	//     public boolean help(int index,int[]nums){
	//         if (index == nums.length-1) {
	// 			return true;
	// 		}

	//         if (nums[index] == 0) {
	// 			return false;
	// 		}
	// 		boolean res = false;

	// if(memo.containsKey(index)) {
	//             return cache.get(index);
	//         }


	// 		for (int jump = 1; jump <= nums[index]; jump++) {
	// 		
	// 				 // because any true result is sufficient enough to  prove that a jumps combination exists
	// 				  if(dfs(i+index,nums,cache)) {
		       // memo.put((i+index),Boolean.TRUE);
		       // return true;




	// 			}
	// 		}

	// cache.put(index,Boolean.FALSE);
	//         return false;

	// 		return res;


	    //方法2: Greedy 最远位置法
	public boolean canJump(int[] nums) {
	      int reach=0;
	    for(int i=0;i<nums.length;i++){
		// i表示position
		//不可到达
		if(i>reach) return false; 
		else{
		//可以到达
		reach=Math.max(reach,i+nums[i]);
		    //例子2: 我们遍历到位置 4，由于 4 > 3，因此位置 4 不可达，我们也就不考虑它可以跳跃的最大长度了，return false;
		}

	    }
	    return true;

		}



	    }






