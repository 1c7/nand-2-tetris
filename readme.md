### 代码和笔记 - Build a Modern Computer from First Principles: From Nand to Tetris (Project-Centered Course)

https://www.coursera.org/learn/build-a-computer

## 问题
if 语句这种条件判断 5>0 在底层是怎么做的？




## 超重点
HalfAdder 2个输入2个输出，sum 的那一列和 Xor 一样，carry 的那一列和 And 一样。
Project 1 是很多非常基本的门， and or xor mux demux
Project 2 HalfAdder, FullAdder, Inc16, ALU
Project 3 开始搞 Register 和 RAM，多个 Register 组成 RAM，多个 RAM 组成更大的 RAM，以及实现 PC。
这次我们不造 Data Flip Flop


<br/>
### Week 4
机器语言


<br/>
### Unit 4.2
只有一个非常大的 RAM 可以用，
但更好的方法是做不同层级的 RAM，快的，小的接近 CPU，大的，慢的。
CPU 本身包含一些 register，这些 register 的数量和功能是机器语言的核心部分。
Their number and functions are a central part of the machine language
Data Register 存数据
Address Register 存地址

Addressing Modes

Input Output
有很多输入输出设备

CPU 和这些设备的一个交互方法是，用 memory mapping
比如内存地址 12345 存放鼠标最新的移动方向

Flow Control
- 顺序执行 executes machine instructions in sequence 
- jump unconfitionally  比如循环
- jump only if some condition is met 


<br/>
### Week 3

<br/>
### Unit 3.5 project 3
http://nand2tetris.org/03.php
最好做法依然是忽略你自己做的，用内置的 CHIP
有 a,b 两个自带的目录，别动。  
为了强迫模拟器用内置实现，因为 RAM 是一层包一层，模拟器会受不了。

给的 chip ：前面做的 CHIP ，以及 DFF (data flip-flop)
前面的 CHIP 有：



目标，造以下 8 个东西：
- Bit
- Register
- RAM8
- RAM64
- RAM 512
- RAM 4K
- RAM 16K
- PC = Program Counter
bit 可以用一个 DFF 和一个 xor 做
16 bit register 可以
8 register RAM
RAM 64 拿 8个 RAM 8 堆就好了
RAM 512 拿 RAM 64 堆
地址的一部分是选 RAM ，还有一部分是选 RAM 里的具体 register
用 mux 和 demux 来处理这些地址

06:40 开始讲 PC，一个 register 一个inc 和一些门可以实现 




<br/>
### Unit 3.4 counters
counter 用于记录当前执行到哪里了，可以想象成是手指指着某个位置。
然后也可以实现控制流，跳过一些代码。
3种可能的控制：
reset: PC = 0    重置到0
next: PC++    就是+1
goto: PC = x   跳到任意位置

CHIP counter:
左边 in  16 bit
右边 out 16 bit

上面, load, inc, reset
视频后半部分就是操作软件来演示了。




<br/>
### Unit 3.3 memory-units
多个 DFF， data flip flop 可以组成一个 x bit 的 register，寄存器。
然后多个 register 可以组成 RAM
在任意时刻，只有一个 register 可以选中。

RAM
左边输入 in (w长度, 比如32bit)
左边输入 address (k)

上面是 load
然后有个 out (w 长度)

RAM 有时钟行为


<br/>
### Unit 3.2

<br/>
### Unit 3.1



<br/>
### Unit 2.5 Project 2
基于项目 1 的 CHIP 之上，再做 5个，
- HalfAdder  
- FullAdder  
- Add16  
- Inc16  
- ALU  


#### 1. HalfAdder 
输入 a,b 输出 sum, carry
sum 当然就是和，carry 就是是否进位
true table 有四列，
你会发现 
sum 的那一列和 Xor 一样
carry 的那一列和 And 一样
所以实现起来很简单

#### 2. FullAdder
输入 a,b,c 输出 sum, carry
2个 HalfAdder  1个 Or 就行了

#### 3. Add16
1个  HalfAdder 处理最右边的，然后15个 FullAdder 处理左边的




<br/>
### Unit 2.4 arithmetic-logic-unit
详细解释了 ALU 这个 CHIP 是咋样的。
这个 ALU 是简化版的，但是够用了。

#### The HACK ALU
x,y 2个 16 bit 的输入
out 1个 16bit 的输出，

6 个输入 bit

| zx |nx| zy | ny | f | no |
|---|---|---|---|---| ---|

2 个输出 bit 

| zr |ng |
|---|---|
| zero | negative |

含义
| name | meaning |
|---|---|---|---|---| ---|
|zx| if zx == 1,  x=0 |
|nx | if nx == 1, x=!x |
|zy | if nx == 1, x=!x |
|ny | if nx == 1, x=!x |
|f| if nx == 1, x=!x |
|no| if nx == 1, x=!x |


注意有顺序，如果 zx 和 nx 都是1，那么 zx 先发生
zy,ny 一致。

f： if  f == 1, then out=x+y, else x&y
注意这些操作是在运算之前的，就是 x 和 y 进来之后，先按照这 6个 bit 进行对应的操作。
然后后面才该干啥干啥。

