# 对象的集合
### 数组
   对象数组保存的时对象的引用，基本类型数组保存的时基本类型的值。
   数组标识符只是一个引用，指向堆中的对象
   返回一个数组与返回其他对象并没有什么区别，只是在方法中定义即可。
### 比较功能
   实现java.lang.Comparable接口，接口只有一个方法：comparaTo()，如果当前小于参数则反回负值。
   Collections类中包含一个Comparator接口，可以反转自然的排序顺序。
## 容器
   容器是用来保存对象的
   **Collection**保存的的对象都服从一些规则
   **Map**保存的是一个对对象，对应着**键值**，单独的键或者值都可以转换成Collection
   list:以特定的顺序保存一组元素
   set：元素不能重复
### 容器的打印

```
import java.util.*;
public class PrintContain{
	static Collection fill(Collection c){
		c.add("a");
		c.add("b");
		return c;
	}
	static Map fill(Map m){
		m.put("1","a");
		m.put("2","b");
		return m;
	}
	public static void main(String args[]){
		ArrayList<String> a =new ArrayList<String>();
		String b[]={"A","B"};
		HashMap<String,String> c =  new HashMap<String,String>();
		
		System.out.println("容器输出"+fill(a));
		System.out.println("数组输出格式："+b);
		System.out.println("容器输出"+fill(c));
	}
}
```

结果:![picture][a]

直接打印容器可以清楚的显示内容，而数组则不行。

### 填充容器
### 容器的缺点
   当对象存入容器中时类型的信息将会丢失，因为容器只保存object的引用，object是所有类的基类。在存入对象时可以接受任何类型，当取出时需要进行类型的强制转话。类型不符合的话将会报错runtimeexception。
   *但容器对于String类有着特殊的支持，会隐式的调用toString（）方法*
```
System.out.println("nnnn"+object类型);//调用时object对象会隐式调用toString()，并不会报错！
```
	
	为了弥补这种缺点：在添加元素的过程中应该明确的指出对象的类型，返回时也应该调用强制转换。

### 迭代器
   collection对象调用Iterator()方法生成iterator对象，该对象有三个方法：
   next():返回下一个元素，第一次掉哟个返回第一个元素
   hasNext():判断下一个元素是否存在
   remove():将对象返回的元素删除
   ```
   ArrayList a = new  ArrayList();
   Iterator i = a.Iterator();
   while(i.hasNex()){
		System.out.println(i.next);
   }
   
```
   
### 容器的分类


















[a]: