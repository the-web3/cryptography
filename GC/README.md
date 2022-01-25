## 混淆电路

### 一. 混淆电路的发展现状

1982 年：姚期智提出混淆电路，此时的混淆电路识两方计算

2009 年：Lindell 等给出了安全性证明和详细介绍

2013 年：Goldwasser 给出了简化形式

### 二. 逻辑电路

### 三. 混淆电路

### 三.GMW 协议

### 四.BGW 协议

BGW 协议也是支持多方的安全计算协议，BGW 协议基于 Shamir(t, n)门限秘密共享机制，利用了 Shamir 秘密共享机制的加法同态和乘法同态的性质。

假设 BGW 协议的参与者一共有 n 人，假设参与者 Pi 需要输入秘密 ，则参与者 Pi 首先利用Shamir(t,n)门限秘密共享机制将秘密 共享给其他所有参与者，阈值 t 的选择根据具体使用情景下的安全性要求决定。

当所有参与者的输入都通过Shamir(t, n)门限秘密共享机制分享后，每个参与者都掌握了协议输入的子秘密。假设一个门的输入分别为 a 和 b ，秘密 ai 和 bi 已经分别由秘密分配函数

.： 
    ![.： 
](https://github.com/guoshijiang/cryptography/blob/master/img/bgw1.png)

分配完成，fa(0) = a, fb(0) = b， 参与者 Pi 掌握 a 和 b 的子秘密 ai , bi。在布尔电路上，可将异或门和与门分别看成在有限域 F2 上的加法和乘法。将异或用模为 2 的加法进行计算，与用模为 2 的乘法进行计算。

.： 
    ![.： 
](https://github.com/guoshijiang/cryptography/blob/master/img/bgw2.png)


对于异或门：由于 Shamir 具有加法同态性，因此

.： 
    ![.： 
](https://github.com/guoshijiang/cryptography/blob/master/img/bgw3.png)

假设 ci = ai xor bi，则 c(i) = a(i) xor b(i) ，而 a(i) = ai和 bi =b(i) 都由 Pi 掌握，因此 Pi 可以本地计算出 ci = ai xor bi 。当所有计算完成后，每个参与者Pi公布自己计算出的 c(i) ，即可恢复出 c(x) 和 c(0)。 

.： 
    ![.： 
](https://github.com/guoshijiang/cryptography/blob/master/img/bgw4.png)


对于与门，和之前叙述过的基于 Shamir(t, n)门限共享机制的多方乘法计算相同，只是 BGW 是在有限域 F2 上。每个参与者 Pi 计算 ai * bi ，接着每个Pi独自选取次数为 t 次的随机多项式 hi(x) ，且满足 hi(x) = di ,1 ≤ t ≤ n ， t < n / 2 。向各个参与者分配 di ，且 cij = hi(x) , 所有参与者分配结束后，Pi 掌握了信息 c1i, c2i ... cni ，同时再利用公开的重组向量1, ... n， 

Pi 计算:

.： 
    ![.： 
](https://github.com/guoshijiang/cryptography/blob/master/img/bgw5.jpeg)

此时 Pi 掌握的子秘密 ci 即为 c 的子秘密。当所有计算完成后，每个参与者公开自己的子秘密，再根据之前叙述的 Shamir(t, n)门限秘密重构算法即可获得 。



### 五.总结

经过近几年的发展，MPC协议系统已经不再使用严格的电路表示，而是使用混合模型，在混合模型中，函数被编译成一组优化的子协议函数，用于公共操作。这组原语可以包括传统的基于电路的协议模型，可以在单个协议中被无缝地描述。混合模型系统通常将中间值表示为一个大的有限域上的密钥分享。它们可以使用信息论和密码协议的混合，因此，计算参与方的数量和威胁模型都不同。

与严格的基于电路的模型相比，混合模型允许存在非常不同的性能特性。例如，在有限域中，比较、位移和相等性测试等操作作为算术电路表示代价高昂。然而，操作密钥分享的专用子协议在共享计算结果方面却非常高效。
