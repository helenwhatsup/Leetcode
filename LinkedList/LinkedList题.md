# LinkedList
* remove(new Integer(1))

* remove(Object o)
* remove(int index)
* That means that list.remove(1) removes the object at position 1 
* remove(new Integer(1)) removes the first occurrence of the specified element from this list.


## Q23 Merge k Sorted Lists

 https://leetcode.com/problems/merge-k-sorted-lists/
 
 ### Sol1:  ArrayList Time: O(n)+O(nlogn)+O(n)
 
    class Solution {
        public ListNode mergeKLists(ListNode[] lists) {
            ArrayList<Integer> res= new ArrayList<>();
            for(ListNode l: lists){
                while(l!=null){
                res.add(l.val);
                l=l.next; //往下走
                }
            }
            Collections.sort(res);
            //build new linkedlist

            ListNode head = new ListNode(0);
            ListNode h = head; // h moves. 
            for(int a: res){
                ListNode node= new ListNode(a);
                h.next=node; //head point to new node
                h=h.next; //head指向下一个node point to the next tnode 
            }
           //h.next=null;
            return head.next;
            }}
 ---
## Sol2:好聪明！！
 *  l和r是链条位置。比如list有3条链子，l=0，r=2，mid=1
 * l1 是merge 链条lists[0]到lists[mid]
 * l2是merge链条 list[mid+1]到list[r]. 然后最后大merge
 
 

          public ListNode mergeKLists(ListNode[] lists) {
              // recursion
              if(lists.length==0){
              return null;
              }
              return partitonMerge(lists, 0, lists.length - 1);
        }
        
       public static ListNode partitonMerge(ListNode[]lists, int left,int right){
           //l和r是链条位置。比如list有3条链子，l=0，r=2，mid=1
           //l1 是merge 链条lists[0]到lists[mid]
           // l2是merge链条 list[mid+1]到list[r]
          //  然后最后大merge
              if (left == right) return lists[left];
           int mid = left + (right - left) / 2;
           ListNode l1 = partitonMerge(lists, left, mid);
           ListNode l2 = partitonMerge(lists, mid + 1, right);
           return mergetwo(l1, l2);

       }
       public static ListNode mergetwo(ListNode l1, ListNode l2){
          if(l1==null){
              return l2;
          }
          if(l2==null){
              return l1;
          }
          //比较value
          if(l1.val<l2.val){
              l1.next=mergetwo(l1.next,l2);
              return l1;
          }else {
              l2.next=mergetwo(l1,l2.next);
              return l2;
          }

     
