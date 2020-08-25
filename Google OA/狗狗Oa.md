## Google OA
* You are given a string s, a split is called good if you can split s into 2 non-empty strings p and q where its concatenation is equal to s and the number of distinct letters in p and q are the same.

Return the number of good splits you can make in s.
Eg:   
Input: "aaaa"  
Output: 3   
Explanation: we can get a - aaa, aa - aa, aaa- a   

--- Sol1. 超时

    class Solution {
        public int numSplits(String s) {
        HashMap<Character,Integer> map= new HashMap<>();
         HashSet<Character> left= new HashSet<>();
         HashSet<Character>right= new HashSet<>();
            int count=0;
            int n=s.length();
       
        for(int i=0;i<s.length();i++){
            String l=s.substring(0,i);
            String r=s.substring(i,s.length());
            
            for(Character c: l.toCharArray()){
                left.add(c);
            }
            for(Character c: r.toCharArray()){
                right.add(c);
            }
          
            if(left.size()==right.size()){
                count++;
            }
            left.clear();
            right.clear();
           
            
        }
    return count;


        }
    }

--- Sol2. Good

            class Solution {
                public int numSplits(String s) {
               if (s == null || s.length() == 0) {
                  return 0;
                }

    Map<Character,Integer> counts = new HashMap<Character,Integer>();
    
    for(Character c: s.toCharArray()){
        counts.put(c,counts.getOrDefault(c,0)+1);
    }
    
    int ways = 0;
    
    Set<Character> leftChars = new HashSet<Character>();
    for (int i = 0; i < s.length() - 1; i++) {
      char curr = s.charAt(i);
      leftChars.add(curr);
      
      int rightCount = counts.get(curr) - 1;
      
      if (rightCount == 0) {
        counts.remove(curr);
      } else {
        counts.put(curr, rightCount);
      }
      
      if (leftChars.size() == counts.size()) {
        ways++;
      }
    }
    
    return ways;
      }
    }

    
