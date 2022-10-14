---
title: 10.6 DB lab
date: 2022-10-06 12:17:16
tags:
---

#### Task1:

![image-20221006121832305](10-6-DB-lab/image-20221006121832305.png)

![image-20221006123418182](10-6-DB-lab/image-20221006123418182.png)

#### Task2:

#### Task3:

##### 3.1:

![image-20221006121957944](10-6-DB-lab/image-20221006121957944.png)

![image-20221006123830526](10-6-DB-lab/image-20221006123830526.png)

##### 3.2:

![image-20221006123855872](10-6-DB-lab/image-20221006123855872.png)

only works will be affected

##### 3.3:

![image-20221006124120665](10-6-DB-lab/image-20221006124120665.png)

![image-20221006124352870](10-6-DB-lab/image-20221006124352870.png)

##### 3.4:

![image-20221006124417383](10-6-DB-lab/image-20221006124417383.png)

![image-20221006124716758](10-6-DB-lab/image-20221006124716758.png)

##### 3.5:

![image-20221006124800707](10-6-DB-lab/image-20221006124800707.png)

![image-20221006124810063](10-6-DB-lab/image-20221006124810063.png)

No, primary key must uniquely identify a entity, although in this figure the names seem to be different, we can not assume it would be the same if we introduce new entities.

##### 3.6:

![image-20221006141713808](10-6-DB-lab/image-20221006141713808.png)

![cd](10-6-DB-lab/无标题1.png)

### 疑惑解答：

1.一对多转关系模式时，外键的设置应是1指向多而不是反过来，例子：dog中设置一个kennel name指向kennel而不是kennel的dog id指向dog（多个dogs share a kennel）

2.转关系模式时，如果一个实体的属性很少，不够外键时，有两种方法：1：用关系中其他实体的属性组合产生其外键。2：创造新的实体，例子：dog中attendence可以创造一个attendence id充当其主键也可以用dog id，show name和opendate组合产生其主键he（课上用的是后者，但二者都合理）
