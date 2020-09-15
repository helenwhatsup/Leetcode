
## 139. Word Break


### BF: TLE

      class Solution {
          public boolean wordBreak(String s, List<String> wordDict) {
            //brute force
              int n=s.length();
              //HashSet<String> set= new HashSet<>(wordDict);

              return dfs(s,new HashSet(wordDict),0);

          }

    public boolean dfs(String s,HashSet<Integer> set,int start ){
        //推出条件
        if(start==s.length()){
            return true;
        }
        for(int end=start+1;end<=s.length();end++){
            String str=s.substring(start,end);
            if(set.contains(str)){
                // if we found one substring
                // call dfs on the remaining part of the string
               if(dfs(s,set,end)){
                   return true;
               } 
                
            }
        }
         return false;
    }
   
}



### DP+ 记忆回溯

            class Solution {
                //这里我们的记忆数组 memo[i] 定义为范围为 [i, n] 的子字符串是否可以拆分.
                // 如果可以拆分，则赋值为1，反之为0。
                // dp[j] = dp[i] && check(s[i+1, j]);
                // 第j的位置可以拆分= 第i的位置可以拆分+ 后半部分(s[i+1, j]） 可以拆分。
                //这等价于s[i+1, j]是否是wordDict中的元素
                //假如wordDict=["apple", "pen", "code"],s = "applepencode";
                    //dp[8] = dp[5] + check("pen")
                  //  翻译一下：前八位能否拆分取决于前五位能否拆分，加上五到八位是否属于字典
                   //memo represents if substring (0,i) is breakable.  
                   //DFS + 记忆化
              public boolean wordBreak(String s, List<String> wordDict) {
                    Boolean[] mem=new Boolean[s.length()];
                    return wordBreak(0,s,new HashSet<String>(wordDict),mem);   
                }
                private boolean wordBreak(int start, String s, Set<String> dict, Boolean[] mem){
                    int n=s.length();
                    if(start==n) return true;
                    if(mem[start]!=null) return mem[start];
                    for(int end=start;end<n;end++) {
                        if(dict.contains(s.substring(start,end+1))&&wordBreak(end+1,s,dict,mem)) 
                        {
                        //前半部分在数组里，后半部分可以break，就把start标注成true。
                        //如果最后一个也是true，那就是true。如果最后是false，就是false。在递归函数更新记忆数组 memo.
                             if(mem[start]=true) return true;
                        }
                    }
                    return mem[start]=false;
                }
                    }
