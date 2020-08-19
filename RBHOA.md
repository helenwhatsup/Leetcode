## Q1 ReverseDigits
12345-> 21435. 
  

                                public int reversedigit(int n){
                                String s = n+ " ";
                                String res="";

                                for(int i=0;i<n;i=i+2){
                                if(i+1<a.length()){
                                res+=s.charAt(i+1)+""+s.charAt(i);
                                }else{
                                    res+=s.charAt(i);
                                }

                                }

                                return Integer.parseInt(res);

                                }
                                
                                
                                
                                
## Q2 Sum of String
String s1 = "11";
String s2 = "9";
Output： ”110“


	public String add(String s1, String s2){
		if(s1 == null || s2 == null) return s1 == null ? s2 : s1;
		int idx1 = s1.length() - 1;
		int idx2 = s2.length() - 1;
		String res = "";
		while(idx1 >= 0 && idx2 >= 0){
			String result = (Integer.parseInt(s1.charAt(idx1) + "") + Integer.parseInt(s2.charAt(idx2) + "")) + "";
			res = result + res;
			idx1--;
			idx2--;
		}//到最头了 ， 把多的那截加上。
		 if(idx1 >= 0) res = s1.substring(0, idx1 + 1) + res;
		 else if(idx2 >= 0) res = s2.substring(0, idx2 + 1) + res;
		return res;
	}
  
