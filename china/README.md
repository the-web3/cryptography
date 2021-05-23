# 第 N 章：国密

### 一. 关于本文

国密即国家密码局认定的国产密码算法。主要有 SM1、SM2、SM3、SM4。密钥长度和分组长度均为 128 位。SM1 为对称加密，SM2 为非对称加密，SM3 消息摘要，SM4 分组密码算法。本次文将详细介绍四种主要国密的实现原理，以及 Java 代码实战，将会分析四种主要国密算法的应用场景；本次文针对有一定密码学基础或对密码学感兴趣的业界朋友

### 二. 本文结构

文章依次介绍 SM1、SM2、SM3、SM4 算法原理和代码实战，让大家对国密算法有所理解之后，我们接着会介绍国密 SM1、SM2、SM3、SM4 算法的应用场景，完成应用场景的介绍，我们将会分析国密的现状，以及国密未来的发展方向。

### 三. SM1 算法原理和代码实战

#### 1. SM1 简介

SM1 为对称加密，盖算法的算法实现原理没有公开，他的加密强度和 AES 相当，需要调用加密芯片的接口进行使用。SM1 高达 128 bit 的密钥长度以及算法本身的强度和不公开性保证了通信的安全性。由于 SM1 加密算法的不公开，我们无法知晓其内部的原理，所以这儿也无法做代码实现。

#### 二. SM1 应用场景

SM 1由获得国密办资质认证的特定机构将算法封装在芯片中，并销售给指定的厂商。SM1 算法己经被普遍应用于电子商务、政务及国计民生（例如国家政务、警务等机关领域）的各个领域。目前，市场上出现的系列芯片、智能 IC卡、加密卡、加密机等安全产品，均采用的是 SM1 算法。 数据加密包括软件加密和硬件加密两种方式。软件加密指单纯依靠代码来实现对软件的保护，而不需要特定的硬件服务。软件加密最突出的优势体现在它的成本低廉，实现简单，并且具备良好的灵活性和可移植性。但是，软件实现的加密要求 CPU 的全程参与，可能会产生不必要的等待和中断，从而导致系统资源浪费，特别是用软件加密处理海量数据时，会存在硬盘读写瓶颈的风险。而硬件加密利用集成在 CPU 芯片上的加密芯片实现，加密过程独立于 CPU，且在芯片内完成，可有效的防止数据被篡改。
大多数银行使用的硬加密，底层算法也常常含有 SM1 。

加密卡，就是将 AES、DES、MDS 等加密和认证算法集成在芯片上，该芯片被制成托卡（即加密卡），所有数据加解密和认证涉及到的运算全部在该卡上完成，进而加速了加解密过程，提升了设备的整体性能。目前，加密卡一般分为两类，一种是实现通用加解密和验证算法的加密卡，另一种是实现国密算法（SM1）的加密卡。

### 四. SM2 算法原理和代码实战

国密 SM2 为非对称加密，也称为公钥密码；国密算法的本质是椭圆曲线加密。关于对称加密和非对称加密的内容请查阅笔者写的《深入理解对称加密和非对称加密》一文。SM2 椭圆曲线公钥密码 ( ECC ) 算法是我国公钥密码算法标准。SM2 算法的主要内容包括 ３ 部分: 数字签名算法;  密钥交换协议和公钥加密算法。

#### 1. SM2 的形成过程

在所有的公钥密码中，使用得比较广泛的有ECC 和 RSA； 而在相同安全强度下 ECC 比 RSA  的私钥位长及系统参数小得多， 这意味着应用 ECC 所需的存储空间要小得多， 传输所的带宽要求更低， 硬件实现 ECC 所需逻辑电路的逻辑门数要较 RSA 少得多， 功耗更低。 这使得 ECC 比 RSA 更适合实现到资源严重受限制的设备中 ， 如低功耗要求的移动通信设备 、无线 通信设备和智能卡等。

