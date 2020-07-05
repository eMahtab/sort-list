# Sort List
## https://leetcode.com/problems/sort-list


# Implementation :
```java
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
    if (head == null || head.next == null)
          return head;
        
    // step 1. cut the list to two halves
    ListNode prev = null, slow = head, fast = head;
    
    while (fast != null && fast.next != null) {
      prev = slow;
      slow = slow.next;
      fast = fast.next.next;
    }
    
    prev.next = null;
    
    // step 2. sort each half
    ListNode l1 = sortList(head);
    ListNode l2 = sortList(slow);
    
    // step 3. mergeSort l1 and l2
    return mergeSort(l1, l2);
  }
  
  private ListNode mergeSort(ListNode l1, ListNode l2) {
     ListNode dummyHead = new ListNode(0), current = dummyHead;
    
     while (l1 != null && l2 != null) {
        if (l1.val < l2.val) {
            current.next = l1;
            l1 = l1.next;
        } else {
            current.next = l2;
            l2 = l2.next;
        }
        current = current.next;
    }
    
    while (l1 != null) {
        current.next = l1;
        current = current.next;
        l1 = l1.next;
    }
      
    while (l2 != null) {
        current.next = l2;
        current = current.next;
        l2 = l2.next;
    }
    
    return dummyHead.next;
  }
}
```

# References :
1. https://www.youtube.com/watch?v=vH-o_6rwCEE
2. https://leetcode.com/problems/sort-list/discuss/46714/Java-merge-sort-solution
