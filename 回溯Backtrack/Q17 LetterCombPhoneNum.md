## Q17 Letter Combinations of a Phone Number
https://leetcode.com/problems/letter-combinations-of-a-phone-number/



class Solution {
 Map<Character, String> map = new HashMap<Character, String>() {{
            put('2', "abc");
            put('3', "def");
            put('4', "ghi");
            put('5', "jkl");
            put('6', "mno");
            put('7', "pqrs");
            put('8', "tuv");
            put('9', "wxyz");
          }};
    public List<String> letterCombinations(String digits) {
      // 最开始是空的，然后空的选了a，a选ad ae af,撤回到a，撤回到空。
    //继续选b，以此类推。
        List<String> list= new ArrayList<>();
        if(digits==null || digits.length()==0){
            return list;
        }
        
        StringBuilder sb= new StringBuilder();
        backtrack(list,digits,new StringBuilder(),0);
        return list;
        
    }
    public void backtrack(List<String>list,String digits,StringBuilder sb,int start){
        if(sb.length()==digits.length()){
            list.add(sb.toString());
        }
        
        // recursion
        
        for(int i=start;i<digits.length();i++){
            //key in the map
            
           String s=map.get(digits.charAt(i));
            
          for(int j=0;j<s.length();j++){
              Character a= s.charAt(j);
              sb.append(a);
              backtrack(list,digits,sb,i+1);
              sb.deleteCharAt(sb.length()-1); //eg. 从ad恢复到a
          }  
        }
