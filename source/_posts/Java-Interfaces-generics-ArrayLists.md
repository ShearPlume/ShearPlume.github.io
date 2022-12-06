---
title: Java Interfaces, generics, ArrayLists
date: 2022-11-21 15:09:29
tags:
- java
- course
---

### 接口

继承了接口的类只能用接口的方法，不能用自己的或者父类的（如果有继承）（即所有方法都必须必须覆盖或实现一个超类型方法）

![image-20221121163830589](Java-Interfaces-generics-ArrayLists/image-20221121163830589.png)

继承和接口同时存在时，先继承再接口：

![image-20221121161105838](Java-Interfaces-generics-ArrayLists/image-20221121161105838.png)

接口与Swing：

当用户在Swing GUI中做某事时（例如，点击一个 按钮）就会创建一个ActionEvent（由Swing自动创建）。
ActionEvents被称为actionPerformed的方法所处理。actionPerformed是ActionListener接口内的方法
如果你想在按钮被按下时发生一些事情，你需要给按钮分配一个具有actionPerformed方法的对象。
ActionListener是定义actionPerformed的接口。
任何实现ActionListener的类都可以被指定为任何组件的监听器。

```java
package Interface;
import java.awt.*;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;
import javax.swing.JTextField;
import java.awt.event.*;

public class Addaction extends JFrame implements ActionListener {
    JTextField text;
    JButton press;
    public Addaction() {
    this.setSize(200,200);
    this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    JPanel panel = new JPanel(new FlowLayout());
    text = new JTextField("Not pressed yet");
    panel.add(text);
    press = new JButton("Press me");
    press.addActionListener(this);
    panel.add(press);
    this.add(panel);
    this.setVisible(true);
    }
    @Override
    public void actionPerformed(ActionEvent e) {
        text.setText("Pressed!");
    }
    public static void main(String[] args) { new Addaction();}
    }
    
```

总结：
接口通过一系列的方法描述某种功能
实现了接口的类产生的对象可以被存储在接口类型的引用中

### 泛型 Generics

#### 引子：

在接口章节中，我们使用了学生类和汽车类来实现了接口Comparable，并改写了其函数CompareTo，注意因为CompareTo函数的形参签名是Object，所以改写函数的第一步是判断传进来的Object是不是学生或者汽车类，这很笨拙，而泛型则解决了这一问题。

#### 泛型的由来

根据《Java编程思想》中的描述，泛型出现的动机：

有很多原因促成了泛型的出现，而最引人注意的一个原因，就是为了创建容器类。

#### 概述

泛型的本质就是"参数化类型"。一提到参数，最熟悉的就是定义方法的时候需要形参，调用方法的时候，需要传递实参。那"参数化类型"就是将原来具体的类型参数化

泛型的出现避免了强转的操作，在编译器完成类型转化，也就避免了运行的错误。

#### 目的

Java泛型也是一种语法糖，在编译阶段完成类型的转换的工作，避免在运行时强制类型转换而出现ClassCastException,类型转化异常。

#### 对比

不使用泛型：

```java
public static void main(String[] args) {
        List list = new ArrayList();
        list.add(11);
        list.add("ssss");
        for (int i = 0; i < list.size(); i++) {
            System.out.println((String)list.get(i));
        }
    }

```

因为list类型是Object。所以int,String类型的数据都是可以放入的，也是都可以取出的。但是上述的代码，运行的时候就会抛出类型转化异常

使用泛型：

```java
public static void main(String[] args) {
        List<String> list = new ArrayList();
        list.add("hahah");
        list.add("ssss");
        for (int i = 0; i < list.size(); i++) {
            System.out.println((String)list.get(i));
        }
    }
```

在上述的实例中，我们只能添加String类型的数据，否则编译器会报错。

#### 泛型通配符TEKV？

本质上这些个都是通配符，没啥区别，只不过是编码时的一种约定俗成的东西。比如 T ，我们可以换成 A-Z 之间的任何一个 字母都可以，并不会影响程序的正常运行，但是如果换成其他的字母代替 T ，在可读性上可能会弱一些。通常情况下，T，E，K，V，？是这样约定的。

？表示不确定的 java 类型，T (type) 表示具体的一个java类型，K V (key value) 分别代表java键值中的Key Value ，E (element) 代表Element

**Object和泛型通配符区别?**

