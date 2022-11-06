---
title: Java File IO
date: 2022-11-05 19:02:14
tags:
- course
- java
---

#### File类

是文件和目录路径名的抽象表示



#### 路径

**相对路径**

..(当前路径的上一级路径) 和 . (当前路径) 表示的就是相对路径,需要注意的是相对路径要有参考(自身)

以当前文件为基准进行一级级目录指向被引用的资源文件。在 Java 代码中以当前运行的代码所在的位置为参照位置，只要被引用的文件相对于引用的文件的位置不变就可以被读取到。一旦改变相对位置就无法被读取到。

例子："./666/forwards.txt"

**绝对路径**

文件在文件系统中真正存在的路径，是指从硬盘的根目录(**Windows**为盘符)开始，进行一级级目录指向文件（从根目录一层层读写）。绝对路径顾名思义就是绝对的地址，就像你只要告诉别人你家的门牌号，他就能找到你家。而不是相对位置你告诉他在老王家的隔壁一样。

目录与目录之间用 \ 表示,,也可以用 / ,形如D:xxxxxx的就是绝对路径，windows因为转义字符所以要输两次\，即\\

例子：”C:\Users\Admin\Documents\Java Files\666\forwards.txt“



#### 读取

使用new FileReader(path)时，会出现检查异常FileNotFoundException，必须throws 异常

```java
	static FileReader fr = null;

public static void lab2(Scanner sc) {
        
        try {
            fr = new FileReader("./666/sums.txt");
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
        while (sc.hasNextLine()) {
            // get the next line
            int out = 0;
            String line = sc.nextLine();
            Scanner temp = new Scanner(line);
            int int1 = temp.nextInt();
            String cacu = temp.next();
            int int2 = Integer.parseInt(temp.next());
            if (cacu.equals("+"))
                out = int1 + int2;
            else if (cacu.equals("-"))
                out = int1 - int2;

            System.out.println(out);
            System.out.println(line);
        }
    }

```

#### 写入

使用new FileReader(path)或new FileWriter(path)时，会出现检查异常FileNotFoundException,必须try catch 异常

使用 fr.read();时会出现检查异常IOException，必须try catch 异常,close()也一样

fw = new FileWriter(path);

BufferedWriter bw =new BufferedWriter(fw);

bw.write("any thing");

bw.flush();（刷新写入）

bw.close();（关闭，并在关闭前执行flush）

```java
public static void lab3() {
        FileReader fr = null;     
        try {
            fr = new FileReader("./666/backwards.txt");
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
        Scanner sc = new Scanner(fr);
        FileWriter fw=null;
        try {
            fw = new FileWriter("./666/forwards.txt");
        } catch (IOException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
        BufferedWriter bw =new BufferedWriter(fw);
        int index = 0;
        char[] buffer=new char[500];
        char temp;
        while (true) {
            try {
                int ifend=  fr.read();
                if(ifend==-1)
                break;
                else
                {
                    temp=(char)ifend;
                    buffer[index++]=temp;
                }

            } catch (IOException e) {
            }      
        }
        char[] fin=new char[index]; 
        System.arraycopy(buffer,0,fin,0,index);

        for(int i=0;i<fin.length;i++)
        {
            try {
                bw.write(fin[fin.length-i-1]);
                // bw.flush();
            } catch (IOException e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
            }
        }
        try {
            bw.close();
        } catch (IOException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
    }
```

