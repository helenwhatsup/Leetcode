## Q22. Generate Parentheses
https://leetcode-cn.com/problems/generate-parentheses/solution/hui-su-suan-fa-by-liweiwei1419/


      class Solution {
          public List<String> generateParenthesis(int n) {
              //generate all combinations of well-formed parentheses.     
              // do some backtrack

              List<String> list = new ArrayList();
              backtrack(list, "",n, 0, 0);
              return list;
          }
          //做加法。即 left 表示“左括号还有几个没有用掉”，right 表示“右括号还有几个没有用掉”，可以画出另一棵递归树。

          public void backtrack(List<String>list,String cur, int len,int open,int close){
              //start总是"("
              // base case: 
              if (cur.length() == len * 2) {
                  list.add(cur);
                  return;
              }

            // recursion开始： 加括号

              //只有open< 3 的时候才可以加( 
              if(open<len){
                  backtrack(list,cur+'(',len,open+1,close);
              } 

              //只有close<open的时候才可以+ ) 
              if(close<open){
                  backtrack(list,cur+')',len,open,close+1);
              }
          }
      }

-------

        public List<String> generateParenthesis(int n) {
              List<String> ans = new ArrayList();
              backtrack(ans, new StringBuilder(), 0, 0, n);
              return ans;
          }
          public void backtrack(List<String> ans, StringBuilder cur, int open, int close, int max){
              if (cur.length() == max * 2) {
                  ans.add(cur.toString());
                  return;
              }

              if (open < max) {
                  cur.append('(');
                  backtrack(ans, cur, open+1, close, max);
                  cur.deleteCharAt(cur.length() - 1);
              }
              if (close < open) {
                  cur.append(')');
                  backtrack(ans, cur, open, close+1, max);
                  cur.deleteCharAt(cur.length() - 1);
              }
          }
      }

