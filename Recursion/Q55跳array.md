	class Solution {
	// 当前的位置+jump的位置-- 再perform recursion 如果是true 那么现在的位置也是true
	
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
	for (int jump = 1; jump <= arr[cp]; jump++) {
					if(cp + jump < arr.length){
						/* here we use logical 'or' operator because any true
						 * result is sufficient enough to  prove that a jumps 
						 * combination exists with which we can reach end of
						 * given array*/
						rv = rv || solve(cp + jump, arr);
					}
				}





-----------------------------------------------------------------------------------------------------------------------------------------------------
				
		for (int jump = 1; jump <= arr[cp]; jump++) {
					if(cp + jump < arr.length){
						/* here we use logical 'or' operator because any true
						 * result is sufficient enough to  prove that a jumps 
						 * combination exists with which we can reach end of
						 * given array*/
						rv = rv || solve(cp + jump, arr);
					}
				}
				
				
---------------------------------------------------------------------------------------------------------------------------------------------------

					//根据nums[index]表示要循环多少次，index是当前我们能到达的位置，
					//在这个基础上有 index+1，index+2.... index+i种跳跃选择
					for(int jump=1;jump<=nums[index];++jump) {
					    if(dfs(jump+index,nums)) {
						return true;
					    }
					}
					return false;
					

---------------------------------------------------------------------------------------------------------------------------------------------------
		
		
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






