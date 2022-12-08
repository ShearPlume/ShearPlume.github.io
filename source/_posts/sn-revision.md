---
title: sn revision
date: 2022-12-06 20:32:06
tags:
---

## 2021

#### 1

##### a

1023的二进制：0000 0011 1111 111103FF

补码：11 11110000 000001 FC01

##### b

会，8位可表示补码数在-128到127之间，而100+30=130>127，实际是-126

01100100+

00011110+11101100

=

10000010+

11101100

=

01101110

##### c

不是，因为二进制补码正负表示范围不同，举例：8位二进制补码范围是-128到+127，而1-128和1+（-128）不一样，前者会超出补码表示范围

##### d

```assembly
;int n
;int[] x[n]
;int[] y[n]
;for(int i=0;i<n;i++)
;{
;	if(x[i]&1!=0)
;	y[i]=0
;	else
;	y[i]=1
;}
;REGISTER USAGE
;r1=i
;r2=n
;r3=1
;r4=x[i]
;r5=y[i]
;r6=temp result
;INITIALISATION
	LEA	R1,0[R0]	;SET I INITIAL 0
	LOAD	R2,N[R0]	;SET N TO R2
	LEA	R3,1[R0]	;SET CONSTANT 1 TO R3
;MAINLOOP
LOOP	CMPGT	R9,R2,R1	;IF I<N
	JUMPF	R9,DONE[R0]	;IF I!<N,GOTO DONE
	LOAD	R4,X[R1]	;LOAD X[I]	
	AND	R6,R4,R3	;X[I] AND 1
	JUMPF	R6,SKIP2[R0]	;IF EVEN, GOTO SKIP2
	STORE	R0,Y[R1]	;IF ODD,Y[I]=0	
	JUMP	SKIP3[R0]	;IF ODD GOTO SKIP3
SKIP2	STORE	R3,Y[R1]	;IF EVEN,Y[I]=1
SKIP3	ADD	R1,R1,R3	;I++
	JUMP 	LOOP[R0]	;GO BACK TO LOOP
DONE	 TRAP	R0,R0,R0	;END

;DATA AREA
X		DATA	1
		DATA	2
		DATA	3
		DATA	4
		DATA	5
		DATA	6
		DATA	6
		DATA	5
		DATA	4
		DATA	3
		DATA	2	
		DATA	1	;SET X[0~N-1]
Y		DATA	0
		DATA	0
		DATA	0
		DATA	0
		DATA	0
		DATA	0
		DATA	0
		DATA	0
		DATA	0
		DATA	0
		DATA	0
		DATA	0	
N		DATA	12	;SET N=12

```

##### e

```assembly
;INITIALISATION
	
	LEA	R1,$41A5[R0]	
	LEA	R3,$4000[R0]
	AND	R1,R1,R3
	LEA	R3,14[R0]
	SHIFTR	R1,R1,R3
	LEA	R2,0[R1]
2+2+1+2+1+2=10
```

#### 2

##### a

缓存存储器如何加速程序的执行？许多高速缓冲存储器只对读周期进行缓冲。为什么会这样，为什么它通常不被看作是一个主要的限制？讨论一下在某些情况下，缓存的写周期是否会带来一些好处。

答：cache的读写速度比普通内存快10倍，但是容量比较小，而cache会暂存第一次从内存中读取的内容，并在有限时间内存储，以便后续再次访问时能快速读取而不用从内存中慢速读取

只对读周期缓冲的原因：多次从memory中读同一个内容时周期时，改成从cache中读取会比直接从memory中读取省去很多时间，但是多次向memory写同一内容时仍需在memory上进行写操作，cache对此没有提高速度的效果

##### b

下面的Sigma 16代码是用来处理一个10个元素的二进制补码数组（只显示了第一个元素），并用它们的二进制补码倒数替换所有的元素。8000美元的数字是不允许的。然而，尽管这段代码可以组装，但它包含几个错误。