ECC 的优势使其成为了最具发展潜力和应用前景的公钥密码算法 ， 至 2000 年国际上已有多个国家和行业组织将 ECC 采纳为公钥密码算法标准。在此背景下，我国从 2001 年开始组织研究自主知识产权的 ECC， 通过运用国际密码学界公认的公钥密码算法设计及安全性分析理论和方法 ， 在吸收国内外已有 ECC 研究成果的基础上 ， 于2004 研制完成了 SM2 算法． SM2 算法于 2010 年 12 月首次公开发布 ， 2012 年3 月成为中国 商用密码标准 （ 标准号为 GM/T0003—2012）， 2016 年 8 月成为中国 国家密码标准 (标准号为 ＧB/Ｔ 32918-2016)。

#### 2. 椭圆曲线

在有限域 K 上，形如以下方程：

![enter image description here](https://images.gitbook.cn/74a9f450-705f-11e9-aa97-d52fde2e3e58)

的方程被称为 Weierstrass 方程，其中 O=[0,1,0] 是唯一 的 Z 坐标为零的点，称为无穷远点。令 x=X/Z, y=Y/Z, 可将方 程记为:

![enter image description here](https://images.gitbook.cn/df7bb020-705f-11e9-b46a-41726d193891)

且仍有无穷远点 O。
对于方程中的系数，定义 

![enter image description here](https://images.gitbook.cn/3a4e1d80-7060-11e9-b46a-41726d193891)

其中:

![enter image description here](https://images.gitbook.cn/5da2c330-7060-11e9-aa97-d52fde2e3e58)

当 Δ ≠ 0 时，椭圆曲线是非奇异的 [1]，即对所有满足 F(X,Y,Z)=0 的射影点 P=(X ∶ Y ∶ Z), F 在 P 点的 3 个偏导数 
![enter image description here](https://images.gitbook.cn/8cfa5c60-7060-11e9-be31-a34bfde053f0)必不全为 0。

当 K 的特征不为 2 或 3 时，Weierstrass 方程又有以下形式：

![enter image description here](https://images.gitbook.cn/bd867df0-7060-11e9-83ce-bf64b45f6e99)

其中:E:y2=x3+Ax2+B 就是国家密码局建议使用的椭圆曲线，本文也是以此曲线为基础进行算法实现。

#### 3. 椭圆曲线基本运算

![enter image description here](https://images.gitbook.cn/55229ef0-72ff-11e9-a8ef-33cfb90ae5eb)

在椭圆曲线上，可以通过以下方式定义加法运算：取椭圆曲线上两点 P、Q，过 P、Q 作直线交椭圆曲线于R’…，过 R’做 y 轴的平行线交椭圆曲线于 R。若 P、Q 重合，则过 P 作曲线的切线交椭圆曲线于 R’…, 过 R’…做 y 轴的平行线交椭圆曲线于 R。规定 R=P+Q。如图一所示。对无穷远点 O 与椭圆曲线上一点 P，O+P=P+O=P。对 于 上 述 简 化 的 Weierstrass 方 程![enter image description here](https://images.gitbook.cn/956c7210-72ff-11e9-b7db-d127bed921dc)令![enter image description here](https://images.gitbook.cn/c6058bf0-72ff-11e9-a8ef-33cfb90ae5eb)

若 R=P+Q，则 :

![enter image description here](https://images.gitbook.cn/ee86cf30-72ff-11e9-a8ef-33cfb90ae5eb)

椭圆曲线密码体制即建立在上述加法运算和曲线构成的Abel 群上的密码体制。椭圆曲线密码体制主要涉及的运算是椭圆曲线上的点乘计算：Q=kP。Q、P 为椭圆曲线上的点，k为整数。

#### 4. 椭圆曲线大数运算的数学基础

##### 4.1 模运算与素数域

同余是数论中的等价关系，对于正整数 m 如果有 a=b+km（a，b，k 均是整数）那么记b=a mod（m），则称 a 与 b 关于 m 同余。当 m=p（p为素数）时，我们定义素数域 FP 可由{0，1，2，3…p-1}中 P 个元素构成，关于 P的模运算称为素数域上模运算。

##### 4.2 有限域上的模运算的设计与实现

有限域上的模运算是 SM2 椭圆曲线公钥密码算法的基础，主要包括模加和模减运算、模乘运算、模幂和模逆运算。模逆运算是模运算中最复杂运算量最大的运算，模逆运算可以通过费马小定理（n 是素数的时候，和 n 互素的某个整数 a 有公式 an-1=1modn 成立）得到，即当 p 为素数时，有ap-1=1mod p，则可得到模逆运算 a-1=ap-2mod p，这样就可以利用模幂运算来表示模逆运算。

##### 4..3 有限域上标量乘运算的设计与实现

标量乘的数学形式，P=（xp，yp）为椭圆曲线E（FP）上的点，k为正整数，P的k倍点为Q。Q=［k］P=P+P+…+P（k个p）。标量乘运算是所有运算中最耗时的运算操作，主要由点加和倍点产生，点加和倍点运算在不同坐标系下的运算规则不同。采用仿射与雅可比混合坐标系下的运算规则：
![enter image description here](https://images.gitbook.cn/df0ad060-7395-11e9-98d2-ebcf245f223d) ，其中，a，b为椭圆曲线上的整数，并且△= ![enter image description here](https://images.gitbook.cn/19a23420-7396-11e9-b02d-058b823f7d15)。

三维坐标P（x1，y1，z1），Q（x2，y2，1）的无穷远点为（1，1，0）。倍点运算P+P=（ x3，y3，z3）声明为Padd1（x1，y1，z1，x3，y3，z3），把2P的值存入（x3，y3，z3），点加运算P+Q=（x3，y3，z3）声明为Padd2（x1，y1，z1，x2，y2，x3，y3，z3），把P+Q的值存入（x3，y3，z3）。最后还要把结果（x3，y3，z3）从雅可比加重摄影坐标系下转换到仿射坐标系下，需要对参数进行转换：x3=x3/z12，y3=y3/z13，即可得到所需的二维坐标点（x3，y3）。

有了点加和倍点运算就可以进行标量乘运算，标量乘从右往左的算法为：输入：点P∈E（Fp）整数k=（k 31k30－k 0）（ki 为 8 位整型数）

输出：Q=［k］P
 初始化Q=O为无穷远点
循环i：0~31
b=k（i b为8位整型数）
循环j：0~7
若（b&1）=1，则Q=Q+P
b=b>>1
P=P+P
返回Q

#### 5. SM2公钥加密算法

素数域椭圆曲线的参数：素数域的模P，椭圆曲线E（FP）的
系数：a，b；E（FP）上的基点G（Gx，Gy）≠0，基点G的解为n余
因子h=1，用户A持有的用户B的公钥PB，用户B持有的私钥dB。

##### 5.1 SM2加密算法

（1）用随机数发生器生成随机数![enter image description here](https://images.gitbook.cn/511015c0-7ac7-11e9-a023-5dfd4cad8c57)
（2）计算椭圆曲线上的点 ![enter image description here](https://images.gitbook.cn/5a7f17f0-7ac7-11e9-bfe0-2d8b1a11ad74)
（3）计算椭圆曲线点 ![enter image description here](https://images.gitbook.cn/64e7e370-7ac7-11e9-a23c-35b15700507e)，若S为无穷远点则报错并退出，h 为余因子，这里取为 1。
（4）计算椭圆曲线上的点![enter image description here](https://images.gitbook.cn/a8f9e220-7ac7-11e9-99f3-43e3454a8bb7)
（5）计算![enter image description here](https://images.gitbook.cn/af24dce0-7ac7-11e9-bfe0-2d8b1a11ad74)，若t全为0则返回1。
（6）计算 ![enter image description here](https://images.gitbook.cn/b91f7d40-7ac7-11e9-a023-5dfd4cad8c57)
（7）计算 ![enter image description here](https://images.gitbook.cn/c0d5d2f0-7ac7-11e9-bfe0-2d8b1a11ad74)。
（8）计算密文![enter image description here](https://images.gitbook.cn/c9029120-7ac7-11e9-bfe0-2d8b1a11ad74)。

##### 5.2. SM2解密算法

（1）从密文中取出 C1，验证C1是否满足椭圆曲线方程，若不满足则报错并退出。
（2）计算![enter image description here](https://images.gitbook.cn/1a2745a0-7ac8-11e9-a023-5dfd4cad8c57)，若S为无穷远点则报错并退出。
（3）计算 ![enter image description here](https://images.gitbook.cn/21efc3c0-7ac8-11e9-bfe0-2d8b1a11ad74)。
（4）计算 ![enter image description here](https://images.gitbook.cn/2867a600-7ac8-11e9-a23c-35b15700507e)。
（5）从 C 中取出 C2 计算 ![enter image description here](https://images.gitbook.cn/2fa7e150-7ac8-11e9-a023-5dfd4cad8c57)
（6）计算![enter image description here](https://images.gitbook.cn/35bac030-7ac8-11e9-a23c-35b15700507e)，若 u 与 C3 不相等，则报错
并退出。
（7）输出明文 m。

#### 6 SM2 代码实现

https://github.com/guoshijiang/NationalSecret


#### 7. SM2 小结

SM2 算法是我国在吸收国际先进成果基础上研发出来的具有自主知识产权的 ECC 算法， 它在安全性和实现效率方面相当于或略优于国 际上同类的 ECC 算法， 能取代 RSA 以满足各种应用对公钥密码算法安全性和实现效率的更高要求， 具有广阔的推广和应用前景。

### 五. SM3 算法原理和代码实战

#### 1. SM3 简介

SM3 密码杂凑算法是中国国家密码管理局年公布的中国商用密码杂凑算法标准。该算法由王小云等人设计，消息分组比特，输出杂凑值比特，采用 Merkle Damgard 结构。密码杂凑算法的压缩函数与的压缩函数具有相似的结构，但是，密码杂凑算法的压缩函数的结构和消息拓展过程的设计都更加复杂，比如压缩函数的每一轮都使用个消息字，消息拓展过程的每一轮都使用个消息字等。

SM3  密码杂凑算法消息分组长度 为 512b, 摘要长度 256b。压缩函数状态 256 b， 共 64 步操作。

#### 2. SM3 的算法描述

##### 2.1. 密码杂凑算法中的常量与函数

初始值： SM3 密码杂凑算法的初始值共 256 b ， 由 8 个 32b 串联构成，
具体值如下 ：
![enter image description here](https://images.gitbook.cn/649a7b10-79e8-11e9-8dec-3dba4995d575)

常量
![enter image description here](https://images.gitbook.cn/69958150-79e8-11e9-91d6-116993cb37bb)

布尔函数
![enter image description here](https://images.gitbook.cn/6ec50510-79e8-11e9-aee1-59a97a37cd88)

上式中的 X，Y 为 32 位的字。

置换函数
![enter image description here](https://images.gitbook.cn/7611ea90-79e8-11e9-91d6-116993cb37bb)

上式中的 X，Y 为 32 位的字。

##### 2.2. SM3 算法描述

对于长度为l(l 小于 2 的 64 次方)比特的消息 M，SM3 密码杂凑算法经过消息填充和迭代压缩，产生杂凑值，杂凑值的长度为 256 比特。

1. 消息填充

假定消息输入的长度为l(l 小于 2 的 64 次方)比特。首先将比特 “1” 添加到消息的末尾，再添加 k 个 “0”，k 是满足 k + l + 1 = 448 mod 512 的最小的非负整数。然后再添加一个 64 位比特串，该比特串是长度 l 的二进制表示。填充后的消息 M 比特长度为 512 倍数。

例如：对消息 01100001 01100010 01100011，其长度 l =24，经填充得到比特串：

![enter image description here](https://images.gitbook.cn/3880e3f0-79ea-11e9-8dec-3dba4995d575)

2. 迭代压縮

迭代压缩是 SM3 密码杂凑算法的主体操作，此步骤产生最终杂凑值。迭代压缩过程可以表述如下：

将消息填充后的消息  M  按 512 比特进行消息分组：![enter image description here](https://images.gitbook.cn/225fcd10-79eb-11e9-aee1-59a97a37cd88)其中： n = (k + 1 + l + 64) / 512

按如下方式迭:

![enter image description here](https://images.gitbook.cn/61aa0a80-79eb-11e9-8dec-3dba4995d575)

其中 CF 是压缩函数， V (0) 为 256 比特初始值 IV，B (i)为填充后的消息分组，迭代压缩的结果为V(n)，同时也是消息 M 的杂凑值。

3.消息拓展

将消息分组 B (i) 按以下方法扩展生成个字 W0，W1  ...  W67； W0'，W1‘ ... W63'，用于压缩函数CF：

![enter image description here](https://images.gitbook.cn/55974310-79ec-11e9-8dec-3dba4995d575)


![enter image description here](https://images.gitbook.cn/5b17cd00-79ec-11e9-8dec-3dba4995d575)![enter image description here](https://images.gitbook.cn/5fb45f90-79ec-11e9-8dec-3dba4995d575)

4.压縮函数

![enter image description here](https://images.gitbook.cn/9fb43160-79ec-11e9-969e-fb1e44586b50)

其中字的存储为大端格式

5.杂凑值

![enter image description here](https://images.gitbook.cn/de678600-79ec-11e9-969e-fb1e44586b50)

输出 256 比特的杂凑值![enter image description here](https://images.gitbook.cn/e4b23dc0-79ec-11e9-969e-fb1e44586b50)

#### 3. SM3 代码实现

https://github.com/guoshijiang/NationalSecret

#### 4. SM3 小结

杂凑函数的设计和应用已经发展了几十余年。自第一个直接构造的杂凑函数诞生以来密码学界普遍认为，构造安全的杂凑函数就是构造抗碰撞的压缩函数。然而，随着王小云等人成功破解 MD5 ，等杂凑函数以后，基于传统 MD 结构设计的杂凑函数被证明是不安全的。因此，对杂凑函数的设计与分析又成为了密码学界的一大研究热点，特别是当前最新的杂凑算法的研宄，推动了研究杂凑函数的高潮。SM3 轮数的研究将会是高潮，减少轮数的 SM3 算法进行随机性分析 32 轮、33 轮、34 轮和 35 轮算法的飞来去器攻击方法。但是如何对更多轮数的算法的原根、碰撞和第二原根进行分析也是需要进一步研究的问题。

### 六. SM4 算法原理和代码实战

#### 1. SM4 简介

SM4  是一种 Feistel  结构的分组密码算法，其分组长度和密钥长度均为128bit。加解密算法与密钥扩张算法都采用 32 轮非线性迭代结构。解密算法与加密算法的结构相同，只是轮密钥的使用顺序相反，即解密算法使用的轮密钥是加密算法使用的轮密钥的逆序。 

#### 2. SM4 算法描述

##### 2.1. 加解密算法描述 

定义 为 e 比特的向量集，<<< i 为 32bit 循环左移 i 位，⊕为 32bit 异或。

现对 SM4 解密算法进行具体介绍。128bit 的明文或密文输入经初始变换分成 4 个字节，与轮密钥经过轮函数的运算经过 32  轮的迭代完成加解密运算。 

设 明 文 输 入 为 ![enter image description here](https://images.gitbook.cn/cb3efb60-79fd-11e9-8dec-3dba4995d575)密 文 输 出 为![enter image description here](https://images.gitbook.cn/d5ecbf20-79fd-11e9-8dec-3dba4995d575)，轮 密 钥 为![enter image description here](https://images.gitbook.cn/e2c440b0-79fd-11e9-91d6-116993cb37bb)，则该算法的加密过程为：

![enter image description here](https://images.gitbook.cn/1ad39a00-79fe-11e9-969e-fb1e44586b50)

在式（1）中， F(.) 称为加密算法的轮函数； T (.)为 ![enter image description here](https://images.gitbook.cn/573f4890-79fe-11e9-91d6-116993cb37bb)  的可逆变换，由非线性变换![enter image description here](https://images.gitbook.cn/7394b390-79fe-11e9-8dec-3dba4995d575)和线性变换 L 复合而成，即 ![enter image description here](https://images.gitbook.cn/91247350-79fe-11e9-91d6-116993cb37bb)。非线性变换 由 4 个并行的 S 盒构成。设输入为 ![enter image description here](https://images.gitbook.cn/ee8e2d60-79fe-11e9-8dec-3dba4995d575)输出为 ![enter image description here](https://images.gitbook.cn/f53b9e90-79fe-11e9-8dec-3dba4995d575)，则 

![enter image description here](https://images.gitbook.cn/ff673a00-79fe-11e9-aee1-59a97a37cd88)                        (3)

其中，![enter image description here](https://images.gitbook.cn/0e00ddf0-79ff-11e9-91d6-116993cb37bb) 为固定的映射表。 

线性变换的输入是非线性变换 的输出。设输入为![enter image description here](https://images.gitbook.cn/6dde0900-79ff-11e9-91d6-116993cb37bb) ，输出为![enter image description here](https://images.gitbook.cn/731247b0-79ff-11e9-969e-fb1e44586b50) ，则： 
                ![enter image description here](https://images.gitbook.cn/7947f0d0-79ff-11e9-8dec-3dba4995d575)    (4)

SMS 解密过程与加密变换结构相同，不同的仅是轮密钥的使用顺序，第一轮使用 ![enter image description here](https://images.gitbook.cn/95154010-79ff-11e9-aee1-59a97a37cd88)，第二轮使用 ![enter image description here](https://images.gitbook.cn/9d277160-79ff-11e9-8dec-3dba4995d575)，依此类推。

##### 2.2. 密钥扩展算法 

该算法中加密算法的轮密钥由加密密钥通过密钥扩展算法生成。  设加密密钥 ![enter image description here](https://images.gitbook.cn/43320110-7a00-11e9-aee1-59a97a37cd88) 。 令 ![enter image description here](https://images.gitbook.cn/4da37f20-7a00-11e9-aee1-59a97a37cd88)，轮密钥为 ![enter image description here](https://images.gitbook.cn/529adbe0-7a00-11e9-91d6-116993cb37bb)，则轮密钥生成方法为：![enter image description here](https://images.gitbook.cn/589f62e0-7a00-11e9-aee1-59a97a37cd88)  (5)

对![enter image description here](https://images.gitbook.cn/7cc4c610-7a00-11e9-aee1-59a97a37cd88) 

![enter image description here](https://images.gitbook.cn/83f8cc60-7a00-11e9-8dec-3dba4995d575)                  （6） 
其中， T* 变换与加密算法轮函数中的 T 变换基本相同，只将其中的线性变换 L 修改为 L*：

![enter image description here](https://images.gitbook.cn/a5805330-7a00-11e9-91d6-116993cb37bb)        (7)

式（5）中的参数 FKi 与式（6）中的参数 CKi 均为固定值。此外， CKi 也可以通过计算得到。 设 ckij 是 CKi 的第 j 个字节，其中 ![enter image description here](https://images.gitbook.cn/0f57a970-7a01-11e9-91d6-116993cb37bb)，即 ![enter image description here](https://images.gitbook.cn/1ac3db30-7a01-11e9-91d6-116993cb37bb) ，则

![enter image description here](https://images.gitbook.cn/255a1f50-7a01-11e9-91d6-116993cb37bb)    (8)

#### 3.  SM4 代码实现

https://github.com/guoshijiang/NationalSecret

#### 4. SM4 小结

SM4 密码算法是中国第一次由专业密码机构公布并设计的商用密码算法，到目前为止，尚未发现有任何攻击方法对SM4 算法的安全性产生威胁。

### 七. 其他国密算法


### 1. SM7

一种分组密码算法。

### 2. SM9 

SM9 是我国采用的一种标识密码标准，由国家密码管理局于2016 年 3 月 28 日发布，相关标准为“GM/T 0044-2016 SM9标识密码算法”。在商用密码体系中，SM9 主要用于用户的身份认证。SM9 算法不需要申请数字证书，适用于互联网应用的各种新兴应用的安全保障。据新华网公开报道，SM9 的加密强度等同于 3072 位密钥的 RSA 加密算法。


### 八. 本文小结

从目前的密码研究技术来看，现有的国密算法的安全性在一段时间内并不会受到任何攻击性危机，但随着密码学技术和量子计算机的发展，未来的国密将会面临更大的挑战，现有国密算法的改进、新的密码算法和抗量子密码学的研究将会成为国密的研究热点。
