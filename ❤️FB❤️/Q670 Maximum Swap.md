## Q670 Maximum Swap
### Sol1: BF



###  SOl2: 目标：最低位的最大数放在最适合的最高位。map 存储最低位的最大数字和index. 然后再正序从一个数开始遍历，找到第一个不是最大的数，将该位置和右边最大数换位置.如果找到的数跟最大一样就不用换了呗。



       class Solution {
            //Sol 2: 目标：最低位的最大数放在最适合的最高位。
               //map 存储最低位的最大数字和index.
                //然后再正序从一个数开始遍历，找到第一个不是最大的数，将该位置和右边最大数换位置. 
               public int maximumSwap(int num) {
               if(num == 0)
                   return 0;
               char[] chars = String.valueOf(num).toCharArray();
               int[] maxIndex = new int[chars.length];
               int max = chars.length - 1;
               //倒过来寻找，当前位置往右，最大的数的下标
               for(int j = chars.length - 1;j>=0;j--){
                   if(chars[j] - '0' > chars[max] - '0'){
                       max = j;
                   }
                   maxIndex[j] = max;
               }
               //正序遍历，找到第一个不是最大的数，将该位置和右边最大数换位置
               for(int i = 0;i<chars.length;i++){
                   int iValue = chars[i] - '0';
                   int maxValue = chars[maxIndex[i]] - '0';
                   if(maxValue != iValue){
                       chars[i] = (char) (maxValue + '0');
                       chars[maxIndex[i]] = (char) (iValue + '0');
                       break;
                   }
               }
               return Integer.parseInt(new String(chars));
           }


