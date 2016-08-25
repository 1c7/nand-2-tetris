### 这里是代码和笔记 - Build a Modern Computer from First Principles: From Nand to Tetris (Project-Centered Course)

https://www.coursera.org/learn/build-a-computer













<br/>
### Nand 
最最基本的门
只有双 1 的时候是0，其他时候都是1 
课上证明了 NAND 可以代替 AND 和 NOT，
而 AND 和 NOT 可以组合出其他任何类型操作。
也就是说只用 NAND 就可以制作出其他任何类型操作。这一个门就够了。



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










