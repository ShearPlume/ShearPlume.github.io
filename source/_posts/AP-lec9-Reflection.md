---
title: AP lec9_Reflection
date: 2023-03-08 13:14:06
tags:
---

## Reflection

### 1.定义

 JAVA反射机制是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法和属性；这种动态获取的信息以及动态调用对象的法的功能称为java语言的反射机制

**反射就是把java类中的各种成分映射成一个个的Java对象**。
    例如：一个类有：成员变量、方法、构造方法、包等等信息，利用反射技术可以对一个类进行解剖，把一个个组成部分映射成一个个对象。（其实：一个类中这些成员方法、构造方法、在加入类中都有一个类来描述）

### 2.反射API

#### 2.1 获取类对应的字节码的对象（三种）

1.调用某个类的对象的getClass()方法，即：对象.getClass()；

```java
Person p1 = new Person();
Class clazz2 = p1.getClass();
```

**注意：**此处使用的是Object类中的getClass()方法，因为所有类都继承Object类，所以调用Object类中的getClass()方法来获取。

2.调用类的class属性类获取该类对应的Class对象，即：类名.class

```java
Class<Person> clazz = Person.class;
```

3.使用Class类中的forName()静态方法（最安全，性能最好）即：Class.forName(“类的全路径”)

```java
ClassLoader classLoader = PersonTest.class.getClassLoader();
Class clazz4 = classLoader.loadClass("com.emhum.demo.Person");
```

​		三种方式常用第三种，第一种对象都有了还要反射干什么。第二种需要导入类的包，依赖太强，不导包就抛编译错误。

#### 2.2常用方法

​			当我们获得了想要操作的类的Class对象后，可以通过Class类中的方法获取和查看该类中的方法和属性。

```java

//获取包名、类名
clazz.getPackage().getName()//包名
clazz.getSimpleName()//类名
clazz.getName()//完整类名
 
//获取成员变量定义信息
getFields()//获取所有公开的成员变量,包括继承变量
getDeclaredFields()//获取本类定义的成员变量,包括私有,但不包括继承的变量
getField(变量名)
getDeclaredField(变量名)
 
//获取构造方法定义信息
getConstructor(参数类型列表)//获取公开的构造方法
getConstructors()//获取所有的公开的构造方法
getDeclaredConstructors()//获取所有的构造方法,包括私有
getDeclaredConstructor(int.class,String.class)
 
//获取方法定义信息
getMethods()//获取所有可见的方法,包括继承的方法
getMethod(方法名,参数类型列表)
getDeclaredMethods()//获取本类定义的的方法,包括私有,不包括继承的方法
getDeclaredMethod(方法名,int.class,String.class)
 
//反射新建实例
clazz.newInstance();//执行无参构造创建对象
clazz.newInstance(222,"韦小宝");//执行有参构造创建对象
clazz.getConstructor(int.class,String.class)//获取构造方法
 
//反射调用成员变量
clazz.getDeclaredField(变量名);//获取变量
clazz.setAccessible(true);//使私有成员允许访问
f.set(实例,值);//为指定实例的变量赋值,静态变量,第一参数给null
f.get(实例);//访问指定实例变量的值,静态变量,第一参数给null
 
//反射调用成员方法
Method m = Clazz.getDeclaredMethod(方法名,参数类型列表);
m.setAccessible(true);//使私有方法允许被调用
m.invoke(实例,参数数据);//让指定实例来执行该方法
```

