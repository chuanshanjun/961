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

**满二叉树:对整个二叉树而言除了叶子节点外，都有两个孩子节点**

### 树的前序,中序,后序,层次序遍历
**树的前、中、后序遍历，都是先"一路到底"，所以我们称为深度优先**
#### 前序遍历
**定义: 访问这个节点在访问这个节点的左右子树之前：所以称为前序遍历**

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/bstpreorderr.png)

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

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/bstinorderr.png)

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

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/bstpostorderr.png)

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

### 深度优先广度优先差异
**广度优先遍历:**
* 1 更快的找到你所要的那个元素
* 2 常用于算法设计中-最短路径
* 3 图中的深度优先与广度优先遍历

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/whorder.png)

例: 当问题发生在 2层 右子树上 如果使用深度优先的话 程序会一股脑的先将所有的左子树遍历一遍，达到真正问题发生处可能需要很多时间，但如果使用广度优先那么就只要遍历几层就可以找到了。

### 二叉树前序遍历的非递归写法
#### 前序-非递归

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/bstpreorder.png)

* 1 判断节点是否为空，为空则返回
* 2 新建一个栈
* 3 根节点入栈
* 4 根节点出栈，将其右节点与左节点入展，因为栈是先进后出的，所以入栈先入右节点
* 5 刚才压入的左节点出栈，再压入其右节点与左节点
* 6 循环上面的步骤...

```java
    // 二分搜索树的非递归前序遍历
    public void preOrderNR(){

        if(root == null)
            return;

        Stack<Node> stack = new Stack<>();
        stack.push(root);
        while(!stack.isEmpty()){
            Node cur = stack.pop();
            System.out.println(cur.e);

            if(cur.right != null)
                stack.push(cur.right);
            if(cur.left != null)
                stack.push(cur.left);
        }
    }
```
#### 中、后序-非递归实现（略）
#### 前、中、后序的递归与非递归实现差别
* 1 非递归需要额外的数据结构**栈**才能实现
* 2 非递归实现比递归实现复杂
* 3 中、后序非递归实现更复杂，实际应用不广

### 二叉树及其性质
二叉树的定义
* 1 每个结点最多只有2颗子树，即二叉树中节点的度只能为0，1，2
* 2 子树有左右顺序之分，不能颠倒。

&emsp;**性质1**

&emsp;非空二叉树上叶子结点数等于双分支结点数加1(没理解)

&emsp;**性质2**

&emsp;二叉树的第i层上最多有2^(i －1)个结点。(i>=1)

&emsp;**性质3**

&emsp;高度或深度为k的二叉树最多有2(k次)−1个结点。换句话说，满二叉树中**前k层的结点个数(前k层的总数)**为2^(k-1)

&emsp;**性质4**

&emsp;如果对一棵有n个结点的完全二叉树的结点按层序编号（从第一层到最后一层，每层从左到右），对任一结点i（1<=i<=n）有：

&emsp;1 如果i=1，则结点i是二叉树的根，无双亲；如果i>1，则其双亲是结点 ⌊ i/2 ⌋ 。

&emsp;2 如果2i>n，则结点i无左孩子（结点i为叶子结点）；否则其左孩子是结点2i 。

&emsp;3 如果2i+1>n，则结点i无右孩子；否则其右孩子是结点2i+1 。

&emsp;**性质5**

&emsp;具有n个结点的完全二叉树的深度为不大于log2n的最大整数+1 

&emsp;具有n(n>0)个结点的完全二叉树的高度为log2n

### 普通树与二叉树的转换(考点只写了这个-普通树与二叉树的转换)

#### 树转换成二叉树

树转换成二叉树的过程如下

1）将同一结点的各孩子结点用线串起来

2）将每个结点的分支从左到右除了第一个外，其余的都剪掉，整理即可得到

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/ordinarytreeconbt.jpg)

### 二叉树转换成树

二叉树转换为树是树转换为二叉树的逆过程，其步骤是：

