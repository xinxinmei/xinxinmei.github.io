## java对列和栈的实现
### 队列
**队列遵守先进先出的原则FIFO**
* 循环数组实现
   首先定义head和tail，为了实现循环在每次进出后对于head和tail的处理采用（head+1）%sizemax以达成循环的目的
   定义数组和add和poll的方法

```
   class CircleArrayQueue<E>{
   public CircleArrayQueue(int size){}
   public void add(E element){}
   public E poll(){}
   private Object[] array ;
   private int head;
   private int tail;
   private int size;

}

```
* 链式存储实现
   在队列内定义一个节点类，节点类含有值和next，在方法中为了实现FIFO，在出队列时释放节点类实例化head对象，进队列时则通过节点类的实例化tail对象添加。
   
```
class LinkQueue<E>{
	public void add(E element){
		if(this.head==null){
			Node head = new Node<e>(element,null);
			head=tail;
		}
		else{
			Node<E> temp = new Node<E>(element,null);
			this.tail.next = temp;
			tail = temp;
		}
	}
	public Node<E> poll(){
		if(this.head==null && this.head.next==null)
			return null;
		else{
			Node <E> temp ;					//保存头节点
			temp = this.head;
			this.head = this.head.next;		//将头节点指向下一个节点
			temp.next = null;	//释放head
			return temp;
		}
	}
	class Node<E>{
		E node;
		Node<E> next;
		public Node(E value,Node n){
			this.node = value;
			this.next = n;
		}
	}
	private Node head;
	private Node tail;
}
```
   
* LinkList实现
   直接使用Queue类和LinkList类实现
   

### 栈
**栈遵守先进后出的原则LIFO**
* 数组实现
   定义top=-1，进栈则加一，出栈则减一。
```
class ArrayStack<E>{
	public ArrayStack(int size){}
	public E push(E element){}
	public E poll(){}
	private Object[] element;
	private int top;
	private int size;
}
```

* 链式存储实现
   定义节点类，top指向栈顶即可。
   
```
class LinkStack<E>{
	class Node<E>{
		private E value;
		private Node<E> next;
		public Node(E e, Node<E> next){
			this.value =e;
			this.next = next;
		}
	}
	public void push(E element ){
		if(top==null){
			this.top = new Node<E>(element,null);
		}else[
			Node<E> temp = new Node<E>(element,top);
			top=temp;
		}
	public Node<E> poll(){
		if(top==null)
			return null;
		else{
			Node<E> temp = top;
			top = top.next;
			temp.next =null;
			return temp;
		}
	}
	private Note<E> top;
}

```
   
* LinkList实现
   利用LinkList类的方法实现。
   
### 小结
**在使用链式存储结构的时候，释放一个节点的时候，将原有的top或者head指向next节点并将值保存到temp当中，将temp.next=null释放即可**
*传入参数后首相判空，然后实例化节点类对象（next为空），在进行插入操作*
 