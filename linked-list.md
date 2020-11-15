# Linked-list

+ [Remove Nth Node From End of List](#remove-nth-node-from-end-of-list)
+ [Merge Two Sorted Lists](#merge-two-sorted-lists)
+ [Linked List Cycle](#linked-list-cycle)
+ [Linked List Cycle II](#linked-list-cycle-II)
+ [Reorder List](#reorder-list)
+ [Reverse Linked List](#reverse-linked-list)
+ [Palindrome Linked List](#palindrome-linked-list)
+ [Middle of the Linked List](#middle-of-the-linked-list)


## Reverse Linked List

https://leetcode.com/problems/reverse-linked-list/

Reverse a singly linked list.

Example:
```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```
Follow up:
A linked list can be reversed either iteratively or recursively. Could you implement both?

```java 
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode curr = head;
        while(curr != null){
            ListNode nextTemp = curr.next;
            curr.next = prev;
            prev = curr;
            curr = nextTemp;
        }
        return prev;
    }
}
```

## Middle of the Linked List

https://leetcode.com/problems/middle-of-the-linked-list/

Given a non-empty, singly linked list with head node head, return a middle node of linked list.
If there are two middle nodes, return the second middle node.

Example 1:
```
Input: [1,2,3,4,5]
Output: Node 3 from this list (Serialization: [3,4,5])
The returned node has value 3.  (The judge's serialization of this node is [3,4,5]).
Note that we returned a ListNode object ans, such that:
ans.val = 3, ans.next.val = 4, ans.next.next.val = 5, and ans.next.next.next = NULL.
```
Example 2:
```
Input: [1,2,3,4,5,6]
Output: Node 4 from this list (Serialization: [4,5,6])
Since the list has two middle nodes with values 3 and 4, we return the second one.
``` 

Note:
The number of nodes in the given list will be between 1 and 100.

```java
class Solution {
    public ListNode middleNode(ListNode head) {
        if(head.next==null) return head;
        if(head.next.next==null) return head.next;
        ListNode[] A = new ListNode[100];
        int t = 0;
        while (head.next != null) {
            A[t++] = head;
            head = head.next;
        }
        int middle = (t%2==0)?(t/2):(t/2+1);
        return A[middle]; 
    }
}
```
## Palindrome Linked List
Given a singly linked list, determine if it is a palindrome.

Example 1:
```
Input: 1->2
Output: false
```
Example 2:
```
Input: 1->2->2->1
Output: true
```
Follow up:
Could you do it in O(n) time and O(1) space?

```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        List<Integer> vals = new ArrayList<>();
        
        //Convert LinkedList into ArraysList
        ListNode currentNode = head;
        while (currentNode != null){
            vals.add(currentNode.val);
            currentNode = currentNode.next;
        }
        
        //Use two-pointer technique to check for pflindrome.
        int front = 0;
        int back = vals.size() - 1;
        while(front < back){
            //Note that we must use ! . equals instead of !=
            //we are comparing Integer, not int.
            if(!vals.get(front).equals(vals.get(back))){
                return false;
            }
            front++;
            back--;
        }
        return true;
    }
}
```

## Merge Two Sorted Lists
https://leetcode.com/problems/merge-two-sorted-lists/

Merge two sorted linked lists and return it as a new sorted list. The new list should be made by splicing together the nodes of the first two lists.

 Example 1:|"
Input: l1 = [1,2,4], l2 = [1,3,4]
Output: [1,1,2,3,4,4]
Example 2:

Input: l1 = [], l2 = []
Output: []
Example 3:

Input: l1 = [], l2 = [0]
Output: [0]
 

Constraints:

The number of nodes in both lists is in the range [0, 50].
-100 <= Node.val <= 100
Both l1 and l2 are sorted in non-decreasing order.

```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode curLeft = l1;
        ListNode curRight = l2;
        ListNode dummyHead = new ListNode();
        ListNode curRes = dummyHead;
        
        while(curLeft != null && curRight != null){
            if(curLeft.val < curRight.val){
                curRes.next = curLeft;
                curLeft = curLeft.next;
            } else {
                curRes.next = curRight;
                curRight = curRight.next;
            }  
            curRes = curRes.next;
        } 
        while(curLeft != null){
            curRes.next = curLeft;
            curLeft = curLeft.next;
            curRes = curRes.next;
        }
        while(curRight != null){
            curRes.next = curRight;
            curRight = curRight.next;
            curRes = curRes.next;
        }    
        return dummyHead.next;
    }
}
```
```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode curLeft = l1;
        ListNode curRight = l2;
        ListNode dummyHead = new ListNode();
        ListNode curRes = dummyHead;
        
        while(curLeft != null && curRight != null){
            if(curLeft.val < curRight.val){
                curRes.next = curLeft;
                curLeft = curLeft.next;
            } else {
                curRes.next = curRight;
                curRight = curRight.next;
            }  
            curRes = curRes.next;
        } 
        if (curLeft != null){
            curRes.next = curLeft;
        }
        if (curRight != null){
            curRes.next = curRight;
        }    
        return dummyHead.next;
    }
}
```

## Remove Nth Node From End of List
Given the head of a linked list, remove the nth node from the end of the list and return its head.
Follow up: Could you do this in one pass?

Example 1:
```
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
```
Example 2:
```
Input: head = [1], n = 1
Output: []
```
Example 3:
```
Input: head = [1,2], n = 1
Output: [1]
``` 

Constraints:
The number of nodes in the list is sz.
1 <= sz <= 30
0 <= Node.val <= 100
1 <= n <= sz
```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        int length = 0;
        ListNode first = head;
        while(first != null){
            length++;
            first = first.next;
        }
        length -= n;
        first = dummy;
        while(length > 0){
            length --;
            first = first.next;
        }
        first.next = first.next.next;
        return dummy.next;
    }
}
```

## Linked List Cycle II
https://leetcode.com/problems/linked-list-cycle-ii/
Given a linked list, return the node where the cycle begins. If there is no cycle, return null.
There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.
Notice that you should not modify the linked list.

Example 1:
```
Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```
Example 2:
```
Input: head = [1,2], pos = 0
Output: tail connects to node index 0
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```
Example 3:
```
Input: head = [1], pos = -1
Output: no cycle
Explanation: There is no cycle in the linked list.
```
Constraints:
The number of the nodes in the list is in the range [0, 104].
-105 <= Node.val <= 105
pos is -1 or a valid index in the linked-list.
 
Follow up: Can you solve it using O(1) (i.e. constant) memory?

```java 
public class Solution {
    public ListNode detectCycle(ListNode head) {
        Set<ListNode> visited = new HashSet<ListNode>();
        
        ListNode node = head;
        while(node !=null){
            if(visited.contains(node)){
                return node;
            }
            visited.add(node);
            node = node.next;
        }
        return null;
    }
}
```
## Reorder List
https://leetcode.com/problems/reorder-list/
Given a singly linked list L: L0→L1→…→Ln-1→Ln,
reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…
You may not modify the values in the list's nodes, only nodes itself may be changed.

Example 1:
```
Given 1->2->3->4, reorder it to 1->4->2->3.
```
Example 2:
```
Given 1->2->3->4->5, reorder it to 1->5->2->4->3.
```
```java
class Solution {
    public void reorderList(ListNode head) {
        if(head == null){
            return;
        }
        
        //Find the middle of linked list
        //F.e. in [1]->[2]->[3]->[4]->[5]->[6]
        ListNode slow = head, fast = head;
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
        }
        
        //Reverse the second part of the list
        //convert [1]->[2]->[3]->[4]->[5]->[6] into [1]->[2]->[3]->[4] and [6]->[5]->[4]
        //reverse the second half in-place
        ListNode prev = null, curr = slow, tmp;
        while(curr != null){
            tmp = curr.next;
            
            curr.next = prev;
            prev = curr;
            curr = tmp;
        }
        
        //Merge tro sorted linked lists
        //merge [1]->[2]->[3]->[4] and [6]->[5]->4 into [1]->[6]->[2]->[5]->[3]->[4]
        ListNode first = head, second = prev;
        while(second.next != null){
            tmp = first.next;
            first.next = second;
            first = tmp;
            
            tmp = second.next;
            second.next = first;
            second = tmp;
        }
    }
}
```
Solution Bricks
This problem is a combination of these three easy problems:
876. Middle of the Linked List
206. Reverse Linked List
21. Merge Two Sorted Lists