i. 为该程序制定一个寄存器使用表（适合作为注释列入）。 

ii. 识别这些错误并解释你将如何纠正它们。

 iii. 写出更正后的程序

###### i:

N=R1

R1=R2

R2=N

00000011

1111111111111101

```assembly
STORE R1,N[R0]
LEA	R2,0[R1]
LOAD R2,N[R0]

R1=4
R2=5


```



```assembly
;register uesage:
;R1	1
;r2 i
;r3 n
;r4 x[i]
;r5 temp bool
		LOAD 	R1,1[R0] ;Set R1 to constant 1
		ADD 	R2,R0,R0 ;i:=0
		LOAD	 R3,n[R0] ;Set R3 to n
FORLOOP	CMPEQ R5,R2,R3 ;Is i<n
		JUMPF R5,OUT[R0] ;if yes, exit
		LOAD R4,X[R2] ;load x[i]
		INV R4,R4,R0 ;R6= -x[i]
		ADD R1,R2,R2 ;i:=i+1
		STORE R4,X[R2] ;x[i]=-x[i]
		JUMP FORLOOP[R0] ;loop
		OUT TRAP R0,R0,R0
; Data Area
		n DATA 10
		X DATA -8
```

###### ii:

错误1：应该用lea

错误2：JUMPF

错误3：INV只是取反，补码求负数还得再+1

错误4：应该是R4=-x[i]（好像不算）

错误5：因该是ADD	R2,R1,R2

错误6：先存负数再i++顺序反了

###### iii:

```assembly
;register uesage:
;R1	1
;r2 i
;r3 n
;r4 x[i]
;r5 temp bool
;r4	-x[i]
		LEA	R1,1[R0] ;Set R1 to constant 1
		ADD 	R2,R0,R0 ;i:=0
		LOAD	 R3,n[R0] ;Set R3 to n
FORLOOP	CMPEQ R5,R2,R3 ;Is i<n
		JUMPT R5,OUT[R0] ;if yes, exit
		LOAD R4,X[R2] ;load x[i]
		INV R4,R4,R0 ;R4= -x[i]
		ADD	R4,R1,R4
		STORE R4,X[R2] ;x[i]=-x[i]
		ADD R2,R1,R2 ;i:=i+1		
		JUMP FORLOOP[R0] ;loop
		OUT TRAP R0,R0,R0
; Data Area
		n DATA 10
		X DATA -8
```

##### c.估计修正后的程序需要多少内存周期才能运行。

循环前：2+1+3=6

循环一次：1+2+3+1+1+3+1+2=14

最后一次循环前：1+2=3

循环后：1

共：6+14*10+3+1=150

##### d.在修正后的程序中，如果一个主存储器周期需要10ns，而一个高速缓存周期需要1ns，那么估计一个带有高速缓存的系统将获得的优势。

原时间：1500ns

cache后9次循环将hit，cache hits =（ 1+2+2+1+1+2+1+2）*9=108

最后一次的3次cycle也会cache hit，total cache hits=108+3=111

saved time=111*9=999ns

total time=10\*（7+14+2\*9）+111=501

#### 3

##### a

在互联网通信中，路由器是如何将IP数据包送到目的地的？解释一下为什么IP使用的路由方法对TCP段或以太网帧都不起作用。

当一个IP数据包需要被发送到其目的地时，路由器使用其路由表来确定最佳路径。路由表是一组规则，路由器根据每个数据包的目标IP地址来确定将传入的数据包发送到哪里。

一旦路由器确定了最佳路径，它就将数据包转发到该路径的下一跳。这个过程一直持续到数据包到达目的地。

IP使用的路由方法对TCP段或以太网帧都不起作用，因为这些类型的数据单元有不同的格式，包含的信息也与IP包不同。例如，一个TCP段包含有关源和目的端口号、序列号和确认号的信息，以及其他与路由过程无关的细节。另一方面，一个以太网帧包含有关源和目的MAC地址的信息，这些信息用于本地网络通信，而不是互联网范围的路由。

