# MyStack

```java
import java.util.Stack;

/**
 * 题目
 * 实现一个特殊的栈，在实现栈的基本功能上，再实现返回栈中最小元素的操作
 * 思路：
 * 用两个栈，stackData保存数据，stackMini保存最小值
 */
public class MyStack {

    private Stack<Integer> stackData;
    private Stack<Integer> stackMini;

    public MyStack() {
        stackData = new Stack<>();
        stackMini = new Stack<>();
    }

    public void push(int newNum) {
        stackData.push(newNum);
        if (stackMini.empty()) {
            stackMini.push(newNum);
        } else if (newNum >= stackMini.peek()) {
            //如果这个数比最小值大，那么压入最小值
            stackMini.push(stackMini.peek());
        } else {
            //如果这个数比最小值小，压入这个数
            stackMini.push(newNum);
        }
    }

    public int pop() {
        if (stackData.empty()) {
            throw new RuntimeException("Your stack is empty");
        }
        stackMini.pop();
        return stackData.pop();
    }

    public int getMini() {
        if (stackMini.empty()) {
            throw new RuntimeException("Your stack is empty");
        }
        return stackMini.peek();
    }
}
```