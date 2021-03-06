# DFS
## DFS和回溯算法区别
DFS是一个劲的往某一个方向搜索，而回溯算法建立在DFS基础之上的，但不同的是在搜索过程中，达到结束条件后，恢复状态，回溯上一层，再次搜索。因此回溯算法与DFS的区别就是有无状态重置~ 

## 用处，题型
* DFS一般用在找ALL Possible Solution , 所有方案，排列or组合的题目上！！！

LC题目： 39，40(done)   46，47（全排列），78，90, Q131(partition Palindrome)

类型	题目       
子集、组合:	子集、子集 II、组合、组合总和、组合总和 II   
全排列: 	全排列、全排列 II、字符串的全排列、字母大小写全排列   
搜索: 	解数独、单词搜索、N皇后、分割回文串、二进制手表   


## 回溯算法关键在于:不合适就退回上一步 然后通过约束条件, 减少时间复杂度.
    
## 模版套路

              public void backtrack(路径，选择列表){
                    if(满足结束条件){
                        result.add(结果);
                    }
                    for(选择：选择列表){
                        做出选择;
                        backtrack(路径，选择列表);
                        撤销选择;
                    }
                }

----

       List<List<Integer>> lists = new ArrayList<>();
          public List<List<Integer>> subsets1(int[] nums) {
              if(nums == null || nums.length ==0){
                  return lists;
              }

          List<Integer> list = new ArrayList<>();
          process(list, nums, 0);
          return lists;

      }

      private void process(List<Integer>list, int[] nums, int start){
      递归终止条件：lists.add(new ArrayList(list));
          for(int i = start; i < nums.length; i++){
            // 根据题目加入某判断条件！！
              //eg. 去重： if (i > start && nums[i] == nums[i - 1]) continue; //去掉重复的
              list.add(nums[i]); 将整数 nums[i] 添加到当前子集 
              process(list, nums, i+1); 选择路径，继续向子集中添加整数：backtrack(i + 1, curr)。
              list.remove(list.size()-1); 从 curr 中删除 nums[i] 进行回溯。
          }
      }
---
# 题目：
## Q Permutation
[]-[1]-[12]-[123]
       -[13]-[132]
       
   -[2]-[21]-[213]
       -[23]-[231]
       
## Q Permutation II 去重：
* 思路：在一定会产生重复结果集的地方剪枝。     
如果已经被选择了，用过了，跳。 if(visited[i]==true){continue;}     
如果当前节点与他的前一个节点一样，并其他的前一个节点被撤销了选择（没有被选择）不行，continue。    
    

        public void dfs(List<List<Integer>> res, List<Integer> list,boolean[]visited, int[]nums){
            HashMap<Integer,Integer> map=new HashMap<>();
            //去重哈 思路：在一定会产生重复结果集的地方剪枝。
            if(list.size()==nums.length){
                res.add(new ArrayList<>(list));
            }
            for(int i=0;i<nums.length;i++){
                //被选择了，用过了，我们已经选择过的节点
                if(visited[i]==true){continue;} 
                //接下来，如果当前节点与他的前一个节点一样，并其他的前一个节点被撤销了选择（没有被选择）不行。
    
             if(i>0 && nums[i] == nums[i-1] && visited[i-1]==false) continue;
            list.add(nums[i]);
            visited[i]=true; //改过了 
            dfs(res,list,visited,nums);
            list.remove(list.size()-1);
            //改回来 
            visited[i]=false;
        }
        
        
    }
}

       