##### b

一个IP接口的地址是192.10.0.1。这个地址代表什么二进制值？同时写出该值的十六进制

bin:1100 0000 0000 1010 0000 0000 0000 0001

hex:00c0 000a 0000 0001

##### c

"IP不可靠，而IP承载着TCP；因此，TCP也不可能是可靠的。" 对这个论证的前提和结论的真实性进行评论，并讨论推理是否有效。

标准答案：

IP是不可靠的：数据包可能丢失，协议不会恢复它们。
数据包可能排序错误或重复，协议不会补偿；协议不检查数据错误[2]。IP确实承载了TCP。所以，两个前提都是真的[1]。
结论是不正确的。TCP会恢复丢失的网段，必要时重新排序，使用网段编号并对所有携带的数据进行校验[2]。
这个论点是无效的，因为低级协议不可靠的事实并不意味着它所携带的高级协议也会不可靠。高层协议可以用来增加低层协议的能力，事实上这就是分层的全部动机[1]。

前提正确，

##### d

在一个特定的主机上可以同时运行许多TCP连接。参照你所知道的关于通信系统及其与操作系统的关系，解释这一点是如何做到的。

标准答案： 

假设一个能够运行多个并发进程的操作系统。 通信系统通过使用称为端口号的传输层子地址来运行多个并发连接[1]。不同的进程在同一时间使用通信系统，将自己附加到不同的端口[1]。当一个包含传输层段的IP数据包到达时，该段由IP层提取并向上传输到传输层[1]。该段有一个带有目的端口号的头，该端口号将其引导到正确的目的进程[1]。当一个进程发送数据时，产生的网段总是包括该进程所处的源端口，以便回复可以被正确引导[1]。

AI：

在一个给定的主机上有可能同时运行许多TCP连接，因为操作系统使用一个被称为 "端口 "的概念来跟踪不同的连接。  当建立一个TCP连接时，主机和远程设备会商定一个唯一的端口号，用来识别连接。这个端口号被操作系统用来跟踪连接，并将传入和传出的数据路由到正确的应用程序中。  由于有超过65,000个可用的端口号，一台主机可以有多个活跃的TCP连接，每个都使用不同的端口号。操作系统使用端口号来跟踪不同的连接，并将数据发送到正确的应用程序。这使得一台主机上的多个应用程序可以同时建立和维护多个TCP连接。



## 2020

#### 1

##### a

Find two 8-bit codewords, X and Y, such that X+Y overflows if the code being used is unsigned but  does not if it is two’s complement. Now find two codewords, W and Z, such that W+Z overflows in  both codes. Explain your reasoning carefully.



##### b

$-2^{31} to 2^{31}-1$

原因：补码最高位是符号位因此数据表示只有31位，而补码会产生所谓的“正0”和“负0”，补码规定将-0的位置留给负数表示范围，因此负数表示范围多1

##### c

找出两个8位编码，X和Y，如果使用的编码是无符号的，X+Y会溢出，但如果是两补的，则不会溢出。 如果是无符号代码，X+Y会溢出，但如果是二进制补码，则不会溢出。现在找出两个代码，W和Z，使W+Z在两种代码中都能溢出。 都会溢出。仔细解释一下你的推理。

X:10000001

Y:01111111

无符号相加是129+127=256超过了八位无符号数的表示范围0~255

补码则是127+（-127）=0=00000000

W:10000001

Z:10000001

无符号数是129+129=258超出0~255

补码则是-127+（-127）=-254超出-128~127

##### d

编写一个Sigma16程序，在一个有n个元素的无符号数组X中，从每个元素中减去1，除非该元素已经为0。 假设n是数据存储器中的无符号变量，表示数组中的元素数。完全注释你的代码。



