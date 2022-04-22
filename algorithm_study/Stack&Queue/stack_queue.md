# Stack and Queue 스택과 큐 (자료구조 기본)
자료구조란 데이터를 표현하고 관리하고 처리하기 위한 구조를 의미하며 그중 스택과 큐는 자료구조의 기초 개념으로 다음의 두 핵심적인 함수로 구성된다.
- **Push** : 데이터를 삽입한다.
- **Pop** : 데이터를 삭제한다.

스택과 큐를 사용할때 _오버플로와 언더플로_ 에 유의해야 한다.

## Stack 스택 (Kellerspeicher)
스택은 **박스 쌓기**에 비유할 수 있다.  
박스는 아래에서부터 위로 차곡차곡 쌓는다. 그리고 아래에 있는 박스를 치우기 위해서는 위에 있는 박스를 먼저 내려야 한다. 이러한 구조를
- **Last In First Out (LIFO)** 후입선출 또는
- **First out Last In (FOLI)** 선입후출 구조라고 한다.  

One case where stacks are often useful is in certain **recursive algorithms**. Sometimes you need to push temporary data onto a stack as you recurse, but then remove them as you backtrack  
**재귀 알고리즘**에서 유용하게 쓰인다. 루프를 돌면서 임시데이터를 스택에 넣고, 그 후 백트래킹을 하면서 다시 스택에서 제거해야 할 때가 있다.

- **`pop()`** remove the top item from the stack
- **`push(item)`** add an item to the top of the stack
- **`peek`** return the top of the stack
- **`isEmpty()`**

```java
// Stack with Array
public class StackArray {
    int top;
    Object[] stack;

    StackArray(int capacity) {
        ptr = 0; // stack pointer
        stack = new Object[capacity];
    }

    void push(Object v) {
        if (ptr >= stack.length) {
            // handling overflow; OverflowIntStackException()
            return;
        }
        stack[ptr++] = v;
    }

    Object pop() {
        if (ptr == 0) {
            // handling underflow; EmptyIntStackException()
            return null;
        }
        return stack[--ptr];
    }

    Object peek() {
        if (ptr == 0) {
            throw new EmptyIntStackException();
        }
        return stack[ptr - 1];
    }

    boolean isEmpty() {
        return ptr == 0;
    }

    boolean isFull() {
        return ptr >= stack.length;
    }
}
```
```java
// Stack with List (linked list)
public class StackList<T> {

    private static class StackNode<T> {
        private T data;
        private StackNode<T> next;

        public StackNode<T>(T data) {
            this.data = data;
        }
    }

    private StackNode<T> top;

    void push(T item) {
        StackNode<T> t = new StackNode<T>(item);
        t.next = top;
        top = t;
    }

    T pop() {
        if (top == null) {
            // handling underflow; EmptyIntStackException()
            return null;
        }
        T item = top.data;
        top = top.next;
        return item;
    }

    Object peek() {
        if (top == null) {
            throw new EmptyIntStackException();
        }
        return top.data;
    }

    boolean isEmpty() {
        return top == null;
    }
}
```
**_파이썬_** 의 기본 리스트에서 ```append()```와 ```pop()``` 메서드를 이용하면 스택 자료구조와 동일하게 동작한다. ```append()``` 메서드는 리스트의 가장 뒤쪽에 데이터를 삽입하고, ```pop()``` 메서드는 리스트의 가장 뒤쪽에서 데이터를 꺼낸다.

## Queue 큐
큐는 **대기 줄**에 비유할 수 있다.  
나중에 온 사람일수록 나중에 들어가기 때문에 흔히 ‘공정한’ 자료구조라고 비유된다. 이러한 구조를
- **First In First Out (FIFO)** 선입선출 구조라고 한다.

**_Enqueue_**: rear에 데이터를 넣는 작업. **_O(1)_**   
**_Dequeue_**: front에서 데이터를 꺼내는 작업. 데이터를 꺼낸 다음 큐의 모든 데이 터들을 모두 맨 앞으로 옮겨야한다. **_O(n)_**

One place where queues are often used is **in breadth-first search or in implementing a cache**. In breadth-first search, for example, we used a queue to store a list of the nodes that we need to process. Each time we process a node, we add its adjacent nodes to the back of the queue. This allows us to process nodes in the order in which they are viewed.  
**BFS 너비 우선 탐색**이나 **캐쉬 구현**에 잘 쓰인다. BFS에서 처리할 노드의 리스트를 어딘가에 저장하고 싶을때, 노드를 처리할때 마다 인접 노드들을 큐에 저장한다면 순차적으로 처리가 가능해진다.

- **`remove()`** remove the first item (front) in the queue
- **`add(item)`** add an item to the end(rear) of the queue
- **`peek`** return the top(front) of the queue
- **`isEmpty()`**

자바에서의 인터페이스 구현은 다음과 같다.
![java_queue](../imgs/java_queue.png)
![java_queue_interface](../imgs/java_queue_interface.png)

```java
// queue with List (Linked list)
public class QueueList<T> {

    private static class QueueNode<T> {
        private T data;
        private QueueNode<T> next;

        public QueueNode<T>(T data) {
            this.data = data;
        }
    }

    private QueueNode<T> first;
    private QueueNode<T> last;

    void add(T item) {
        QueueNode<T> t = new QueueNode<T>(item);
        if (last != null) {
            last.next = t;
        }
        last = t;
        if (first == null) {
            first = last;
        }
    }

    T remove() {
        if (first == null) {
            // handling underflow; NoSuchElementException()
            return null;
        }
        T item = first.data;
        first = first.next;
        if (first == null) {
            last = null;
        }
        return item;
    }

    Object peek() {
        if (first == null) {
            throw new NoSuchElementException();
        }
        return first.data;
    }

    boolean isEmpty() {
        return first == null;
    }
}
```

### Ring Buffer 링 버퍼 (Zyklisches Array)
 링 버퍼는 **배열의 처음이 끝과 연결 될 수 있는 큐** 로 사이를 먼저 설정 해야 하지만 **Enqueue** 와 **Dequeue** 둘 모두 시간 복잡도는 **_O(1)_** 이다.

 ![ring_buffer](../imgs/ring_buffer.png)

```java
class QueueArray implements Queue {
    int first, last;
    Object[] queue;

    QueueArray(int capacity) {
        first = 0;
        last = 0;
        queue = new Object[capacity];
    }

    void add(Object v) {
        int next = (last + 1) % queue.length;
        if (next == first) {
            // handling overflow;
            return;
        }
        queue[last] = v;
        last = next;
    }

    Object remove() {
        if (first == last) {
            // handling underflow;
            return
        }
        Object x = queue[first];
        first = (first + 1) % queue.length;
        return x;
    }

    boolean isEmpty() {
        return first == last;
    }

    boolean isFull() {
        return (first == (last + 1) % queue.length);
    }
}
```

**파이썬** 으로 큐를 구현할 때는 ```collections``` 모듈에서 제공하는 ```deque``` 자료구조를 활용하자. ```deque```는 스택과 큐의 장점을 모두 채택한 것인데 데이터를 넣고 빼는 속도가 리스트 자료형에 비해 효율적이며 ```queue``` 라이브러리를 이용하는 것보다 더 간단하다.

![deque](../imgs/deque.jpg)
