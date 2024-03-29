---
title: CSD-Information-Theory
date: 2023-02-20 02:17:55
tags:
- CSD
---

## 信息论

信息理论是对信息的量化、存储和通信的科学研究。 

信息理论的一个关键措施是熵。

熵量化了随机变量的值或随机过程的结果中所涉及的不确定性的数量。 

信息论中的其他一些重要衡量标准是互信息、信道容量、误差指数和相对熵。 

信息是消息的有效内容;信息蕴涵于事件的不确定性之中

明年电子科大男生比女生多——几乎是必然的，信息量趋于零 

明年电子科大女生比男生多——可能性很小，信息量极大

入学前，有大于/小于/等于三种可能，存在不确定性

入学后，仅存一种结果，信息不确定性降为零

信息量=消息获得前的不确定性

### 信息量的度量--熵

![image-20230222073226026](CSD-Information-Theory/image-20230222073226026.png)

### 消息中的冗余：冗余度

► 所有的数据编码方式都有一些结构，这使得它们与纯粹的随机集合不同。 

► 英语是高度结构化的，有很多的冗余。 

► 压缩英语文本的文件减少了结构，但在压缩编码表中仍有一些结构。 

► 信息理论提供了对冗余量的定量估计。 

► 利用这种冗余的代码破解攻击被称为统计攻击。

冗余，为了描述信息而包含在消息中的多余部分

定义：长度为Ｎ比特的消息Ｍ，假设它的信息量为Ｈ(Ｍ)，则其冗余度为：

![image-20230222074142031](CSD-Information-Theory/image-20230222074142031.png)

（也可以说$H(M)\div N$ 等于1时，没有冗余。这个可看作编码效率）

 总冗余为![image-20230222074426126](CSD-Information-Theory/image-20230222074426126.png)

![image-20230222074514388](CSD-Information-Theory/image-20230222074514388.png)

有意思~

![image-20230222074632519](CSD-Information-Theory/image-20230222074632519.png)

1/(1-D)=/N/H(M),表示消息长度/信息量，完美压缩就是把消息压缩到只剩信息

### 语言的绝对码率

► 绝对速率（R）被定义为可由语言编码的最大信息位数，假设所有字符序列的可能性相同。 

► 让L成为字母表中的字符数。 

► R = log2(L)

​		 o 注意，这意味着L = 2^R

► 在英语中，R = log2(26) = 4.7 

#### 一种语言的实际码率  

► 一种语言的实际码率（r）被定义为该语言中每个字符信息的平均比特数。 

​	o 它本质上是每个字符的熵。 

► 我们可以通过定义所有长为N的字符串的每个字符的码率rN来计算它，并观察N变大后的趋势。 

► 我们可以利用熵将其定义为。

► rN = H(X) / N 

​	o 其中X是所有长度为N的消息的集合，使用语言中的字符。

► 随着N的增加，速率下降，因为选择较少，一些选择更有可能。 

​	o 这种减少迅速变小到一个恒定值。 

► 在英语中，rN对于大的N来说每个字符是在1.0和1.5比特之间。 

► r是N大时rN的值。 

► 本课程将假设英语的r=1.5。

### 一种语言的冗余度

►一种语言的冗余度（D）被定义为：D = R - r （绝对码率-实际码率）

为什么R>r?

​	因为R假设每个字母出现概率一样，然而实际中不一样，实际中我们是知道一些信息的，所以实际r会比较小

► 在英语中，D = 3.7 ... 3.2。我们将使用3.2。 

► 这对应于68%的冗余度。 

► 冗余度来自于

​		o不均匀的单字母分布；

​		o不均匀的二位组合（2个字母）频率；

​		o不均匀的三位组合（3个字母）频率。 

► 通过删除元音和双字母。

► mst ids cn b xprsd n fwr ltrs, bt th xprnc s mst nplsnt. 

### 唯一解距离Unicity Distance

► 如果我们对一些密码文本进行解码以产生纯文本，我们如何判断我们是否已经成功了?

► 我们需要多少个字符的密码文本来确定一个看起来不错的解密后的明文是真正的信息。 

► 这个数字被称为统一性距离。

► 假设我们有一个L符号的字母表。 