Object是所有类的根类，是具体的一个类，使用的时候可能需要类型强制转换的，但是用通配符 ?、T 、K 、V、 E 等这些的话，在实际用之前类型就已经确定了，不需要强制转换。

### 泛型的使用

三种：泛型类，泛型方法，泛型接口

#### 泛型类

把泛型定义在类上

格式：

```java
public class 类名 <泛型类型1,...> {
    
}
```

**泛型类型==必须是引用类型==（非基本数据类型）**

#### 泛型方法

把泛型定义在方法上

格式：

```java
public <泛型类型> 返回类型 方法名（泛型类型 变量名） {
    
}
```

注意点：方法声明中定义的形参只能在该方法里使用，而接口、类声明中定义的类型形参则可以在**整个接口、类中使用**。当调用fun()方法时，根据传入的实际对象，编译器就会判断出类型形参T所代表的实际类型

```java
class Demo{  
  public <T> T fun(T t){   // 可以接收任意类型的数据  
   return t ;     // 直接把参数返回  
  }  
};  
public class GenericsDemo26{  
  public static void main(String args[]){  
    Demo d = new Demo() ; // 实例化Demo对象  
    String str = d.fun("汤姆") ; // 传递字符串  
    int i = d.fun(30) ;  // 传递数字，自动装箱  
    System.out.println(str) ; // 输出内容  
    System.out.println(i) ;  // 输出内容  
  }  
};
```



#### 泛型接口

把泛型定义在接口

格式：

```java
public interface 接口名<泛型类型> {
    
}
```

如果实现类实现泛型接口，接口未传入实际泛型时，实现类声明的时候也需要将泛型声明到类中

```java
interface IB<T> {
    T test(T t);
}
/**
 * 未传入泛型实参时，与泛型类的定义相同，在声明类的时候，需要将泛型的声明一起加到类中
 * @param <T>
 */
class B<T> implements IB<T> {
    @Override
    public T test(T t) {
        return t;
    }
}
```

如果实现接口时，接口指定了具体的数据类型，这个类实现接口中所有的方法位置都要将泛型替换至具体的数据类新

```java
/**
 * 如果实现接口时，接口指定了具体的数据类型，
 * 这个类实现接口中所有的方法位置都要将泛型替换至具体的数据类新
 */
interface IB<Integer> {
    Integer test(Integer t);
}
class B1 implements IB<Integer> {
    @Override
    public Integer test(Integer t) {
        return t;
    }
}
```

### ArrayList

ArrayList 类是一个可以动态修改的数组，与普通数组的区别就是它是没有固定大小的限制，我们可以添加或删除元素。

ArrayList 继承了 AbstractList ，并实现了 List 接口

ArrayList是泛型类所以有<>标志

ArrayList 类位于 java.util 包中，使用前需要引入它，语法格式如下：

```java
import java.util.ArrayList; // 引入 ArrayList 类

ArrayList<E> objectName =new ArrayList<>();　 // 初始化
```

**E**: 泛型数据类型，用于设置 objectName 的数据类型，**只能为引用数据类型**。

**objectName**: 对象名。

ArrayList 是一个数组队列，提供了相关的添加、删除、修改、遍历等功能。

#### 添加元素到 ArrayList 可以使用 add() 方法:

```java
import java.util.ArrayList;

public class RunoobTest {
    public static void main(String[] args) {
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        System.out.println(sites);
    }
}
//输出：[Google, Runoob, Taobao, Weibo]
```

#### 访问 ArrayList 中的元素可以使用 get() 方法：

```java
import java.util.ArrayList;

public class RunoobTest {
    public static void main(String[] args) {
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        System.out.println(sites.get(1));  // 访问第二个元素
    }
}
//输出：Runoob
```

#### 如果要修改 ArrayList 中的元素可以使用 set() 方法：

```java
import java.util.ArrayList;

public class RunoobTest {
    public static void main(String[] args) {
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        sites.set(2, "Wiki"); // 第一个参数为索引位置，第二个为要修改的值
        System.out.println(sites);
    }
}
//输出：[Google, Runoob, Wiki, Weibo]
```

#### 如果要删除 ArrayList 中的元素可以使用 remove() 方法：

```java
import java.util.ArrayList;

public class RunoobTest {
    public static void main(String[] args) {
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        sites.remove(3); // 删除第四个元素
        System.out.println(sites);
    }
}
//输出：[Google, Runoob, Taobao]
```