```assembly
;int n;
;for(int i=0;i<n;i++)
;{
;    if(x[i]!=0)
;	x[i]-=1          
;}
;REGISTER USAGE
;R1=I
;R2=N
;R3=CONSTANT 1
;R4=TEMP BOOL AND TEMP AND RESULT
;R5=X[I]
;INITIALISATION
	LEA	R1,0[R0]	;SET I INITIAL 0
	LOAD	R2,N[R0]	;SET N TO R2
	LEA	R3,1[R0]	;SET CONSTANT 1 TO R3
;MAINLOOP
LOOP	CMPGT	R4,R2,R1	;IF I<N
	JUMPF	R4,DONE[R0]	;IF I!<N,GOTO DONE
	LOAD	R5,X[R1]	;LOAD X[I]
	CMPEQ	R4,R5,R0	;IF X[I]==0
	JUMPT	R4,SKIP1[R0]	;IF X[I]==0,GOTO SKIP1
	SUB	R4,R5,R3	;X[I]-=1	
	STORE	R4,X[R1]	;STORE
SKIP1	ADD	R1,R1,R3	;I++
	JUMP 	LOOP[R0]	;GO BACK TO LOOP
DONE	TRAP	R0,R0,R0	;END
;DATA AREA
X		DATA	3
		DATA	-6
		DATA	0
		DATA	10	;SET X[0~N-1]
N		DATA	4	;SET N=4

```

#### 2

##### a

区分主存储器和辅助存储器，并简要解释CPU如何访问存储在两者中的数据  存储的数据。如果一个用户在运行现代操作系统的PC上遇到了性能问题，并使用虚拟内存  遇到问题，在什么情况下，你会建议增加主内存的数量？解释一下你的理由。

AI:

主存储器和辅助存储器是两种不同类型的存储设备，在计算机系统中发挥不同的作用。

主存储器，也被称为RAM（随机存取存储器），由存储器模块组成，是计算机系统中的主要存储区域，通常位于主板上。主存储器的容量有限，但速度快，所以它被用作程序和数据的主要存储区域。由于主存储器的容量有限，当一个程序需要更多的存储空间时，系统会将一些不太常用的数据存储在二级存储器中。

二级存储器是由硬盘、固态驱动器或其他大容量存储设备组成的。它的容量比主存储器大得多，但访问速度较慢。由于其容量大，二级存储器用于数据的长期存储。

当一个程序需要访问主存储器中的数据时，CPU直接访问主存储器，因为它的速度较快。如果一个程序需要访问二级存储器中的数据，CPU首先访问一级存储器，将需要的数据加载到一级存储器中，然后再访问一级存储器来获取数据。

如果用户在运行使用虚拟内存的现代操作系统的PC上遇到了性能问题，我会建议增加主内存的数量。这是因为主内存被用作CPU和辅助内存之间的缓冲器，如果主内存不足，系统将不得不不断地在主内存和辅助内存之间交换数据，这会降低性能。通过增加主内存的数量，系统将有更多的空间来存储数据，减少交换的需要并提高性能。

答案：

 主存储器是可通过地址总线直接寻址的存储器。CPU可以通过将该位置的地址放在地址总线上，随机访问这种存储器中的任何选定的位置：然后地址解码单独选择该位置，数据可以通过数据总线读或写到该位置[2]。二级存储器不是随机访问的，而是被视为I/O设备（磁盘）。磁盘被划分为有编号的扇区，每个扇区可以存储一个固定大小的数据块。CPU必须通知I/O（磁盘）接口它希望处理的扇区编号，以及该操作是读还是写。如果是前者，它将从扇区接收一个数据块；如果是后者，它将向扇区发送一个数据块[2]。 一个现代的多任务操作系统将使用虚拟内存来允许更多的任务被激活，而不是主内存所能支持的。如果主内存已满，则在磁盘上和磁盘外交换页面，但这很慢。如果任务运行时有持续的磁盘活动，一个合理的假设是没有足够的主内存，页面交换频繁发生。增加主内存可以缓解这种情况[2]。

