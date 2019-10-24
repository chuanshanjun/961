### 一、栈(stack)、队列(Queue)、向量(vector)
### 线性表的基本概念和实现
线性表的存储结构有顺序存储和链式存储结构两种。前者被称为顺序表，后者被称为链表。
### 顺序表
顺序表就是把线性表中所有的元素按照其逻辑顺序，依次存储到从指定的存储位置开始的一块连续的存储空间，这样线性表的第一个元素的存储位置就是指定的存储位置，第i+1个的存储位置紧跟着第i个元素的位置。(类比ArrayList)
### 链表
在链表存储中，每个结点不仅包含所存元素的信息，还包含元素之间的逻辑关系的信息，如单链表中前驱结点包含后继结点(next)的地址信息，这样就可以通过前驱结点的位置找到后继结点的位置。(类比LinkedList)
### 两种存储结构的比较
#### 顺序表
* 随机访问特性，位置是确定的
* 要求占用连续的存储空间，存储分配只能预先进行，即静态分配
* 插入操作要移动多个元素
* 增: addLast O(1) addFirst() O(n) 总:O(n)
* 删: removeLast O(1) removeFirst O(n) 总:O(n)
* 改: set(index, e) O(1)
* 查: get(index) O(1) find(e) O(n)
#### 链表
* 不支持随机访问
* 结点中的存储精简利用率稍低一些
* 支持存储空间的动态分配
* 插入操作无需移动元素

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/linkedlist.png)
### 多种链表形式
#### 单链表
##### 带头结点的单链表(虚拟头节点)
头指针head 指向头结点，头指针值域不包含任何信息，从头结点的后继结点开始存储信息，头指针始终不为null，**当head->next 等于NULL的时候，链表为空**。

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/dummy-head-link.png)
##### 不带头结点的单链表
头指针head直接指向开始结点，**当head为NULL的时候，链表为空**。

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/common-link.png)

注意：不论是带有节点的链表还是不带头结点的链表。头指针都指向链表中的第一个结点，；而头结点是带头结点的链表中的第一个结点，只作为链表存在的标志。(虚拟头节点)

#### 双链表
双链表就是在单链表的结点上增添一个**指针域**，**指向当前结点的前驱(prev)**
同样，双链表也分为带头结点的双链表和不带头结点的双链表。

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/double-link.png)

#### 循环双列表 
循环双链表的构造源自双链表，即将终端结点的next指针指向链表中第一个结点，将链表中第一个结点的prev指针指向终端结点。不带头结点的循环双链表当head等于null的时候为空。

带头结点的循环双链表当head->next和heaad->prev两个指针都等于head时链表为空。

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/head-cyc-link.png)

#### 静态链表
静态链表借助一位**数组**来表示，结构体数组中的每一个结点含有两个分量：一个是数据结构元素分量data，另一个是指针分量，指示了当前结点的直接后继结点在数组中的位置。

### 链表的操作
#### 单链表的操作
##### 单链表删除结点
![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/20181025104317.png)

删除”节点30”

删除之前：”节点20” 的后继节点为”节点30”，而”节点30” 的后继节点为”节点40”。

删除之后：”节点20” 的后继节点为”节点40”。

##### 单链表增加结点
![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/20181025104505.png)

在”节点10”与”节点20”之间添加”节点15”

添加之前：”节点10” 的后继节点为”节点20”。

添加之后：”节点10” 的后继节点为”节点15”，而”节点15” 的后继节点为”节点20”。

单链表的特点是：节点的链接方向是单向的；相对于数组来说，单链表的的随机访问速度较慢，但是单链表删除/添加数据的效率很高。

#### 双链表操作
##### 双链表删除节点
![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/20181025104559.png)

删除”节点30”

删除之前：”节点20”的后继节点为”节点30”，”节点30” 的前继节点为”节点20”。

”节点30”的后继节点为”节点40”，”节点40” 的前继节点为”节点30”。

删除之后：”节点20”的后继节点为”节点40”，”节点40” 的前继节点为”节点20”。

##### 双链表添加节点
![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/20181025104726.png)

在”节点10”与”节点20”之间添加”节点15”

添加之前：”节点10”的后继节点为”节点20”，”节点20” 的前继节点为”节点10”。

添加之后：”节点10”的后继节点为”节点15”，”节点15” 的前继节点为”节点10”。

”节点15”的后继节点为”节点20”，”节点20” 的前继节点为”节点15”。

