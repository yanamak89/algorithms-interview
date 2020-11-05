# Arrays

+ [206. Reverse Linked List](#206_reverse-linked-list)
+ [876. Middle of the Linked List](876-middle-of-the-linked-list)
+ [234. Palindrome Linked List](234-palindrome-linked-list)

## 206. Reverse Linked List

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

## 876. Middle of the Linked List

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
## 234. Palindrome Linked List
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
