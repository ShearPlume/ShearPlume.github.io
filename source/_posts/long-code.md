---
title: long code
date: 2023-04-26 19:29:24
tags:
---

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