#### 使用for-each迭代元素：

```java
import java.util.ArrayList;
 
public class JiyikTest {
     public static void main(String[] args) {
         ArrayList<String> sites = new ArrayList<String>();
         sites.add("Google");
         sites.add("Jiyik");
         sites.add("Taobao");
         sites.add("Weibo");
         for (String i : sites) {
             System.out.println(i);
         }
     }
 }
//输出：
//Google
//Jiyik
//Taobao
//Weibo
```



#### ArrayList常用方法：

| 序号 | 方法                                                         | 描述                                          |
| ---- | ------------------------------------------------------------ | --------------------------------------------- |
| 1    | [add()](https://www.jiyik.com/w/java/java-arraylist-add)     | 将元素插入到指定位置的 arraylist 中           |
| 2    | [addAll()](https://www.jiyik.com/w/java/java-arraylist-addall) | 添加集合中的所有元素到 arraylist 中           |
| 3    | [clear()](https://www.jiyik.com/w/java/java-arraylist-clear) | 删除 arraylist 中的所有元素                   |
| 4    | [clone()](https://www.jiyik.com/w/java/java-arraylist-clone) | 复制一份 arraylist                            |
| 5    | [contains()](https://www.jiyik.com/w/java/java-arraylist-contains) | 判断元素是否在 arraylist                      |
| 6    | [get()](https://www.jiyik.com/w/java/java-arraylist-get)     | 通过索引值获取 arraylist 中的元素             |
| 7    | [indexOf()](https://www.jiyik.com/w/java/java-arraylist-indexof) | 返回 arraylist 中元素的索引值                 |
| 8    | [removeAll()](https://www.jiyik.com/w/java/java-arraylist-removeall) | 删除存在于指定集合中的 arraylist 里的所有元素 |
| 9    | [remove()](https://www.jiyik.com/w/java/java-arraylist-remove) | 删除 arraylist 里的单个元素                   |
| 10   | [size()](https://www.jiyik.com/w/java/java-arraylist-size)   | 返回 arraylist 里元素数量                     |
| 11   | [isEmpty()](https://www.jiyik.com/w/java/java-arraylist-isempty) | 判断 arraylist 是否为空                       |
| 12   | [subList()](https://www.jiyik.com/w/java/java-arraylist-sublist) | 截取部分 arraylist 的元素                     |
| 13   | [set()](https://www.jiyik.com/w/java/java-arraylist-set)     | 替换 arraylist 中指定索引的元素               |
| 14   | [sort()](https://www.jiyik.com/w/java/java-arraylist-sort)   | 对 arraylist 元素进行排序                     |
| 15   | [toArray()](https://www.jiyik.com/w/java/java-arraylist-toarray) | 将 arraylist 转换为数组                       |
| 16   | [toString()](https://www.jiyik.com/w/java/java-arraylist-tostring) | 将 arraylist 转换为字符串                     |
| 17   | [ensureCapacity()](https://www.jiyik.com/w/java/java-arraylist-ensurecapacity) | 设置指定容量大小的 arraylist                  |
| 18   | [lastIndexOf()](https://www.jiyik.com/w/java/java-arraylist-lastindexof) | 返回指定元素在 arraylist 中最后一次出现的位置 |
| 19   | [retainAll()](https://www.jiyik.com/w/java/java-arraylist-retainall) | 保留 arraylist 中在指定集合中也存在的那些元素 |
| 20   | [containsAll()](https://www.jiyik.com/w/java/java-arraylist-containsall) | 查看 arraylist 是否包含指定集合中的所有元素   |
| 21   | [trimToSize()](https://www.jiyik.com/w/java/java-arraylist-trimtosize) | 将 arraylist 中的容量调整为数组中的元素个数   |
| 22   | [removeRange()](https://www.jiyik.com/w/java/java-arraylist-removerange) | 删除 arraylist 中指定索引之间存在的元素       |
| 23   | [replaceAll()](https://www.jiyik.com/w/java/java-arraylist-replaceall) | 将给定的操作内容替换掉数组中每一个元素        |
| 24   | [removeIf()](https://www.jiyik.com/w/java/java-arraylist-removeif) | 删除所有满足特定条件的 arraylist 元素         |
| 25   | [forEach()](https://www.jiyik.com/w/java/java-arraylist-foreach) | 遍历 arraylist 中每一个元素并执行特定操作     |
