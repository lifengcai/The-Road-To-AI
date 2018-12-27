#　题目描述   
> 定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。

# 解答

> 设置一个数据栈，一个辅助栈，辅助栈中存储的是每一步的最小值，当前状态的最小值就是辅助栈的栈顶元素，即

> - 把元素压入数据栈时，比较辅助栈栈顶元素和压入的元素的大小，如果压入的元素比栈顶元素小，那么就把压入的元素压入辅助栈；如果压入的元素比栈顶元素大，那么就把栈顶元素再次压入辅助栈；
> - 当从数据栈中弹出元素时，同时也要从辅助栈中弹出元素。


```c
class Solution {
public:
    void push(int value) {
        vstack.push(value);
        if(minstack.empty() || value < minstack.top()){
            minstack.push(value);
        }
        else{
            minstack.push(minstack.top());
        }
    }
    void pop() {
        vstack.pop();
        minstack.pop();
    }
    int top() {
        return vstack.top();
    }
    int min() {
        return minstack.top();
    }
private:
    stack<int> vstack;
    stack<int> minstack;
};
```


> 下面解法 minstack 空间小一些，不重复存储同样的数

```c
class Solution {
public:
    void push(int value) {
        vstack.push(value);
        if(minstack.empty() || value <= minstack.top()){
            minstack.push(value);
        }
    }
    void pop() {
        if(vstack.top() == minstack.top()){
            vstack.pop();
            minstack.pop();
        }
        else{
            vstack.pop();
        }
    }
    int top() {
        return vstack.top();
    }
    int min() {
        return minstack.top();
    }
private:
    stack<int> vstack;
    stack<int> minstack;
};
```