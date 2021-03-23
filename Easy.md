# Data Structure Implement

## Stack

1. Due to the **LIFO**, only the **first node** is stored.
2. It will be more efficient to divide the size of array by 4

### LinkedList
```java
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
```java
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

## Queue

1. Due to the **FIFO**,  the first and last node need to be stored
2. Last node as a new node, first node as a first remove node

### LinkedList
```java
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

## Heap
```java
// Comming
```