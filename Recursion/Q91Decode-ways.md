## Q91. Decode Ways
          
          
          
          
          class Solution {
              HashMap<Integer, Integer> memo = new HashMap<>();

              public int numDecodings(String s) {

                  return decode(s,0);


              }
              //2|32232323232 和 23|2232323232
          //   爬楼梯变种！！
          // 所以，如果我们分别知道了上边划分的右半部分 32232323232 的解码方式是 ans1 种，2232323232 的解码方式是 ans2 种，那么整体 232232323232 的解码方式就是 ans1 + ans2 种。可能一下子，有些反应不过来，可以看一下下边的类比。

          // 假如从深圳到北京可以经过武汉和上海两条路，而从武汉到北京有 8 条路，从上海到北京有 6 条路。那么从深圳到北京就有 8 + 6 = 14 条路。

          //从中，我们可以看出规律。
          // 如果开始的数为0，结果为0。
          // 如果开始的数加上第二个数小于等于26。结果为 numDecodings（start+1）+ numDecodings（start +2）
          // 如果开始的数加上第二个数大于26。结果为 numDecodings（start +1）

              //如果为2067。 结果为numDecodings（20 67）+ numDecodings（2 067）= numDecodings(20 67)

              public int decode(String s,int index){
                  // end条件:
                  if(s.length()==0 || s==null){
                      return 0;
                  }
                  if (index == s.length()) {
                      return 1;
                  }

                  // If the string starts with a zero, it can't be decoded
                  if (s.charAt(index) == '0') {
                      return 0;
                  }

                  if (index == s.length()-1) {
                      return 1;
                  }

                  if(memo.containsKey(index)){
                      return memo.get(index);
                  }
                  //decode 326= decode(3 26)+ decode(32 6)(x)
              //waysOf: decode 2326=waysOfdecode(2| 326)+decode(23|26)

                  //当前的答案= decode(往后1位)+decode(往后2位)
                  int ways=decode(s,index+1);
                   if (Integer.parseInt(s.substring(index, index+2)) <= 26) {
                       ways += decode(s,index+2);
                   }


                  memo.put(index,ways);
                  return ways;

              }
          }
