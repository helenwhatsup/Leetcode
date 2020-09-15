
## 139. Word Break




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
