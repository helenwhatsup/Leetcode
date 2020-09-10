class Solution {
    public int leastInterval(char[] tasks, int n) {
       //sort by frequenct
        
        // （最高频出现字母次数-1）* cooling period = max possible idle time.
        //没填满： return （num of tasks+空闲时间）。
        
        //step1. track frequency of each tasks.
          if (tasks.length <= 1 || n < 1) return tasks.length;
        int[] freq= new int[26]; //26个字母
         // Declare and create an array of 26 int

        for(char c: tasks){
            // Subtract the integer value of character 'a', this 
          //   puts 'A' at index 0, 'B' at index 1, and so on...
          //  int index = ch - 'A';
            
            //convert char to int ''
            freq[c-'A']++;
        }        
        
        //  eg. "A","B","C","A","D","B","A"
       //  freq: [3,2,1,1,0,0,0]
        Arrays.sort(freq); //从高到低sort by frquency，所以这里A频率最高。
        
        int max = freq[25]; //最大的那个。
        int slot=(max - 1) * (n + 1) + 1;;
        //然后，再放别的进去slot。
        int secondmax= 24;
       
        //再排序下一个任务，如果下一个任务B个数和最大任务数一致，
         //则retCount++ ==> A->B->X->A->B->X->A->B
        while(secondmax>=0 && freq[secondmax]==max){
            secondmax--;
            slot++;
        }
        return Math.max(tasks.length,slot);
        
    //最后的结果至少大于等于tasks.length，因为有空缺idle。
        
        
    }
}
