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
  
## Q3 NUm of even digit
		import java.util.*;

		class evendigit {
			public static void main(String[] args){
				evendigit instance = new evendigit();
				int a = 2468;
			System.out.println(instance.evendigit(a));
			//return 4.
			}

			public int evendigit(int a){
			int res=0;
			String s=a+"";
			for(int i=0;i<s.length();i++){
			    if(Integer.parseInt(s.charAt(i)%2==0){
			    res=res+1;
			    })
			}
			    return res;
			}
		}

## Q4 Rotate over diagonal (n=1,rotate 90; n=2,rotate 180,n=3,rotate 270)
			  int M[][] = { {1, 2, 3}, 
					{4, 5, 6},     
					{7, 8, 9}}; 
		90:
				1 4 3 
				8 5 2 
				7 6 9 

    import java.util.*;

    class rotateMatrix {
        public int[][] rotate(int[][] M, int n){
            if(n==1){
                int[][]res=rotate90(M);
                return res;
            }
            if(n==2){
                int[][]res=rotate180(M);
                return res;
            }
            if(n==3){
                int[][]res=rotate270(M);
                return res;
            }
        }

        public int[][] rotate90(int[][]M){
            int l=M.length();
            int result=new int[n][n];
            for(int i=0;i<n;i++){
                for(int j=0;j<n;j++){
                    //diagonal and anti-diagonal
                    if(i+j==n-1|| i==j){
                        res[i][j]==M[i][j];
                    }else{
                        res[j][n-1-i]=M[i][j];
                    }
                }
            }
                return res;
        }

        public int[][] rotate180(int[][]M){
            int l=M.length();
            int result=new int[n][n];
            for(int i=0;i<n;i++){
                for(int j=0;j<n;j++){
                    //diagonal and anti-diagonal
                    if(i+j==n-1|| i==j){
                        res[i][j]==M[i][j];
                    }else{
                        res[n-1-i][n-1-j]=M[i][j];
                    }
                }
            }
                return res;
        }
        public int[][] rotate270(int[][]M){
            int l=M.length();
            int result=new int[n][n];
            for(int i=0;i<n;i++){
                for(int j=0;j<n;j++){
                    //diagonal and anti-diagonal
                    if(i+j==n-1|| i==j){
                        res[i][j]==M[i][j];
                    }else{
                        res[n-1-j][i]=M[i][j];
                    }
                }
            }
                return res;
        }
    }


## Q5 calculate alternating sum

//eg. input 123456, return 1-2+3-4+5-6 = -3

    public static int altersum(int n) {
        String s = Integer.toString(n);
        int res=0;
        //store in arr of digits

        int[] arr = new int[s.length()];
        for (int i = 0; i < s.length(); i++)
        {
            arr[i] = s.charAt(i) - '0';
            //char to int 
        }
        //int to arr of digits
        for(int i=0;i<arr.length;i++){
            if(i%2==0){
                res+=arr[i];
            }else{
                res-=arr[i];
            }
                    }
                    return res;
    }    
}


## Q6 RemoveDigit
* Calculate how many ways exactly one digit could be removed from one of the strings so that s is lexicographically smaller than t

				int removeOne(String s, String t){
				int slen=s.length();
				int tlen=t.length();
				int count=0;

				for(int i=0;i<slen;i++){
				    if(s.charAt(i)-'0'>=0 && s.charAt(i)<=9){
					//i+1 is starting index
					String tmp=s.substring(0,i)+s.substring(i+1);
					if(tmp.compareTo(t)<0){
					    count++;
					}

				    }
				}

				for(int j=0;j<tlen;j++){
				    if(s.charAt(j)-'0'>=0 && s.charAt(j)<=9){
					//i+1 is starting index
					String tmp=t.substring(0,j)+t.substring(j+1);
					if(s.compareTo(tmp)<0){
					    count++;
					}

				    }
				}
				return count;

				}
## Q7 Sort diagonal  每条左上到右下diagonal都要sorted 
			public int[][] sortDiagonals(int[][] matrix) {
			    int n = matrix.length;
			    if(n < 2) {
				return matrix;
			    } else {
				for(int i = n - 2; i >= 0; i--) {
				    int x = i;
				    int y = 0;
				    ArrayList<Integer> list = new ArrayList<>();
				    while(y < n && x < n) {
					list.add(matrix[x][y]);
					y++;
					x++;
				    }
				    Collections.sort(list);
				    x = i;
				    y = 0;
				    while(y < n && x < n) {
					matrix[x][y] = list.get(y);
					y++;
					x++;
				    }
				}
				for(int j = 1; j < n - 1; j++) {
				    int x = 0;
				    int y = j;
				    ArrayList<Integer> list = new ArrayList<>();
				    while(y < n && x < n) {
					list.add(matrix[x][y]);
					y++;
					x++;
				    }
				    Collections.sort(list);
				    x = 0;
				    y = j;
				    while(y < n && x < n) {
					matrix[x][y] = list.get(x);
					y++;
					x++;
				    }
				}
				return matrix;
			    }
			}

			public static void print2D(int mat[][]) 
			{ 
			    for (int[] row : mat) 
				System.out.println(Arrays.toString(row)); 
			} 
			}



## Q8 Good Tuple: exactly two out of three are equal. use hashset and if size maintains 2, res++
		public static void main(String args[]) {
		       // int[] arr2 = new int[]{1, 2, 3,4, 4, 5,5,6,6, 6};
			String s="11215323";

        System.out.println(goodtuple(s));
    }
  	public static int goodtuple(String cur) {
		if(cur.length() < 3) {
			return 0;
		}
		int res = 0;
		for(int i = 1; i < cur.length() - 1; i++){
            HashSet<Character> set = new HashSet<>();
            //Set集合中不允许添加重复的元素，如果有两个重复的话size就是2.
			set.add(cur.charAt(i));
			set.add(cur.charAt(i - 1));
			set.add(cur.charAt(i + 1));
			if(set.size() == 2) {
				res++;
			}
		}
		return res;
	}

}

## Q9 divisorSubstrings
* Give a number n and digit number k find the number of serial substring which is able to divisible n.

		public static int findDivisor(int n, int k) {
		    String big= n+"";
		    int res=0;
		    HashSet<Integer> set=new HashSet<>();
		    for(int i=0;i<=big.length()-k;i++){
			 int win=Integer.parseInt(big.substring(i,i+k-1));
			 if(!set.contains(win)&& n%win==0){
			     set.add(win);
			     res++;
			 }

		    }
		 return res;

		 }


