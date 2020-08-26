# Google OA
## Q1 Maximum Time
* You are given a string that represents time in the format hh:mm. Some of the digits are blank (represented by ?). 
Fill in ? such that the time represented by this string is the maximum possible. Maximum time: 23:59, minimum time: 00:00. You can assume that input string is always valid.

		public class Maxtime {
				// "static void main" must be defined in a public class.
				public class Main {
				    public static void main(String[] args) {
					giveMeMaxTime("23:5?");// 23:59
				    giveMeMaxTime("2?:22");// 23:22
				    giveMeMaxTime("0?:??");// 09:59
				    giveMeMaxTime("1?:??");// 19:59
				    giveMeMaxTime("?4:??");// 14:59
				    giveMeMaxTime("?3:??");// 23:59
				    giveMeMaxTime("??:??");// 23:59
				    giveMeMaxTime("?4:5?"); //14:59
				    }
    
		    public static void giveMeMaxTime(String time){
			char[] timechar = time.toCharArray();
			if(timechar[0]=='?'){
			timechar[0]=(timechar[1]<='3' || timechar[1] =='?') ?'2':'1'; 
			}
			if(timechar[1]=='?'){
			timechar[1]=(timechar[0]=='2')?'3':'9';
			//如果第一个数字是2，那么第二个数字就是3，这样组合就是23，如果不是2，则可能为1 or 0，所以第二个数字就写9

			}
			// timechar[2]=：  不用动
			// 如果timechar[3]=？ 则写5， timechar[4]=? 则填9
			timechar[3]=(timechar[3]=='?')?'5':timechar[3];
			timechar[4]=(timechar[4]=='?')?'9':timechar[4];

			System.out.println(timechar);

		    }


		}
## Q2 Hotel Booking 
You have to find which room is booked maximum number of times.
Example:

Input: ["+1A", "+3E", "-1A", "+4F", "+1A", "-3E"]
Output: "1A"
Explanation: 1A as it has been booked 2 times.



	public class Main {
	    public static void main(String[] args) {
			String[] A = { "+1A", "+3E", "-1A", "+4F", "+1A", "+1A", "-3E", "+3E", "+3E" };
		System.out.println(hotelbooking(A));
		}
	  //note substring(1): begin index=1

	    public static String hotelbooking(String []rooms){
	    Map<String,Integer>map=new HashMap<>();
	    String maxroom="";
	    int booktime=0;
	    int  maxbook=0;
	    for(String s:rooms){
		    if(s.charAt(0)=='+'){
		    String room=s.substring(1);
		    map.put(room,map.getOrDefault(room, 0)+1);

	//排序取最大
		   if(map.get(room)>maxbook){
		       maxbook=map.get(room);
		       maxroom=room;
		   }
		   // 次数相同
		   if(map.get(room)==maxbook){
		    if(maxroom.compareTo(room)==1){ //maxroom字母排序靠前
			maxroom=room;
		    }

		   }

		}
	    }   
	  return maxroom;
	    }
	}


## Q3 Largest Subarray Length K
* Compare all continuous subarray of length K and find the largest based on starting index. RETURN subarray
* Basically, my interpretation is that we can look at all the possible starting indices for a starting array and compare the first value. 
All elements are unique (distinct), so one value within an array will always be larger or smaller than another--giving us the largest subarray if we just compare that first index.
//最后一位starting index 是 n-k

		public class Main {
		  public static void main(String args[]) {
			int[] arr2 = new int[]{1,4,2,3,5,6};
			System.out.println(maxResultantArray(arr2,3));
		    }
  
		    public static int[] maxResultantArray(int[] arr, int k) {
			int []result= new int [k];
			int maxstart=0;
			int index=0;
			int maximum=Integer.MIN_VALUE;
			for(int i=0;i<arr.length-k;i++){
			 if(arr[i]>maximum){
			     maximum=arr[i];
			     index=i;
			 }
			 //得出来的是index with maximum starting point 
			    }
			    for(int i=0;i<k;i++){
			       result[i]= arr[index+i];
			    }
			return result;
			}

		}


## Q2 Spilt String 
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
    
    --------
 ## Q3 maximum subarray
 * Given array N and Int K, delete subarray of any size from array N so that the number of element > K and number of element <K are equal. 
 * Find maximum length of subarray after deletion. 
    
        public static int maxResultantArray(int[] arr, int k) {
            int [] sumarr= new int [arr.length];
            int totalsum=0;
            //create a new arr, record sum of this arr
            for(int i=0;i<arr.length;i++){
                if(arr[i]>k){
                    sumarr[i]=1;
                }
                else if(arr[i]<k){
                    sumarr[i]=-1;
                }
                else{
                    sumarr[i]=0;
                }
                totalsum+=sumarr[i];
            }
            //Now we have to find min subarray length with sum equal to cumulative sum of new array
            // Given an array containing 1,-1, and 0, find the minimum length subarray with sum as k == total_sum. Answer is n - subarray_len.

               HashMap<Integer,Integer> map= new HashMap<>();
                map.put(0,-1);   
                int cursum=0;

                int len=Integer.MAX_VALUE;

               //left pointer 
              int j=-1;
                for(int i=0;i<arr.length;i++){
                    cursum+=sumarr[i];
                    while(j<=i){
                    if(cursum==totalsum){
                        j++;
                        len=Math.min(len,i-j+1);
                        cursum-=sumarr[j];
                    }
                }


            }
            return arr.length-len;

            }
            }
## Q4 alphabet ordering


    int main() {
	
	string s;
	cin>>s;
	if(s.size()==0){cout<<0;return 0;}
	int ans=1;
	for(int i=0;i<s.size();i++){
	    ans++;
	    while(i+1<s.size()&&s[i]<=s[i+1])i++;
	    while(i+1<s.size()&&s[i]>=s[i+1])i++;
	    
	}
	
	cout<<ans;
    