0800 

<br/>
### [Unit 2.3 Negative Number](https://www.coursera.org/learn/build-a-computer/lecture/seM6y/unit-2-3-negative-numbers)
##### 用最左边那位的 0 和 1 来代表正数负数是一种方法，  
造成的问题： -0 是什么鬼？  (1000 0000)

##### 另一个方法：2^n - x
1101是 -3   
怎么从一串二进制看出是什么负数？   
第一步，根据位数算出2的次方，这里有4位，2的4次方，== 16    
第二步，直接看这个二进制代表的正数是什么，1101 是8+4+0+1 = 12+1 = 13     
第三步，13-16 = -3，    

1111 是 -1
第一步，16
第二步，8+4+2+1 = 15
第三步，15-16 = -1

这叫做 2's complement representation
所以一段二进制，根据不同的看法，可以是某个正数或者是某个负数    
这种算法谁想出来的？？

4 bit ，4个xxxx，0~7 是正数，-1~-8是负数


04:01   for free
这样做负数的运算很简单，都不用干嘛，
-2  +  -3 = 14 + 13 （同样二进制，不同看法而已）
然后一算，得到11011，但是最前面那位扔掉了，变成1011，
然后其实就是 -5 了哈哈哈  

07:24
怎么根据 x 计算出 -x？  
2^n-x = 1+(2^n-1)-x

比如 4 怎么转换成 -4？  (2's complement 表示法)

4 = 0100
1111 - 0100 = 1011
然后 1011 +1 = 1100   
完了。

1100 = 正数 12 = 负数 12-16 = -4   
视频完。    



<br/>
### Unit 2.2 Binary Addation 
overflow ：最左边2位都是1，要进位，怎么吧？不管它。 ignore it  
05:56  开始讲 Adder  
- Half Adder - a,b 输入, sum, carry 输出  
- Full Adder - a,b,c 输入, sum, carry 输出，其实和 half 的区别就是多了个输入负责接进位  
- Adder  - 多 bit 的 Adder  
最右边是 half adder 因为不可能有进位，然后左边全都是 full adder，


总结， half 也好 full 也好都只是2位的bit 运算， adder 才是多位的.  




<br/>
### Unit 2.1
讲2进制怎么理解成10进制， 2的0次方  1次方，2次方，等等。  

2和10进制之间怎么转换，
2 -> 10  
10 -> 2  找最大的2次方数字，
10进制的87，最大的2次方数是64，然后拼下去




<br/>
### Nand 
最最基本的门    
只有双 1 的时候是0，其他时候都是1       
课上证明了 NAND 可以代替 AND 和 NOT，     
而 AND 和 NOT 可以组合出其他任何类型操作。       
也就是说只用 NAND 就可以制作出其他任何类型操作。这一个门就够了。      
没讲具体内部实现，这门课的唯一 primitive 门就是这个门了，  
然后要你按照顺序实现各种门。  



<br/>
### 索引是相反的
a[0] 是最右边的，



<br/>
#### Mux (Multiplexor)
| input | output | bottom-input |
|-------|--------| ------ |
| a, b |  out  | sel |
sel 就像开关
sel == 0 输出 a
sel == 1 输出 b

<br/>
#### AndMuxOr 
| input | output | bottom-input |
|-------|--------| ---- |
| a, b |  out  |  sel   |
sel == 0 进行 And 判断
sel == 1 进行 Or 判断

<br/>
####  DMux (DMultiplexor)
| input | output | bottom-input |
|-------|--------|---- |
| in  |  a, b|  sel |
sel == 0, in 去 a     
sel == 1, in 去 b    
   
根据 sel 是什么值, 决定是往 a 输出还是往 b 输出    
就像是分叉路口, 由 sel 决定是向左还是向右    

<br/>
#### And16
and 操作，只不过是 16 位的

<br/>
#### Mux4Way16 
16 bit, 4 way multiplexor

a,b,c,d 四个输入, 都是 16 bit 的, 四个 16 bit 的
2 bit sel 因为要控制四个输入，要用2个 bit 来表示4个东西
1 个 16 bit 的 out

<br/>
#### Xor
2个输入，1个输出
只有2个输入不一样的情况, 才输出 1
其他都是 0





<br/>
### HDL, Hardware Description Language, 硬件描述语言
- .hdl 是源文件    

- .cmp 是用来比较的, compare.    
  里面是正确的结果
  这个文件的生成方式就是用 hdl 和 tst 一起, 弄一个 .out 文件,
  里面是正确输出
  然后改成 .cmp 

- .tst 是 test script, 设定案例并且运行, 比如 ```set a 0, set b 0, eval;```   

<br/>
### Hardware simulators 硬件模拟器
这门课用的是自己的模拟器, 够用了    
外面有很多其他的模拟器  

<br/>
### 课程会给你 3 个文件
.hdl 是没实现完全的 chip  
.cmp 是正确的结果  
.tst 测试  

**你只需要写 hdl, ** write missing implementation