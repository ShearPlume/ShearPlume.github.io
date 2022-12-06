---
title: sn revision
date: 2022-12-06 20:32:06
tags:
---



1.为了实现多任务，当一个任务占用cpu太久时，硬件定时器达到设定时间后停止执行当前进程，并跳转到中断的地方继续执行中断代码

## 2021

### 1

#### a

1023的二进制：0000 0011 1111 111103FF

补码：11 11110000 000001 FC01

#### b

会，8位可表示补码数在-128到127之间，而100+30=130>127，实际是-126

01100100+

00011110+11101100

=

10000010+

11101100

=

01101110

#### c

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

## 2020

##### a

Find two 8-bit codewords, X and Y, such that X+Y overflows if the code being used is unsigned but  does not if it is two’s complement. Now find two codewords, W and Z, such that W+Z overflows in  both codes. Explain your reasoning carefully.

X:10000001

Y:01111111

无符号相加是129+127=256超过了八位无符号数的表示范围0~255

补码则是127+（-127）=0=00000000

W:10000001

Z:10000001

无符号数是129+129=258超出0~255

补码则是-127+（-127）=-254超出-128~127