1）若某结点的左孩子结点存在，将左孩子结点的右孩子结点、右孩子结点的右孩子结点……都作为该结点的孩子结点，将该结点与这些右孩子结点用线连接起来；

2）删除原二叉树中所有结点与其右孩子结点的连线；

3）整理（1）和（2）两步得到的树，使之结构层次分明。

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/btreeconverttree.jpg)

### 森林转换成二叉树

森林是由若干棵树组成，可以将森林中的每棵树的根结点看作是兄弟，由于每棵树都可以转换为二叉树，所以森林也可以转换为二叉树。

将森林转换为二叉树的步骤是：

1）先把每棵树转换为二叉树；

2）第一棵二叉树不动，从第二棵二叉树开始，**依次把后一棵二叉树的根结点作为前一棵二叉树的根结点的右孩子结点，用线连接起来**。当所有的二叉树连接起来后得到的二叉树就是由森林转换得到的二叉树。

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/forest2btree.jpg)

### 二叉树转换成森林

二叉树转换为森林比较简单，其步骤如下：

1）先把每个结点与右孩子结点的连线删除，得到分离的二叉树；

2）把分离后的每棵二叉树转换为树；

3）整理第（2）步得到的树，使之规范，这样得到森林。

### 树的存储结构,标准形式

**满二叉树与完全二叉树的区别**

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/treediff.png)

#### 顺序存储结构

树的顺序存储结构最简单直观的是**双亲存储结构**，用一维数组即可实现。将所有结点存到一个数组中。每个结点都有一个**数据域data**和一个**数值parent**指示其双亲在数组中存放的位置。根结点由于没有父结点，parent用-1表示。
int tree[maxSize]

树的双亲存储结构在**克鲁斯卡尔算法**中有重要应用

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/treestore.png)

#### 链式存储结构

&emsp;1 孩子存储结构

&emsp;孩子存储结构实质上就是图的邻接表存储结构

&emsp;树就是一种特殊的图，把图中的多对多关系删减成一对多关系即可的得到树

&emsp;2 孩子兄弟存储结构
&emsp; 树转换成二叉树的过程**就是变成了孩子兄弟存储结构**

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/treestore1.png)

**完全树(complete tree)的数组形式存储**
顺序存储结构最适合于**完全二叉树，用户存储一般二叉树会浪费大量的存储空间**
20版天勤 P137

### 树的应用
二叉排序树和平衡二叉树与查找关系密切，因为放到查找一章讲解

### Huffman树(最优二叉树)的定义与应用
#### Huffman树相关的概念
1）路径：是指在一棵树中，从一个节点到另一个节点之间的分支构成的通路，如从节点8到节点1的路径如下图所示：

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/15325717690810.jpg)

2）路径的长度：是指路径上的分支数目，在上图中，路径长度为2。

3）树的路径长度：是指从根到每个结点的路径长度之和。

4）带权路径长度：结点具有权值，从该结点到根之间的路径长度乘以结点的权值，就是该结点的带权路径长度。

5）树的带权路径长度：是指树中所有**叶子节点**的带权路径之和。

6 节点的权：指的是为树中的每一个节点赋予的一个非负的值，如上图中每一个节点中的值。

有了如上的概念，对于**Huffman树，其定义**为：
给定n权值作为n个叶子节点，构造一棵二叉树，若这棵二叉树的带权路径长度达到最小，则称这样的二叉树为最优二叉树，也称为Huffman树。

#### Huffman树的构建
给定n个权值，用这n个权值来构建赫夫曼树的算法描述如下：
1）将这n个权值分别看成只有根节点的n棵二叉树，将这些二叉树的集合记为F。
2）从F中选出两颗根结点的权值最小的树，作为左右子树，构建一棵新的二叉树，新的二叉树的根结点的权值为左右子结点的权值之和。
3）从F中删去a,b，加入新构建的树C
4）重复2，3步，直到F中只剩下一棵树为止，这棵树就是赫夫曼树。

