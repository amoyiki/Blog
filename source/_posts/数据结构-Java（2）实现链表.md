---
title: 数据结构--Java（2）实现链表
date: 2016-11-07 16:34:03
categories: "Data Structure"
tags:
- 学习
---

### 单向链表 ###
<!-- more -->
```python
/**
 * Created by Administrator on 2016-11-07.
 */
public class LinkedList {
    private class Node{
        private Node next;
        private Object obj;
        public Node(Object obj){
            this.obj = obj;
        }
    }

    public Node first;
    public int pos = 0;
    public LinkedList(){
        this.first = null;
    }
    public void addFirst(Object obj){
        Node node = new Node(obj);
        node.next = this.first;
        this.first = node;

    }
    public Object delFirst() throws Exception {
        if(isEmpty()){
            throw new Exception("This LinkedList is empty!");
        }
        Node temp = this.first;
        this.first = temp.next;
        return temp.obj;
    }
    public void add(int index, Object obj) throws Exception {
        if (isEmpty()){
            throw new Exception("This LinkedList is empty!");
        }

        Node node = new Node(obj);
        Node cur = first;
        Node pre = first;
        while (index != pos){
            pre = first;
            cur = first.next;
            pos++;
        }
        node.next = cur;
        pre.next = node;
        pos = 0;
    }
    public void remove(Object obj) throws Exception {
        if (isEmpty()){
            throw new Exception("This LinkedList is empty!");
        }
        if (first.obj.equals(obj)){
            this.first = this.first.next;
        }else{
            Node pre = this.first;
            Node cur = this.first.next;
            while (cur != null){
                if (cur.obj.equals(obj)){
                    pre.next = cur.next;
                    break;
                }
                pre = cur;
                cur = cur.next;
            }
            if (cur == null){
                throw new Exception("Not Found");
            }
        }

    }

    public Node find(Object obj) throws Exception {
        if (isEmpty()){
            throw new Exception("This LinkedList is empty!");
        }
        Node cur = first;
        while(cur != null){
            if (cur.obj.equals(obj)){
                return cur;
            }
            cur = cur.next;
        }
        return null;
    }
    public boolean isEmpty(){
        return (first == null);
    }
    public void display(){
        if(first == null)
            System.out.println("empty");
        Node cur = first;
        while(cur != null){
            System.out.print(cur.obj.toString() + " -> ");
            cur = cur.next;
        }
        System.out.print("\n");
    }

    public static void main(String[] args) throws Exception {
        LinkedList ll = new LinkedList();
        ll.addFirst(4);
        ll.addFirst(3);
        ll.addFirst(2);
        ll.addFirst(1);
        ll.display();
        ll.delFirst();
        ll.display();
        ll.remove(3);
        ll.display();
        System.out.println(ll.find(1));
        System.out.println(ll.find(4).obj);
        ll.add(1,5);
        ll.display();
    }
}

```

**out**
>1 -> 2 -> 3 -> 4 -> 
>2 -> 3 -> 4 -> 
>2 -> 4 -> 
>null
>4
>2 -> 5 -> 4 -> 

