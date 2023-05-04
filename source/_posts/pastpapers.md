---
title: pastpapers
date: 2023-04-26 03:02:01
tags:
---

## SEpaper2020

### 1a

？

### 1b

异常可以用来以安全的方式设计类，它提供了一种结构化的方式来处理错误和特殊情况，即使在出现意外事件或条件时也能确保类的正常运行,因为有时fail比产生错误的数据更能让人接受

other 3:

• Data Hiding

数据隐藏，，是指将一个类的内部状态从外部实体中隐藏起来，只通过明确定义的接口或方法提供访问。这种方法通过防止未经授权的修改或不一致的更新来帮助保持一个对象状态的一致性。

好处：

保护对象的内部状态不被未经授权的访问或修改

使得维护和更新代码更加容易，因为对内部实现的改变不会影响外部接口

• Atomic Operations 

 原子操作是指完全完成或根本不执行的操作，确保一个对象的状态保持一致，即使在操作过程中发生错误或异常情况。换句话说就是不将时序耦合暴露在类之外，防止调用类时因未调用全部操作而产生错误

好处：
确保对象状态的一致性和有效性，即使在出现错误或特殊情况下也是如此
简化了错误处理，因为它消除了在发生错误时手动跟踪和撤销部分修改的需要



• Explicit Constructors 

使用显示构造函数，每次初始化对象的时候都将对象所需要初始化的全部属性初始化，这确保了只有有效的对象被创建，减少了在对象的生命周期中出现错误或意外行为的可能性。

好处：
确保只有有效的对象被创建，减少错误或意外行为的可能性

### 1c

一个网络由一些用链接连接起来的节点组成。实际的网络结构是动态的，因为节点可以下线和被添加，两个节点之间的连接也可以建立和断开。说明如何以安全的方式将这个网络建模为Node对象和Link对象的集合，以及适当的方法。要做到这一点，你应该定义不变量，并解释如何使用你选择的方法以安全的方式添加和删除节点和链接。该系统的一个要求是，给定一个Node对象，总是可以找到与该节点相连的所有链接，并且每个Link对象可以返回它所连接的Nodes。

不变量：

1.一个link最多链接两个节点，不能设置成public（**数据隐藏**）

2.删除一个节点，其余与这个节点链接的节点的link也会被删除(**原子操作**)

3.创建link时，同时要创建它的俩node（**显式构造函数**）

4.删除节点时要handle删除link失败的error情况（**Exceptions**）    

```java
public class Node
{
    private List<Link> links;//（**数据隐藏**）
    public Node()
    {
        links=new ArrayList<Link>();//（**显式构造函数**）
    }
    public void addlink(Node n)
    {
        for (Link link : links) {
            if(link.getNode()[0]==n)
            return;//(**原子操作**)
        }    
        Link l1=new Link(this,n);
        links.add(l1);
        n.addlink(this);        
    }
    public List<Link> getLinks()
    {
        return links;//（**数据隐藏**）
    }
    
}

public class Link
{
    //static int nodesNum=2;
    private Node[] nodes;
    public Link(Node n1,Node n2)
    {
        nodes=new Node[2];//(**原子操作**)（**显式构造函数**）
        nodes[0]=n1;
        nodes[1]=n2;
    }
    public Node[]getNode()
    {
        return nodes;//（**数据隐藏**）
    }    
}
```



### 2a

### 2b

借助于一个例子，解释一下继承可以被用来为使用接口的抽象行为建模的机制。这种方法的好处是什么？



### 2d

### 2e

### 3a

### 3b 



### long code

我们提供了一个简化的考试报告和抄袭检查工具的Java实现，旨在输出一份关于考试的报告：例如，如何调整额外时间的权重和任何可疑的抄袭行为。为了节省空间，这个实现是局部的，你应该假设以后会提供缺失的功能，例如，有一种方法可以将提交的内容添加到考试中。

#### Exam

```java
import java.util.ArrayList;

public class Exam {
    public String name;
    public ArrayList<ExamScript> submissions;//不符合安全类原则之数据隐藏

    // Date of exam
    public int day;
    public int month;
    public int year;

    public Exam(String name) {
        this.name = name;
        submissions = new ArrayList();
    }

    public Exam(String name, int day, int month, int year) {
        this.name = name;//不符合安全类原则之显式构造函数应构造全部属性的原则，可能会破坏所有的exam都有submission这一不变量
        this.day = day;
        this.month = month;
        this.year = year;
    }

    public ArrayList<ExamScript> getSubmissions() {
        return submissions;
    }
}
```

#### ExamScript

```java
import java.sql.Time;

public class ExamScript {
    public Student student;//不符合安全类原则之数据隐藏
    public String answer;
    public Time timeTaken;

    public ExamScript(Student student, String answer, Time timeTaken) {
        this.student = student;
        this.answer = answer;
        this.timeTaken = timeTaken;
    }
}
```

#### ReportGenerator

```java
public class ReportGenerator {
    protected String title;
    public boolean writeHTML;

    public ReportGenerator(boolean shouldWriteHTML) {
        writeHTML = shouldWriteHTML;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public boolean isSimilar(ExamScript s1, ExamScript s2) {//stamp 耦合，只需要传answer就行了
        // Implementation hidden
        return false; 
    }

    // Must be called before printContent
    public void printTitle() {
        String report = "";
        if (writeHTML) {//控制耦合
            report += String.format("<h1>%s</h1>\n", title);//万一没有set title会报错，应该有exception
        } else {
            report += String.format("%s\n", title);
        }
        System.out.println(report);
    }

    // printTitle should always be called before printContent
    public void printContent(Exam e) {//破坏了原子操作，应该把title和content一起打印
        String report = "";
        if (writeHTML) {//控制耦合
            report += String.format("<h1>Exam Report for exam %s</h1>\n",
                    e.name);
            for (ExamScript s : e.submissions) {
                boolean isSimilarToAny = false;
                for (ExamScript s2 : e.submissions) {
                    isSimilarToAny = isSimilar(s, s2) || isSimilarToAny;
                }
                report += String.format("<li>%s | %s | %s</li>\n",
                        s.student, s.timeTaken.toString(),
                        isSimilarToAny);
                // More reporting, unshown
            }
        } else {
            report += String.format("Exam Report for exam %s\n", e.name);
            for (ExamScript s : e.submissions) {
                boolean isSimilarToAny = false;
                for (ExamScript s2 : e.submissions) {
                    isSimilarToAny = isSimilar(s, s2) || isSimilarToAny;
                }
                    report += String.format("%s, %s, %s\n",
                            s.student, s.timeTaken.toString(),//stamp耦合？需要传整个student吗
                            isSimilarToAny);
                // More reporting, unshown
            }
        }
        System.out.println(report);
    }
}
```

#### Student

```java
public class Student {
    private int guid;
    public boolean hasExtraTime;

    public Student(int guid) { this.guid = guid; }
    public void setExtraTime() { hasExtraTime = true; }
}
```