##### b

下面这段Sigma 16代码的目的是将一个8元素的数组（只显示了第一个元素）与所有的元素相加，将结果放在另一个变量sum中。然而，尽管这段代码可以组装，但它包含几个错误。
i. 为该程序制定一个寄存器使用表（适合作为注释）。
ii. 识别这些错误，在每一种情况下解释什么是错误的，以及你将如何纠正它。
iii. 写出更正后的程序

```assembly
;registor usage
;r1 1
;r2 i
;r3 n
;r4 sum
;r5 temp bool
;r6 x[i]
LEA	R1,1[R0] ;Set R1 to constant 1
ADD R2,R0,R0 ;i:=0
LEA R3,n[R0] ;Set R3 to n
ADD R4,R0,R0 ;sum=0
FORLOOP CMPEQ R5,R2,R3 ;Is i<n
JUMPF R5,OUT[R0] ;if yes, exit
LOAD R6,X[R0] ;load x[i]
ADD R4,R4,R1 ;sum:=sum + x[i]
ADD R1,R2,R2 ;i:=i+1
JUMP FORLOOP[R0] ;loop
OUT STORE R4,sum[R0]
TRAP R0,R0,R0
; Data Area
n DATA 8
sum DATA 0
x 	DATA 0
```

###### i

###### ii

1：应该是JUMPT

2：应该是LAOD R6,X[R2]

3：应该是ADD R4,R4,R6 ;sum:=sum + x[i]

4：应该是ADD R2,R2,R1 ;i:=i+1

5：应该用load得到n

###### iii

```assembly
;registor usage
;r1 1
;r2 i
;r3 n
;r4 sum
;r5 temp bool
;r6 x[i]
LEA	R1,1[R0] ;Set R1 to constant 1
ADD R2,R0,R0 ;i:=0
LOAD	R3,n[R0] ;Set R3 to n
ADD R4,R0,R0 ;sum=0
FORLOOP CMPEQ R5,R2,R3 ;Is i<n
JUMPT R5,OUT[R0] ;if yes, exit
LOAD R6,X[R2] ;load x[i]
ADD R4,R4,R6 ;sum:=sum + x[i]
ADD R2,R2,R1 ;i:=i+1
JUMP FORLOOP[R0] ;loop
OUT STORE R4,sum[R0]
TRAP R0,R0,R0
; Data Area
n DATA 8
sum DATA 0
x 	DATA 0
```

##### c

1+2+3+1+1+2=10

10*8+1+2+2+1+3+1+3+1=94

##### d

在修正后的程序中，如果一个主存储器周期需要10ns，而一个高速缓存周期需要1ns，那么估计一个带有高速缓存的系统将获得多少优势。

（1+2+2+1+1+2）\*7\*9+3*9=594

```assembly
int[]x
int[]y
for(int i=0;i<n;i++)
{
	x[i]=max(x[i],y[i]);
}

R1 I
R2 N
R3 X[I]
R4 Y[I]
R5 TEMP BOOL
R6 1

	ADD	R1,R0,R0
	LOAD R2,N[R0]
	LEA	R6,1[R0]
LOOP	COMEQ	R5,R1,R2
	JUMPT	OUT[R0]
	LOAD	R3,X[R1]
	LOAD	R4,Y[R1]
	COMGT	R5,R3,R4;IF X IS GREATER
	JUMPT	R5,FLAG[R0]
	LEA		R3,0[R4]
	STORE	R3,X[R1]
FLAG	
	ADD		R1,R1,R6	
	JUMP	LOOP[R0]
OUT	TRAP	R0,R0,R0
		
	



X	DATA	1
	DATA	2
	DATA	3
Y	DATA	2
	DATA	3
	DATA	4
N	DATA	3
```