► 长度为N的可能消息的数量是$L^N = (2^R)^N = 2^{RN}，因为L = 2^R$ $(R=\log_2^L)$

► 有意义的消息的数量可以用语言的实际码率来表示，即 $2^{rN}$

► 如果我们假设所有信息的可能性相同，那么偶然得到一个有意义信息的概率是

​							$	\frac{N_{am}}{N_{pm}}= 2^{rN} / 2^{RN} = 2^{(r-R)N} = 2^{-DN}$，D是语言的冗余度

分子分母分别代表明显有意义的信息的数量 和 可能的信息数量

### 密钥空间

►尝试所有可能的钥匙，保留那些看起来正确的钥匙。
	o 穷举搜索或蛮力攻击。
► 让K是所有可能钥匙的集合。
► 现在钥匙的数量是$2^{H(K)}$
	o 我们必须使用钥匙空间的熵，因为所选择的钥匙值可能表现出一些冗余性。
► 所以错误钥匙的预期数量是
	 $2^{H(K) }- 1$, 大约为$2^{H(K)}$
► 在这里我们假设有很多可能的钥匙，除了一个之外都是错误的。

► ==看上去可能是正确的错误解的预期数量==
= 错误钥匙的数量 * 机会有意义的信息的概率

=$2^{H(K)} * 2^{-DN}$

=$2^{H(K)-DN}$

► 这是一个快速递减的N的函数
► 我们可以将指数=0时的交叉点上的N值定义为统一性距离Nu
$H(K) – D\times N_u = 0,因此 N_u = H(K) / D$

### 使用唯一解距离

► 如果$N>N_u$(N为明文长度)
那么得到假阳性的机会是可以忽略不计的，因为看起来正确的错误信息的数量远远小于1。
► 另一方面，如果$N < N_u$，那么许多看起来正确的信息将是错误的。
► $N_u$约是明确破解密码和确定密钥所需的字符数。

唯一解距离是针对唯密文攻击所做的分析。实际操作中往往会采 用更有效的方式 

唯密文攻击时，所需的密文长度通常远大于唯一解距离 

利用冗余度 

​	消息中，字符间、上下文存在的一系列规则，产生冗余 

​	密文中冗余被分散，但仍存在。累计足够多的密文将保证只有一对消息 和密钥满足这些规则，此时破译成功 当宣称某种密码系统和密钥被破译时： 

​	若使用的密文长度远大于唯一解距离，则可信； 

​	若使用的密文长度相当于或小于唯一解距离，则很可疑。

### 随机假设

► 前面的模型假设了一个随机加密系统。 

► 特别是，在以下方面没有关系： 

o 类似的密钥和密码文本 

o 类似的明文文本和密码文本。 

► 如果加密是非随机的，则统一性距离较小。

### 混淆和扩散 

► 这个随机概念通常用两个术语表示：混淆和扩散。 

► 如果改变密钥中的一个比特会改变大约一半的密码文本的比特，那么一个加密系统具有良好的混淆性。 

► 一个加密系统具有良好的扩散性，如果改变纯文本中的一个比特就会改变大约一半的密码文本的比特。

### QUIZ

1. 定义 "一组信息的熵"，并说明如何计算它。一种语言包含5个符号。A、B、C、D和E。A、B、C各出现1/4的时间，而D和E出现1/8的时间。这种语言的熵是多少？

   *一组信息所携带的信息量，本质上是事件发生概率的函数*

   $*E(m)=1/4(2*3)+2*1/8*3=2.25$

2. 定义 "统一性距离 "一词。计算它需要什么信息？"单性距离 "的概念有什么用？一种新发明的语言在其字母表中有16个不同的符号，而且相当精确。平均来说，字母表中的每个字母都传达了2比特的信息。这种语言的信息是用8个字符的密钥来加密的。众所周知，用户会选择全部为小写的英语密钥。这些加密信息的统一性距离是多少？

   *确认一个看似正确的解密是否是真的明文，所需要破解的最少密文字母数量*

   *用来设计密文长度来防止敌人破解。或者当敌人生成破解时，如果$D>>D_n$，则不可信*
   $$
   H(K)=8*1.5=12\\
   
   D=R-r=log(16)-2=2\\
   
   Nu=H(K)/D=12/2=6\\
   $$
