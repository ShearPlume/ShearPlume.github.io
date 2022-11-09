---
title: DB lab SQL1
date: 2022-11-09 00:15:19
tags:
- DB
- lab
---

#### basic task：

1.使用远程桌面找到自己的数据库：

![image-20221109002104565](DB-lab-SQL1/image-20221109002104565.png)

2.使用脚本新建表：

![image-20221109002223093](DB-lab-SQL1/image-20221109002223093.png)

![image-20221109002142329](DB-lab-SQL1/image-20221109002142329.png)

3.使用脚本插入元组：

![image-20221109002211779](DB-lab-SQL1/image-20221109002211779.png)

4.测试提取：

![image-20221109002256486](DB-lab-SQL1/image-20221109002256486.png)

#### extra task：

##### 创建employee 和department表

![image-20221109005616419](DB-lab-SQL1/image-20221109005616419.png)

##### 创建dep的代码：

```sql
CREATE TABLE DEPARTMENT(
	DNUMBER INT NOT NULL PRIMARY KEY,
	DNAME VARCHAR (20) UNIQUE,
	MGR_SSN INT,
	FOREIGN KEY(MGR_SSN) REFERENCES EMPLOYEE(SSN)	
);
```

注意因为外键只能是表级约束，所以只能在随后单独写，不用像soultion一样非得加CONSTRAINT关键字和约束名，直接写就行

![image-20221109005708895](DB-lab-SQL1/image-20221109005708895.png)

##### 添加参照完整性约束：

给员工表的外键DNO添加级联参照约束：

```sql
ALTER TABLE EMPLOYEE 
	ADD CONSTRAINT EMP_FK2 
	FOREIGN KEY (DNO) REFERENCES DEPARTMENT(DNUMBER) 
	ON UPDATE CASCADE;
```

之后再修改dep中的research部门和dev部门的DNUMBER（分别从1改到100和从2改到200），这样他们的员工的外键DNO也会随之而变：

![image-20221109013155644](DB-lab-SQL1/image-20221109013155644.png)
