# Code Review

## Stack Implement

### Note
1. Due to the **FIFO**, only the **first node** is stored.
2. It will be more efficient to divide the size of array by 4

### LinkedList
```+java
public class StackLinkedList {
    Node first = null;

    public static class Node {
        String item;
        Node next;
    }

    public boolean isEmpty() {
        return first == null;
    }

    public void push(String item) {
        Node oldFirst = first;
        first = new Node();
        first.item = item;
        first.next = oldFirst;
    }

    public String pop() {
        String item = first.item;
        first = first.next;
        return item;
    }
}
```

### Array
```+java
public class StackArray {
    String[] array = new String[1];
    int index = 0;

    public void push(String item) {
        if (index == array.length) {
            resize(2 * array.length);
        }
        array[index++] = item;
    }

    public String pop() {
        String item = array[--index];
        array[index] = null;
        if (index > 0 && index == array.length / 4) {
            resize(array.length / 2);
        }
        return item;
    }

    public void resize(int size) {
        String[] newArray = new String[size];
        for (int i = 0; i < index; i++) {
            newArray[i] = array[i];
        }
        array = newArray;
    }
}
```

## Queue Implement

### LinkedList
```+java
public class QueueLinkedList {
    Node first, last;

    public class Node {
        Node next;
        String item;
    }

    public boolean isEmpty() {
        return first == null;
    }

    public void enqueue(String item) {
        Node oldLast = last;
        last = new Node();
        last.item = item;
        last.next = null;
        if (isEmpty()) {
            first = last;
        } else {
            oldLast.next = last;
        }

    }

    public String dequeue() {
        String item = first.item;
        first = first.next;
        if (isEmpty()) {
            last = null;
        }
        return item;
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
```+python3
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
```+Java
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

## 35. Reverse Linked List 

### Description
Reverse a linked list.

### Note
1. **Can not** point directly to original node
2. The new node is created to point previous node

### Python
```+python3
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
        while head != None:
            prev = ListNode(head.val, prev)
            head = head.next
        return prev
```

### Java
```+java
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
        while (head != null) {
            ListNode node = new ListNode(head.val);
            node.next = prev;
            prev = node;
            head = head.next;
        }
        return prev;
    }
}
```