![alt](https://raw.githubusercontent.com/chuanshanjun/mess/master/DataStruct/15325743576122.jpg)

对于树中节点的结构为：

```c++
struct huffman_node{
        char c; // 字符
        int weight; // 权重
        char huffman_code[LEN]; // 路径长度?
        huffman_node * left; // 左子树
        huffman_node * right; //  右子树
};
```

对于Huffman树的构建过程为：

```c++
int huffman_tree_create(huffman_node *&root, map<char, int> &word){
        char line[MAX_LINE];
        vector<huffman_node *> huffman_tree_node;

        map<char, int>::iterator it_t;
        for (it_t = word.begin(); it_t != word.end(); it_t++){
                // 为每一个节点申请空间
                huffman_node *node = (huffman_node *)malloc(sizeof(huffman_node));
                node->c = it_t->first;
                node->weight = it_t->second;
                node->left = NULL;
                node->right = NULL;
                huffman_tree_node.push_back(node);
        }


        // 开始从叶节点开始构建Huffman树
        while (huffman_tree_node.size() > 0){
                // 按照weight升序排序
                sort(huffman_tree_node.begin(), huffman_tree_node.end(), sort_by_weight);
                // 取出前两个节点
                if (huffman_tree_node.size() == 1){// 只有一个根结点
                        root = huffman_tree_node[0];
                        huffman_tree_node.erase(huffman_tree_node.begin());
                }else{
                        // 取出前两个
                        huffman_node *node_1 = huffman_tree_node[0];
                        huffman_node *node_2 = huffman_tree_node[1];
                        // 删除
                        huffman_tree_node.erase(huffman_tree_node.begin());
                        huffman_tree_node.erase(huffman_tree_node.begin());
                        // 生成新的节点
                        huffman_node *node = (huffman_node *)malloc(sizeof(huffman_node));
                        node->weight = node_1->weight + node_2->weight;
                        (node_1->weight < node_2->weight)?(node->left=node_1,node->right=node_2):(node->left=node_2,node->right=node_1);
                        huffman_tree_node.push_back(node);
                }
        }

        return 0;
}
```

#### Huffman树的特点
1）权值越大的结点，距离根结点越近。

2）树中没有度为1的结点，这类树又叫做正则（严格）二叉树。

3）树的带权路径长度最短

### Huffman树应用
#### Huffman编码
常见的.zip压缩文件和.jpeg图片文件的底层技术都用到了赫夫曼编码。

例如字符串S=AAABBACCCDEEA

| A   | B   | C   | D   | E  |
| ------ | ------ | ------ | ------ | ------ |
| 5次 | 2次 | 3次 | 1次 | 2次 |

以出现的次数为权值，构建一个赫夫曼树，对每个结点的左右分支进行编号，左0右1，从根到每个结点的路径的数字序列即为每个字符的编码，对A~E的赫夫曼编码规则

以出现的次数为权值，构建一个赫夫曼树，对每个结点的左右分支进行编号，左0右1，从根到每个结点的路径的数字序列即为每个字符的编码，对A~E的赫夫曼编码规则

| A   | B   | C   | D   | E  |
| ------ | ------ | ------ | ------ | ------ |
| 0 | 110 | 10 | 1110 | 1111 |

则H(S)=00011011001010101110111111110
上述有赫夫曼树导出每个字符的编码，进而得到整个字符串的编码的过程称为赫夫曼编码。
**在前缀码中，任一字符的编码串都不是另一字符编码串的前缀，赫夫曼编码产生的是最短前缀码**。

### 赫夫曼n叉树
赫夫曼二叉树是赫夫曼n叉树的一种特例，当对于结点数目大于等于2的待处理序列，都可以构造赫夫曼二叉树，但却不一定能构建赫夫曼n叉树，当无法构建时。需要补上权值为0的结点让整个序列凑成可以构造赫夫曼n叉树的序列。

### 三、查找(search)
#### 查找的基本概念
查找的定义：给定一个K值，在含有N个记录的表中找出关键字等于K的记录。若找到，则查找成功，返回该记录的信息或者该记录在表中的位置；否则查找失败，返回相关的指示记录。
由于查找算法的基本操作是关键字的比较，并且关键字比较次数与待查找关键字有关（对于一个查找表来说，对其中不同的关键字查找，关键字比较的次数一般不同），因此通常把查找过程中对关键字的平均比较次数作为衡量一个算法优劣的标准，平均查找长度用ASL来表示。

#### 对线性关系结构的查找

#### 顺序查找
基本思路：从表的一端开始，顺序扫描线性表，一次将扫描到的关键字和给定的K值比较。
顺序查找法对于顺序表和链表都是适用的，对于顺序表，可以通过数组下标递增来顺序扫描数组中的各个元素；对于链表，则可以通过表结点指针反复执行p=p->next来扫描表中的各个元素。
```java
int Search(int a[], int n ,int t){
    int i;
    for (int i = 1; i <=n; ++i) {
        if(a[i]==k)
            return i;
        return 0;
    }
}
```

```java
// 获得链表的第index(0-based)个位置的元素
    // 在链表中不是一个常用的操作，练习用：）
    public E get(int index){

        if(index < 0 || index >= size)
            throw new IllegalArgumentException("Get failed. Illegal index.");

        Node cur = dummyHead.next;
        for(int i = 0 ; i < index ; i ++)
            cur = cur.next;
        return cur.e;
    }
```

#### 二分查找
基本思路：

&emsp; 1 首先确定整个查找区间的中间位置 mid = （ left + right ）/ 2

&emsp; 2 用待查关键字值与中间位置的关键字值进行比较；

&emsp; 若相等，则查找成功

&emsp; 若大于，则在后（右）半个区域继续进行折半查找

&emsp; 若小于，则在前（左）半个区域继续进行折半查找

&emsp; 3 对确定的缩小区域再按折半公式，重复上述步骤。

二分查找必须要求

1.存储在数组中

2.有序排列

时间复杂度O(logn)

### Hash查找法:(看书和复习手册)

### BST树
#### BST树定义及特性 略
#### BST树 ADT
```java
public class BST<E extends Comparable<E>> {
    // 根节点
    private Node root;
    // 树的容量
    private int size;

    private class Node {
        public E e;
        public Node left, right;

        public Node(E e) {
            this.e = e;
            left = null;
            right = null;
        }
    }

    public BST(){
        root = null;
        size = 0;
    }
}
```

#### BST树查找
```java
// 看二分搜索树中是否包含元素e
    public boolean contains(E e){
        return contains(root, e);
    }

    // 看以node为根的二分搜索树中是否包含元素e, 递归算法
    private boolean contains(Node node, E e){
        // 查找不到返回false
        if(node == null)
            return false;
        // 比较相等则返回true
        if(e.compareTo(node.e) == 0)
            return true;
        // 如果比节点小则进入左子树    
        else if(e.compareTo(node.e) < 0)
            return contains(node.left, e);
        else // e.compareTo(node.e) > 0
            return contains(node.right, e);
    }
```

#### BST树插入
```java
// 向以node为根的二分搜索树中插入元素e，递归算法
    // 返回插入新节点后二分搜索树的根
    private Node add(Node node, E e){
        // node存在则插入成功
        if(node == null){
            size ++;
            return new Node(e);
        }
        // 比节点小则转入左子树
        if(e.compareTo(node.e) < 0)
            node.left = add(node.left, e);
        else if(e.compareTo(node.e) > 0)
            node.right = add(node.right, e);

        return node;
    }
```

#### BST查找最小值也最大值
```java
// 一直查找最左端的点直到找不到为止
// 寻找二分搜索树的最小元素
    public E minimum(){
        if(size == 0)
            throw new IllegalArgumentException("BST is empty");

        Node minNode = minimum(root);
        return minNode.e;
    }

    // 返回以node为根的二分搜索树的最小值所在的节点
    private Node minimum(Node node){
        if( node.left == null )
            return node;

        return minimum(node.left);
    }
```

#### BST树删除
```java

```