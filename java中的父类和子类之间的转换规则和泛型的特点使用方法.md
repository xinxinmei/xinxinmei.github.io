### java中的父类和子类之间的转换规则：

* 子类转换成父类没有什么要求，直接赋值即可: eg: father f= new son()

* 父类转换成子类的话需要使用强制转换 ： eg： son s = (son) f ;

  子类继承父类的非私有的的方法和属性，子类可以覆写父类的方法，子类可以有自己的属性和方法，**所以子类的实例是一个父类的实例，而父类的一个实例不一定是子类的实例。**

  注意在进行父类转换成子类的过程中，可以先用instanceOf（）方法判断一下父类是否是子类的实例。



### 泛型的使用

*错误：创建泛型数组*

* 泛型的使用

  泛型方法：public static <E> void main( E   element)

  限定上界：public static <T extends 类名<T>> T 方法名（）或者是,<T implements 接口名<T>>

  泛型类：class 类名<E>

  类型通配符： List<？>，？可以是String Integer等

  

