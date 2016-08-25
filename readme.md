### 代码和笔记 - Build a Modern Computer from First Principles: From Nand to Tetris (Project-Centered Course)

https://www.coursera.org/learn/build-a-computer






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










