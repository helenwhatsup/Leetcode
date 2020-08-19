## Q1 ReverseDigits
  

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