### 栈
### 栈的基本概念
* 栈是一种只能在一端进行插入或删除操作的线性表。其中允许进行插入或者删除操作的一端称为栈顶（TOP）。栈顶由一个称谓栈顶指针的位置指示器（其实就是一个变量），对于顺序栈，就是记录栈顶元素所在数组位置标号的一个整形变量，对于链式栈就是记录栈顶元素所在的结点地址的指针。另一端被称为栈底，栈底是固定不变的。
* 栈的特点，先进后出（FILO）
* 栈的存储结构，可用顺序表和链表来存储栈，分为顺序栈和链式栈。 即栈的本质上是线性表。
* 当n各元素以某种顺序进栈，并且可以在任意时刻出栈，所获得的元素排列的数目N满足函数N=1/(n+1)Cn2n
* 栈通常包括的三种操作：push、peek、pop。

push – 向栈中添加元素。

peek – 返回栈顶元素。

pop – 返回并删除栈顶元素的操作。

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/stack.png)

### 顺序栈（数组实现,从尾部插入,尾部删除,从尾部都是O(1)）
#### 顺序栈的特殊状态和操作
&emsp;1.栈空状态

&emsp;st.top==-1 有的书上规定st.top ==0为栈空条件(栈顶位置指示器-变量，赋值为0或1)

&emsp;2.栈满状态

&emsp;st.top==maxSize-1 maxSize为栈中最大元素的个数，则maxSize-1 为栈满时栈顶元素在数组中的位置

&emsp;3.非法状态（上溢和下溢）栈满继续进入栈就会出现上溢状态，栈空继续出栈就会出现下溢状态

&emsp;4.进栈操作 ++(st.top);st.data[st.top]=x;(底层数组addLat()操作，把数组尾部当作栈顶，从尾部增加)

&emsp;5.出栈操作 x=st.data[st.top];–(st.top);(底层数组removeLast()，把数组尾部当作栈顶，从尾部删除)

```java
@Override
    public void push(E e) {
        array.addLast(e);
    }

    @Override
    public E peek() {
        return array.getLast();
    }

    @Override
    public E pop() {
        return array.removeLast();
    }
```

### 链栈(链表实现,从头入,因为头插入,头删除,查头都是是O(1))
#### 链栈的特殊状态和操作
&emsp;1.栈空状态 head->next==NULL

&emsp;2.栈满状态 不存在栈满的情况

&emsp;3.元素进栈操作 node.next=head;head=node;(链表头增加元素)

&emsp;4.元素出栈操作 node.next=head;head = node;(链表头删除元素)

```java
@Override
    public void push(E e){
        list.addFirst(e);
    }

    @Override
    public E pop(){
        return list.removeFirst();
    }

    @Override
    public E peek(){
        return list.getFirst();
    }
```

### 队列
### 队列的基本概念
* 队列也是一种受限制的线性表，其显示为仅允许在表的一端进行插入，在表的另一端进行删除，可进行插入的一端是队尾，可进行删除的一头是队头。
* 队列的特点，先进先出（FIFO）
* 可用顺序表和链表来存储队列，队列按存储结构颗分为顺序队和链队两种。

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/queue.png)

### 顺序队
为了深刻体会到**循环队列这个结构优于非循环队列的地方**，我们将首先介绍数组实现的非循环队列结构。队列这种数据结构，无论你是用链表实现，还是用数组实现，它都是要有两个指针分别指向队头和队尾。在我们数组的实现方式中，用两个int型变量用于记录队头和队尾的索引。

#### 非循环的顺序队存在的问题
普通的数据队列存在的一个问题就是出队列是O(n)
![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/arrayqueueq1.png)

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/arrayqueue2.png)

#### 循环的顺序队列
我们可以在队列的头部增加front,当有入队的时候tail往后移动
![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/looparray.png)

出队(返回队首的元素，然后将队首的内容置为null)的话front往后移,这样出队也是O(1)操作
![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/loopqueue2.png)

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/loopqueue3.png)

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/loopqueue4.png)

循环队列到索引最后一位的话就不能再入队了，我们对应的解决方案是
将tail移动到队首,这样tail的真实索引方法是(tail+1)%c
我们可以认为front==tail队列为空
(tail+1)%c==front为队列满(此时可以自动扩容))
![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/loopqueue5.png)

