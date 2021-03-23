# Leetcode Review

## 35. Reverse Linked List 

### Description
Reverse a linked list.

### Python
```python
# Definition of ListNode
class ListNode(object):
    def __init__(self, val, next=None):
        self.val = val
        self.next = next

class Solution:
    """
    @param head: n
    @return: The new head of reversed linked list.
    """
    def reverse(self, head):
        # write your code here
        prev = None
        curr = head
        
        while curr != None:
            temp = curr.next
            curr.next = prev
            prev = curr
            curr = temp
        
        head = prev
        return head
```

### Java
```java
// Definition for ListNode
public static class ListNode {
    int val;
    ListNode next;

    ListNode(int x) {
        val = x;
        next = null;
    }
}

public class Solution {
    /**
     * @param head: n
     * @return: The new head of reversed linked list.
     */
    public ListNode reverse(ListNode head) {
        // write your code here
        ListNode prev = null;
        ListNode curr = head;
        
        while (curr != null) {
            ListNode temp = curr.next;
            curr.next = prev;
            prev = curr;
            curr = temp;
        }
        head = prev;
        return head;
    }
}
```

## 56. TwoSum

### Description

Given an array of integers, find two numbers such that they add up to a specific target number.

The function **twoSum** should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are zero-based.

### Note
1. The Hashtable is **O(1)** to query key.
2. Using the **target-number** as Hashtable key

### Python
```python
class Solution:
    """
    @param numbers: An array of Integer
    @param target: target = numbers[index1] + numbers[index2]
    @return: [index1 + 1, index2 + 1] (index1 < index2)
    """
    def twoSum(self, numbers, target):
        # write your code here
        table = {}
        for i in range(len(numbers)):
            if numbers[i] not in table:
                table[target - numbers[i]] = i
            else:
                if table.get(numbers[i]) > i :
                    return [i,table.get(numbers[i])]
                else:
                    return [table.get(numbers[i]),i]
```

### Java
```java
import java.util.Hashtable;

public class TwoSum {
    /**
     * @param numbers: An array of Integer
     * @param target:  target = numbers[index1] + numbers[index2]
     * @return: [index1 + 1, index2 + 1] (index1 < index2)
     */
    public int[] twoSum(int[] numbers, int target) {
        // write your code here
        Hashtable<Integer, Integer> hashtable = new Hashtable<>();
        int[] result = new int[2];
        for (int i = 0; i < numbers.length; i++) {
            if (!hashtable.containsKey(numbers[i])) {
                hashtable.put(target - numbers[i], i);
            } else {
                if (i > hashtable.get(numbers[i])) {
                    result[0] = hashtable.get(numbers[i]);
                    result[1] = i;
                } else {
                    result[1] = hashtable.get(numbers[i]);
                    result[0] = i;
                }
                return result;
            }
        }
        return null;
    }
}

```