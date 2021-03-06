## LC Q76  Minimum Window Substring


      class Solution {
          public String minWindow(String s, String t) {
      if(s == null || t == null || s.length() == 0 || t.length() == 0 || s.length() < t.length()) return "";
              int min=Integer.MAX_VALUE;

              HashMap<Character,Integer> mapT= new HashMap<>();

              for(Character c: t.toCharArray()){
                  mapT.put(c,mapT.getOrDefault(c,0)+1);
              }

              boolean flag = false;

              int start=0;
              int end=0;

              int minLeft = 0;
              int minRight = 0;

              int count=t.length(); // the number of characters that I need to match
              //记住一点：map始终记录着当前滑动窗口下，我们还需要的元素数量，我们在改变i,j时，需同步维护need。 
              while(end<s.length()){

                  Character c=s.charAt(end); //get a char

                  if(mapT.containsKey(c)){
          //例如当滑动窗口包含某个元素，我们就让need中这个元素的数量减1，代表所需元素减少了1个；当滑动窗口移除某个元素，就让need中这个元素的数量加1。
                      mapT.put(c,mapT.get(c)-1);
                      //需要的数量减少了1. 就我们不需要当前的indicates we have found at least one element from the substring. 
                      if(mapT.get(c)>=0){
                          count--;
                      }
                  }

                  while(count==0 && start<=end){
                      //count==0就是维持 窗口中要找东西的个数。 只要窗口内匹配的字符达到了要求，右边界固定，左边界收缩
                      //找到了一个substring，移动左指针。
                      flag=true;
                    int curLen = end + 1 - start;
                      if(curLen <= min){
                          minLeft = start;
                          minRight = end;
                          min = curLen;
                      }

                      Character leftC= s.charAt(start);
                      //原来减去的给加回来
                       if(mapT.containsKey(leftC)){
                          mapT.put(leftC, mapT.get(leftC) + 1);//释放字符。
                          if(mapT.get(leftC) >= 1) count++;
                           //map.get(char)>=1说明已经不被需要了，所以窗口中要找的东西+1，needcount+1. 
                      }
                          start++;
                  }

                   end++;
              }
              return flag == true ? s.substring(minLeft,minRight+1): "";

          }
      }