#### 顺序循环队列的状态
* front==tail队列为空
* (tail+1)%c==front为队列满(此时可以自动扩容))
```java
@Override
    public void enqueue(E e){
        // 入队操作
        if((tail + 1) % data.length == front)
            resize(getCapacity() * 2);

        data[tail] = e;
        tail = (tail + 1) % data.length;
        size ++;
    }

    @Override
    public E dequeue(){
        // 出队操作
        if(isEmpty())
            throw new IllegalArgumentException("Cannot dequeue from an empty queue.");

        E ret = data[front];
        data[front] = null;
        front = (front + 1) % data.length;
        size --;
        if(size == getCapacity() / 4 && getCapacity() / 2 != 0)
            resize(getCapacity() / 2);
        return ret;
    }
```

### 普通链队
#### 链队的状态
* front == tail 队空状态
* 队满状态 不存在队满状态 （假设内存无限大的情况下）
```java
@Override
    public void enqueue(E e){
        if(tail == null){
            tail = new Node(e);
            head = tail;
        }
        else{
            tail.next = new Node(e);
            tail = tail.next;
        }
        size ++;
    }

    @Override
    public E dequeue(){
        if(isEmpty())
            throw new IllegalArgumentException("Cannot dequeue from an empty queue.");

        Node retNode = head;
        head = head.next;
        retNode.next = null;
        if(head == null)
            tail = null;
        size --;
        return retNode.e;
    }
```
### 循环链队
#### 循环链队的状态
* (tail + 1) % data.length == front队满状态
```java
@Override
    public void enqueue(E e){

        if((tail + 1) % data.length == front)
            resize(getCapacity() * 2);

        data[tail] = e;
        tail = (tail + 1) % data.length;
        size ++;
    }

    @Override
    public E dequeue(){

        if(isEmpty())
            throw new IllegalArgumentException("Cannot dequeue from an empty queue.");

        E ret = data[front];
        data[front] = null;
        front = (front + 1) % data.length;
        size --;
        if(size == getCapacity() / 4 && getCapacity() / 2 != 0)
            resize(getCapacity() / 2);
        return ret;
    }
```

### 向量
向量（Vector）是一个封装了动态大小数组的顺序容器（Sequence Container）。跟任意其它类型容器一样，它能够存放各种类型的对象。可以简单的认为，向量是一个能够存放任意类型的**动态数组**。

&emsp;1.顺序序列

&emsp;顺序容器中的元素按照严格的线性顺序排序。可以通过元素在序列中的位置访问对应的元素(通过索引访问)。

&emsp;2.动态数组

&emsp;支持对序列中的任意元素进行快速直接访问，甚至可以通过指针算述进行该操作。操供了在序列末尾相对快速地添加/删除元素的操作。

&emsp;3.能够感知内存分配器的（Allocator-aware）-动态扩容

&emsp;容器使用一个内存分配器对象来动态地处理它的存储需求。

&emsp;vector的扩充机制：按照容器现在容量的一倍进行增长。vector容器分配的是一块连续的内存空间，每次容器的增长，并不是在原有连续的内存空间后再进行简单的叠加，而是重新申请一块更大的新内存，并把现有容器中的元素逐个复制过去，然后销毁旧的内存。这时原有指向旧内存空
间的迭代器已经失效，所以当操作容器时，迭代器要及时更新。
```java
// 将数组空间的容量变成newCapacity大小
    private void resize(int newCapacity){

        E[] newData = (E[])new Object[newCapacity]; // 申请新的连续的内存空间
        for(int i = 0 ; i < size ; i ++) // 将原先的数据复制过去
            newData[i] = data[i];
        data = newData; // 将新的数组赋值给data
    }
```

### 抽象数据结构（ADT）
一个抽象数据结构（Abstract Data type）可以看做一些数据对象以及附加在这些对象上的操作的集合。对于栈来说，数据对象集为存储在栈内的数据元素，操作集为元素进栈，元素出栈，判断栈是否为空等操作。
```java
Stack<E>
void push(E)
E pop()
E peek() // 查看栈顶元素
int getSize()
boolean isEmpty()
```

### ADT 队列(Queue)
```java
Queue<E>
void enqueue(E)
E dequeue()
E getFront()
int getSize()
boolean isEmpty();
```
### 二、树
### 树的基本概念和术语
![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/15324886413081.jpg)
树是一种**非线性**的数据结构

他是若干结点（A,B,C…等都是结点）的集合，是由**唯一的根节点A**和**若干颗互不相交的子树**组成的。其中每一棵子树又是一棵树，也是由唯一的根结点和若干颗互不相交的子树组成的。
由此可知，树的定义是**递归**的。(有唯一根节点与互不相交的子树构成)

树的结点包含一个数据元素以及若干指向其子树的分支。

结点拥有的**子树数目**称为**结点的度**。
度为0的结点称为**叶子结点**或终端结点；

