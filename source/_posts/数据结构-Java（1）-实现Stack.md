---
title: 数据结构--Java（1） 实现Stack
date: 2016-10-31 15:59:38
categories: "Data Structure"
tags:
- 学习
---
### 利用数组实现Stack ###
<!-- more -->
```java
public class ArrayStack<T> implements StackADT<T> {
    private final int DEFAULT_SIZE=2;//默认大小
    private int capacity;//栈容量
    private int size;//栈大小

    private int top;
    private Object[] array;

    public ArrayStack(){
        this.capacity = DEFAULT_SIZE;
        this.array = new Object[this.capacity];
        this.size = 0;
        System.out.println(top);
    }

    public ArrayStack(int capacity){
        this.capacity = capacity;
        this.array = new Object[this.capacity];
        this.size = 0;
    }
    @Override
    public void clear() {
        Arrays.fill(this.array,null);
        this.size = 0;
        this.top = 0;
        this.capacity = DEFAULT_SIZE;
        this.array = new Object[this.capacity];
    }

    @Override
    public boolean isEmpty() {
        return this.size == 0;
    }

    @Override
    public T peek() {
        if (isEmpty()){
            return null;
        }
        return (T) this.array[this.top-1];

    }

    @Override
    public T pop() {
        T v = (T) this.array[top-1];
        array[this.top-1] = null;
        this.top = this.top - 1;
        this.size--;
        return v;
    }

    @Override
    public void push(T v) {
        if (this.size<this.capacity){
            this.array[top] = v;
            this.size++;
            this.top++;
        }else {
            addStackCap();
            push(v);
        }
    }

    private void addStackCap() {//扩容
        this.capacity = this.capacity+DEFAULT_SIZE;
        Object[] newArray = new Object[this.capacity];
        System.arraycopy(this.array, 0, newArray, 0,this.array.length);
        Arrays.fill(array, null);//原来的数组置空
        this.array = newArray;
    }

    @Override
    public int size() {
        return this.size;
    }
    /**
     * 测试栈
     * @param args
     */
    public static void main(String[] args) {
        ArrayStack<Integer> a = new ArrayStack<Integer>();
        a.push(3);
        a.push(5);
        a.push(2);
        a.push(1);
        a.push(6);
        System.out.println("栈大小:"+a.size());
        System.out.println("栈容量:"+a.capacity);
        System.out.println("栈顶元素:"+a.peek());
        while (!a.isEmpty()){
            System.out.println(a.pop());
        }
        System.out.println("栈大小:"+a.size());
        System.out.println("栈容量:"+a.capacity);
        System.out.println("栈顶元素:"+a.peek());
        System.out.println("************");
        a.clear();
        System.out.println("栈大小:"+a.size());
        System.out.println("栈容量:"+a.capacity);
    }
}


interface StackADT<T> {
    public void clear();
    public boolean isEmpty();
    public T peek();
    public T pop();
    public void push(T v);
    public int size();
}
```

### 利用LinkedList实现Stack ###

```java
public class Stack<T> {
    private LinkedList<T> storage = new LinkedList<T>();
    /** 入栈 **/
    public void push(T v){
        storage.addFirst(v);
    }
    /** 出栈 **/
    public T pop(){
        if(isEmpty()) return null;
        return storage.removeFirst();
    }
    /** 栈为空 **/
    public boolean isEmpty() {
        return storage.isEmpty();
    }
    public String toString(){
        return storage.toString();
    }
    public void clear(){ storage.clear(); }
    public static void main(String[] args) {
        Stack stack = new Stack<String>();
        stack.push("a");
        stack.push("b");
        stack.push("c");
        System.out.println(stack.toString());
        Object obj = stack.pop();
        System.out.println(obj+"------"+stack.toString());
        obj = stack.pop();
        obj = stack.pop();
        System.out.println(obj);
    }
}
```
