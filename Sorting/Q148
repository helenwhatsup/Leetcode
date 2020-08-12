perform merge sort on linkedlist 

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode sortList(ListNode head) {
//而归并排序（又称混合排序）因其可以利用递归来交换数字，天然适合链表这种结构。
归并排序的核心是一个 merge() 函数，其主要是合并两个有序链表。是将链表从中间断开，分成两部分，左右两边再分别调用排序的递归函数 sortList()，得到各自有序的链表后，
再进行 merge()，这样整体就是有序的了。
        if(head == null){
            return head;
        }
        if(head.next == null){
            return head;
        }
        
      ListNode pre=head;
      ListNode slow=head;
      ListNode fast=head;
        while(fast!=null && fast.next!=null){
            pre=slow;
            slow=slow.next;
            fast=fast.next.next;
        }
      // 第一段 head to slow, 第二段，slow to end
       pre.next = null;
        
        //handle those two sub list
        ListNode h1 = sortList(head); //断成一个一个mode，然后一个一个merge
        ListNode h2 = sortList(slow);
        
        return merge(h1, h2);
    }
    
    
    
    public ListNode merge(ListNode left, ListNode right){
        if(left==null) return right;
        if(right==null) return left;
        if(left.val<=right.val){
            left.next=merge(left.next,right);
            return left;   
        }else{
            right.next=merge(left,right.next);
            return right;
        }
    }
}
        
  