度不为0的结点称为非终端结点或**分支结点**。
除根结点之外，**分支结点**也称为**内部结点**。

树的度是树内各结点的度的**最大值**。

结点的子树的根称为该结点的**孩子**。相应地，该结点称为孩子的**双亲**。
同一个双亲的孩子之间互称为**兄弟**（Sibling）。

节点点的**祖先**(Ancestor)从根到该节点所经分支上的所有节点
例如树结构如下：给定的key为节点7，所有的祖先节点为 4,2,1。
```
          1
        /   \
      2      3
     /  \
   4     5
  /
7
```

结点的层次：结点的层次从根开始定义起，根为**第一层**，根的孩子为**第二层**。若某结点在第L层，则其子树的根就在第L+1层。其双亲在同一层的结点互为**堂兄弟**。

树中结点的最大层次称为树的**深度**或**高度**(Depth)。

* 深度：对于任意节点n,n的深度为从根到n的唯一路径长，根的深度为0；(深度：从根结点开始，往下。)
* 高度：对于任意节点n,n的高度为从n到一片树叶的最长路径长，所有树叶的高度为0；(高度：到叶子结束，“往上”。)
![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/tree_deep_height.jpg)

如果将树中结点的各子树看成从左至右是有次序的，不能互换的，则称该树为**有序树**，否则称为**无序树**。

森林是m(m>=0)棵互不相交的树的**集合**。对树中每个结点而言，其子树的集合即为森林。

可以将森林(Forests)定义为可以通过删除根节点并将根节点连接到第一级节点的边缘来获得的不相交树的集合。
![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/forest.png)

### 树的前序,中序,后序,层次序遍历
#### 前序遍历
**定义: 访问这个节点在访问这个节点的左右子树之前：所以称为前序遍历**

如果二叉树为空树，则什么都不做，否则：

1）访问根节点

2）前序遍历左子树

3）前序遍历右子树
```java
// 二分搜索树的前序遍历
    public void preOrder(){
        preOrder(root);
    }    
// 前序遍历以node为根的二分搜索树, 递归算法
    private void preOrder(Node node){
        if(node == null)
            return;

        System.out.println(node.e);
        preOrder(node.left);
        preOrder(node.right);
    }
```
#### 中序遍历
**定义: 访问这个节点在访问这个节点的左右子树之中：所以称为中序遍历**

**特殊意义:二分搜索树的中序遍历的结果是顺序的**

如果二叉树为空，则什么都不做，否则:

1) 中序遍历左子树

2) 访问根节点

3) 中序遍历右子树
```java
// 二分搜索树的中序遍历
    public void inOrder(){
        inOrder(root);
    }

    // 中序遍历以node为根的二分搜索树, 递归算法
    private void inOrder(Node node){
        if(node == null)
            return;

        inOrder(node.left);
        System.out.println(node.e);
        inOrder(node.right);
    }
```
#### 后序遍历
**定义: 访问这个节点在访问这个节点的左右子树之后：所以称为后序遍历**

如果二叉树为空，则什么都不做，否则:

1) 后序遍历左子树

2) 访问根节点

3) 后序遍历右子树
```java
// 二分搜索树的后序遍历
    public void postOrder(){
        postOrder(root);
    }

    // 后序遍历以node为根的二分搜索树, 递归算法
    private void postOrder(Node node){
        if(node == null)
            return;

        postOrder(node.left);
        postOrder(node.right);
        System.out.println(node.e);
    }
```
### 层次遍历
**定义：层序遍历的话又称为广度优先,通常不用递归，而且还需要借助额外的数据结构，队列。**
![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/bstls1.png)

如图所示为二叉树的层次遍历:

* 1 即按照箭头所示方向，按照0，1，2的层次顺序对二叉树中的各个结点访问。
* 2 要进行层次遍历需要建立一个队列，先将二叉树头结点入队列，然后出队列。
* 3 访问该结点，如果他有左子树，则将左子树的根节点入队，如果他有右子树，则将右子树的根节点入队，然后出队列。 
* 4 对出对结点访问，如此反复，直到队列为空为止。

```java
// 二分搜索树的层序遍历
    public void levelOrder(){

        if(root == null)
            return;

        Queue<Node> q = new LinkedList<>();
        q.add(root);
        while(!q.isEmpty()){
            Node cur = q.remove();
            System.out.println(cur.e);

            if(cur.left != null)
                q.add(cur.left);
            if(cur.right != null)
                q.add(cur.right);
        }
    }
```