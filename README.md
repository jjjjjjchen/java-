## java-

# 基础冲刺一星期


super：
1.可以修饰方法、属性、构造器；
2.super修饰构造器， 通过 super（形参列表）;    在子类的构造器中调用父类指定的构造器。
3.调用了父类的构造器  不等于创建了父类的对象。
>任何一个类的构造器的首行，要么显示的调用本类中重载的其他的构造器   “this（形参列表）”   或    显示的调用父类中指定的构造器，用的是“super（形参列表）”   要么就是调用父类中空参的构造器

# 多态
## 多态性的表现
- 方法的重载和重写
- 子类对象多态性
## 使用的前提
- 要有继承关系
- 要有方法的重写
## 格式：`Person p = new Man();//向上转型 子类的转换成父类的`(这就是子类对象多态性)   虚拟方法调用：通过父类的引用指向子类的对象实体，当调用方法时，实际执行的是子类重写父类的方法
## 如果调用子类特有的方法，而父类中没有。 程序运行有两个状态：编译时状态、运行时状态。看左边，将此引用的对象理解为父类的类型，编译通不过  但是在运行时看右边，关注真正的对象的实体。
- 编译中P是Person类型的，编译时调用只能调用Person类型的，Man里面的结构不能调用
- 多态性只对于方法有效，对于属性没有作用
### 如果就是特么想调用：（向上转型不需要强制转换符） 向下转型，加个强转符可以转。
### 子类男人就不能强转成女人，虽然编译可以通过，但是运行不行
### instanceof 对象 instanceof 类：判断对象a是否是一个类A的实例 是的话返回true 否的话false
    >如果对象a是A类的实例，那么a也是父类的实例
```java
if (p1 instanceof Woman){
		Woman w1 = (Woman)p1;
		w1.shopping;
}
```
## 向下转型
- 需要使用强制转换符
- 为了不报错，最好在向下转型前进行一个判断：一个对象是否是一个类的实例instanceof



## 多态的作用：比如说
```java
public void show(Person p){
	
}
```
这里的形参如果没有多态的话，只能放Person的对象，但是有了多态性以后，就可以放子类的对象了。（这里本质就是 父类的引用变量指向了子类的实体）

## 属性的多态性  属性没有多态性   看左边


# java.lang.Object类 ，是所有类的根父类   这里看equals(); 方法
- 有一个空参的构造器
- `equals();`方法 判断两个引用变量的值是否相等
- 若我们需要比较两个对象的属性值都相同，需要重写equals方法，
## == : 
1. 两边基本数据类型（数据类型不一样的话，他也是就看数值的 两端数据类型可以不同 返回也可以是true）
2. 放引用数据类型  比较的是地址值
```java
String str1 = new String("AA"); //这是一个string类 创造一个字符串可以用这种方法
String str2 = new String("AA");
sysout(str1 == str2);
sysout(str1.equals(str2));//这里String类重写了equals方法 真正比较的是内容是否是一样的
//像 String类 包装类 Data类等重写了Object类的equals的方法
```
String 类重写了


# String类：
```java
String str1 = "AA";
String str2 = "AA";
String str3 = new String("AA");// String类有一个构造器
```

# toString方法
打印对象所在的类 和在 堆空间里的信息
- 当我们打印一个对象的引用时，默认的就是调用toString方法
- 当我们打印的类没有重写Object的方法时，调用的就是Object之中的   返回此对象返回的类及对应堆空间对象的首地址值。
- 但我们重写了 调用的就是子类中的重写的方法
- 重写的话，常常这样写：对象的信息重写
- eclipse有自动调用选项
- 同样的，字符串、Data、包装类、File类重写了toString方法的重写


# 包装类
## 基本数据类型到包装类
基本类型没有资格调用方法，每一个包装类对应一个包装类
重点在于 基本数据类型、包装类、String之间的转换 
```java 
//调用包装类的构造器就可以了
Integer i = new Integer(12);//就是类似于C语言中不需要字符串-去那个对应的偏移了
Integer i = new Integer(12);//而且任何类型都可以转
```
## 包装类转回到基本数据类型
调用包装类的方法就可以

## JDK5.0之后
可以自动装箱和自动拆箱 不需要new对象  不需要调函数
返回值是什么类型的 就用什么类型的

# 关键字static
可以用来修饰 属性、方法、*代码块（或者说初始化块）、*内部类
static修饰属性

#单例设计模式
单例：
1. 解决的问题使用一个类只能够创建一个对象
2. 如何实现：
## 饿汉式实现
```java

public class TestSingleton {
	//instance.getInstance();       这个是不可以的，因为TestSingleton类里面没有实例instance
	public static void main(String[] args) {
		Singleton.getInstance();
	}
	
}
//只能创建Singleton的单个实例
class Singleton{
//1.私有化构造器，只能在类的内部创建对象
	private Singleton() {
		
	}
//2.在类的内部创建一个类的实例
//3.公共方法里面的引用也必须是静态类型的
	private static Singleton instance = new Singleton();
	
	public static Singleton getInstance(){       //注意：静态的方法里面只能调静态的变量 所以累的实例也要静态的
		System.out.println("aa");
		return instance;
		
	}
}
```
## 懒汉式
```java
//   懒汉式的线程是不安全的
public class TestSingleton1 {
	public static void main(String[] args) {
		
	}
}

class Singleton1{
	private Singleton1() {
		
	}
	private static Singleton1 instance = null;  //先不new，先创建引用对象，没有开辟堆内存的空间。
	public static Singleton1 getInstance() {
		if(instance == null)
			instance = new Singleton1();
		return instance;
	}
}
```


#main方法





#非static初始化块的使用 （类的第四个成员 代码块）


初始化块只能用static修饰
分类：
1. 静态代码块：
```java
static{


}
```
- 随着类的加载而加载，所以静态代码块只加载一次
- 加载早于非静态的代码块
- 里面可以有输出语句
- 静态之间按照顺序结构执行
- 只能调用静态的，不能调用非静态的



2. 非静态代码块：
```java
{
	orderId = 1002;
	orderName = "AA";
	sysout("我是非静态代码块1");
}

{
	sysout(我是非静态代码块2);
}
```
- 可以对类的属性进行初始化操作，同时也可以使用本类中声明的方法
- 里面可以有输出语句
- 一个类中可以有多个非静态的代码块，代码块之间按照顺序结构执行。
- 每当创建一个对象时，就会执行一下非静态代码块
- 非静态代码的执行要早于构造器



# final关键字的使用
1. final修饰类，这个类不能被继承，如String类 System类 StringBuffer类
2. final修饰的方法，这个方法不能被重写Object中的
3. final修饰的属性是常量：
- 此常量在哪里赋值，不能默认初始化
- 可以显示的赋值（代码块、构造器中赋值也可以）（在方法中赋值不可以）（只要在对象构造之前初始化就可以）
- 不可以再赋值
如果一个变量用Static final,就是全局静态常量

>异常里面有finally 和 finalize

# 抽象类





