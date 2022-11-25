# Leetcode-Hot100 T2 两数相加

## 2022-04-12

```java
/**
* Leetcode 2.两数相加
* 
*
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
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    //the return List: sum
    ListNode sum = new ListNode(0);
    
    //length of sum
    int length = 0;
    
    //get the longer length of l1 and l2
    int len1 = 1, len2 = 1;
    ListNode temp = l1;
    while(temp.next != null){
        len1++;
        temp = temp.next;
    }
    temp = l2;
    while(temp.next != null){
        len2++;
        temp = temp.next;
    }
    
    //set length into the longer one
    length = len1 >= len2 ? len1 : len2;
    
    //set the sum-list each val = 0
    //and complete l1, l2 with 0
    ListNode ptr = sum;
    ListNode ptr1=l1;
    ListNode ptr2=l2;
    for(int i=0;i<length;i++){
        ptr.val = 0;
        ptr.next = new ListNode(0);
        ptr = ptr.next;

        if(ptr1.next == null){
            ptr1.next = new ListNode(0);
        }
        if(ptr2.next == null){
            ptr2.next = new ListNode(0);
        }
        ptr1 = ptr1.next;
        ptr2 = ptr2.next;
    }   
    
    
    //core part
    //go through l1,l2, get each val of sum by adding l1 and l2
    ptr1 = l1;
    ptr2 = l2;
    ptr = sum;
    for(int i=0;i<length;i++){
        ptr.val += (ptr1.val + ptr2.val);
        if(ptr.val >= 10){
            ptr.val -= 10;
            ptr.next.val += 1;
        }
        ptr = ptr.next;
        ptr1 = ptr1.next;
        ptr2 = ptr2.next;
    }
    
	//check whether sum-list has Zero ahead 
    ListNode check_ptr = sum;
    for(int i=0;i<length;i++){
        if(check_ptr.next.val == 0 && check_ptr.next.next == null)
            {check_ptr.next = null;break;}
        check_ptr = check_ptr.next;
    }
    
    return sum;
}
}
```

# Offcial Solution
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode pre = new ListNode(0);
        ListNode cur = pre;
        int carry = 0;
        while(l1 != null || l2 != null) {
            int x = l1 == null ? 0 : l1.val;
            int y = l2 == null ? 0 : l2.val;
            int sum = x + y + carry;
            
            carry = sum / 10;
            sum = sum % 10;
            cur.next = new ListNode(sum);

            cur = cur.next;
            if(l1 != null)
                l1 = l1.next;
            if(l2 != null)
                l2 = l2.next;
        }
        if(carry == 1) {
            cur.next = new ListNode(carry);
        }
        return pre.next;
    }
}

/* 作者：guanpengchn
 * [链接](https://leetcode-cn.com/problems/add-two-numbers/solution/hua-jie-suan-fa-2-liang-shu-xiang-jia-by-guanpengc/)
 * 来源：力扣（LeetCode）
*/
```