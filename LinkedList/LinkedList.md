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
## Sol2:
