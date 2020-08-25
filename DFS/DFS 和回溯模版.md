## DFS
** DFS和回溯算法区别
DFS是一个劲的往某一个方向搜索，而回溯算法建立在DFS基础之上的，但不同的是在搜索过程中，达到结束条件后，恢复状态，回溯上一层，再次搜索。因此回溯算法与DFS的区别就是有无状态重置~ 

** 用处，题型


LC题目： 39，40，46，47，78，90

类型	题目链接
子集、组合	子集、子集 II、组合、组合总和、组合总和 II
全排列	全排列、全排列 II、字符串的全排列、字母大小写全排列
搜索	解数独、单词搜索、N皇后、分割回文串、二进制手表


**回溯算法关键在于:不合适就退回上一步 然后通过约束条件, 减少时间复杂度.
    
* 模版套路

              result = []
              def backtrack(路径, 选择列表):
                  if 满足结束条件:
                      result.add(路径)
                      return
                  for 选择 in 选择列表:
                      做选择
                      backtrack(路径, 选择列表)
                      撤销选择
                      

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
          lists.add(new ArrayList(list));
          for(int i = start; i < nums.length; i++){
            // 根据题目加入某判断条件！！
              list.add(nums[i]); 将整数 nums[i] 添加到当前子集 
              process(list, nums, i+1); 选择路径，继续向子集中添加整数：backtrack(i + 1, curr)。
              list.remove(list.size()-1); 从 curr 中删除 nums[i] 进行回溯。
          }
      }
