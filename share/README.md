# 第 M 章：秘密共享

密码学的发展可以追溯到公元前 400 年前，人类使用密码学的历史几乎和文字的历史一样长。公元前 400 年前，斯巴达人发明了 “塞塔式密码“。在中国古代，也出现过密码学的影子的，中国古代的藏头诗大家应该都知道，这也属于密码学的使用范畴。在密码学的发展过程中，战争起到了很大的作用，从古至今，军方使用的技术都是世界上最先进的，包括密码学也一样。密码学体系在当今时代已经是一个完善的学科体系，全世界有很多专家学者终其一生为密码学的发展添砖加瓦。我们现在所熟知的对称密码，非对称密码，数字签名，单项散列函数，PKI 体系，共享密码等都可以是一个值得深入研究的方向。本文将带领大家去理解共享秘密相关的一些技术，希望大家从中能学到一些共享密码的知识。

### 共享密钥的发展历程

秘密的共享是信息安全研究的一个重要的分支，密码主要是为了对重要信息进行加密，保证信息的安全新，而秘密共享却可以保证密钥的安全性，它为密码学的发展提供了一个崭新的思路。秘密共享的原理是将秘密分成若干份，交给不同的人去保管，设定管理秘密的一定数量的人贡献出自己持有的秘密，就可以恢复秘密了。

#### 1.1秘密共享的产生

秘密共享的概念最早由著名密码学家 Shamir 和 Blakley 于 1979 年分别独立提出并给出了各自的方案。Shamir 的( t，n) 门限方案基于 Lagrnage ( 拉格朗日) 插值法来实现，Blakley 的( t，n) 门限方案是利用多维空间点的性质来建立的。

秘密共享的概念一经提出，受到专家学者们的极大的关注与研究。 这些年取得的成果颇丰。大致可以分为如下几类。

##### **1.1.1 门限秘密共享方案**

在( t，n) 门限秘密共享方案中，任何包含至 少 t 个参与者的集合都是授权子集，而包含 t-1 或更少参与者的集合都是非授权子集，实现( t， n) 门限秘密共享的方法除了 Shamir 和 Blakley 的方案外，还有基于中国剩余定理的 Asmuth-Bloom 法以及使用矩阵乘法的 Karnin-Greene Hellman 方法等。

##### **1.1.2 一般访问结构上秘密共享方案** 

门限方案是实现门限访问结构的秘密共享方案，对于其它更广泛的访问结构存在局限性， 如在 甲 、乙 、丙 、丁 四 个成员中共享秘 密 ，使甲和丁或乙和丙合作能恢复秘密，门限秘密共享方案就不能解决这样的情况. 针对这类问题，1987 年密码学研究人士提出了一般访问结构上的秘密共享方案。1988 年有人又提出了一个更简单有效的方法—单调电路构造法，并且证明了任何访问结构都能够通过完备的秘密共享方案加以实现。

##### **1.1.3 多重秘密共享方案**

只需保护一个子秘密就可以实现多个秘密的共享，在多重秘密共享方案中每个参与者的子秘密可以使用多次，但是一次秘密共享过程只能共享一个秘密。

##### **1.1.4 多秘密共享方案**

多重秘密共享解决了参与者的子秘密重用 的问题，但其在一次秘密共享过程中只能共享一个秘密。

##### **1.1.5 可验证秘密共享方案**

参与秘密共享的成员可以通过公开变量验证自己所拥有的子秘密的正确性，从而有效地防止了分发者与参与者，以及参与者之间的相互欺骗的问题。可验证秘密共享方案分为交互式和非交互式两种。交互式可验证的秘密共享方案是指各个参与者在验证秘密份额的正确性时需要相互之间交换信息；非交互式可验证的秘密共享是指各个参与者在验证秘密份额的正确性时不需要相互之间交换信息。在应用方面，非交互式可验证秘密共享可以减少网络通信费用，降低秘密泄漏的机会，因此应用领域也更加广泛。

##### **1.1.6 动态秘密共享方案**

动态秘密共享方案是 1990 年提出，它具有很好的安全性与灵活性，它允许新增或删除参与者、定期或不定期更新参与者的子秘密以及在不同的时间恢复不同的秘密等等. 以上是几种经典的秘密共享方案. 需要说明的是，一个具体的秘密共享方案往往是几个类型的集合体。

##### **1.1.7 其他秘密共享**

 量子秘密共享、可视秘密共享、 基于多分辨滤波的秘密共享、基于广义自缩序列的秘密共享。

###经典秘密共享方案介绍

#### 2.1 shamir 门限秘密共享方案

Shamir 的( t，n) 门限方案基于 Lagrnage ( 拉格朗日) 插值法来实现，简单地说，设秘密通过秘密共享算法分发给个成员共享，每一个成员持有一个子密钥也称为 shadow 或 Secret debris，如果满足:

*  任何不少于 t 个的有效成员使用他持有的正确的碎片都可以恢复秘密。 
*  任何 t 个以下的成员集都无法恢复秘密。

我们称这种方案为 (t ,n) 门限秘密共享方案，简称为门限方案，t 称为方案的门限值。

作为各种秘密共享方案中最简单实用的门限秘密共享方案，(k,n) 门限秘密共享方案也是这些方案中最具有代表性和广泛应用的方案。

下面简单介绍一下这个方案。

##### **2.1.1 系统参数**

假定 n 是参与者的数目，n 是门限值，p 是一个大素数要求 p > n 并且大于 p 秘密 s 的可能的最大取值;秘密空间与份额空间均为有限域 GF(p)。

##### **2.1.2 秘密分发**

秘密分发者 D 给 n 个参与者 Pi(0 ≤ i ≤ n) 分配份额的过程，即方案的分配算法如下:

* 随机选择一个 GF(p) 上的 k - 1 次多项式 使得 f(0) = a0 = s要在个参与者中分享的秘密 D 对 f(x) 保密。

* D 在 Zp 中选择 n 个互不相同的非零元素 x1, x2, …, xn，计算 (0≤ i ≤ n)。 

* 将 ( xi , yi ) 分配给参与者 Pi( 0 ≤ i ≤ n)，值 xi 是公开的，yi 作为的秘密份额，不公开。 

##### **2.1.3  秘密重构**

给定任何 t 个点,不妨设为前 t 个点（x1， y1），(x2,  y2)，…, (xt, yt)。由插值公式：

![enter image description here](https://images.gitbook.cn/597d0a10-3de6-11e9-83a7-c387b6fac45c)

Shamir 方案作为一种被广泛选用的门限方案，具有以下优点：

* t 个秘密份额可以确定出整个多项式，并可计算出其他的秘密份额。 

* 在原有分享者的秘密份额保持不变的情况下，可以增加新的分享者，只要增加后分享者的总数不超过。

* 还可以在原有共享密钥未暴露之前，通过构造常数项仍为共享密钥的具有新系数的次多项式，重新计算新一轮分享者的秘密份额，从而使得分享者原有的秘密份额作废。

但同时方案存在以下问题

* 在秘密分发阶段，不诚实的秘密分发者可分发无效的秘密份额给参与者

* 在秘密重构阶段，某些参与者可能提交无效的秘密份额使得无法恢复正确秘。 

* 秘密分发者与参与者之间需点对点安全通道。

#### 2.2 基于中国剩余定理的秘密共享方案

中国剩余定理最早出现在我国古代数学名著《孙子算经》中，因而又被称为孙子定理，中国剩余定理在密码学中被广泛的使用。

令 p1, p2,...,pm 表示 m 个两两互素的正整数。给定任意 m 个整数，k1,k2,k3,...,km，存在唯一的一个整数 K 属于 GF(p1p2 ..., pm)满足：


	K = K1 mod p1
	K = K2 mod P2
	......
	K = Km mod Pm

1983 年，密码学专家提出两一种基于中国剩余定理的秘密共享方案，整体思路如下。

##### **2.2.1 初始化阶段**

设 P = {p1, p2, ... , Pn} 为参与者的集合。{p, d1, d2, ... dn} 是一组满足下列条件的整数。

* s < p, s 是需要共享的密明。
* d1 < d2 < ... dn。
* 对i = 1,2, ... , n, 有 gcd(di, p) = 1，其中 gcd(x, y) 表示 x 和 y 的最大公约数。
* 对于所有 i 不等于 j，有 gcd(di, dj) = 1。
* d1d2...dk > pdn-t+2dn-k+3 ... dn。

其中第 5 条意味着最小的 k 个 di 的乘积要大于 p 和 k—1 个最大的di之积。

##### **2.2.2 密明分发阶段**
令 N = d1d2...dt，则 N/p 大于任意的 k-1 个 di 之积。令 r 是 [0, N/p-1] 中一个随机数。为了将密明 s 分割为 n 份，密朗分发者 D 计算 s' = s + rp，这里将 s' 限制在 [0, N - 1] 中，则每个参与者 Pi 的子密钥 xi 为：

	xi = s' mod (di)


##### **2.2.3 密钥重构阶段**

任意 k 个参与者，不妨假设为 P1, P2, ... Pk 拿出他们的 k 个子密钥 x1, x2, ... xk，由中国剩余定理可得到对应的模：

	N1 = d1d2 ... dk

因为 N1 大于等于 N，可由中国剩余定理唯一的确定 s'。而后可由 s', r, p 计算出密钥：

	s = s' - rp
	

如果仅仅知道 k-1 个子密朗，虽然由N2可知s'，
	
	N2 = d1d2 ... dk-1
但由于 N/N2 > p，且gcd(N2, p) = 1，所以使 x 大于等于 N 和 x=s'mod(p) 的数 x 在模 p 下的同余类上均匀分布，因此没有足够的信息决定s'。在该方案中，密钢恢复算法的时间复杂度为O(k)，空间复杂度为O(n)。

### 可验证秘密共享

通常的密钥共享方案，都假设密钥分发者是诚实的。这会导致基本密钥共享中存在一个主要的安全问题：不能防止密钥分发者的欺骗，即分发者在分发子密钥时可能会给一个或者多个参与者分发伪造的子密钥。为了解决这个问题，Chor 等人提出了可验证密钥共享的概念。可验证密钥共享就是把一个普通的密明共享方案附加上一个允许参与者认证他们收到的子密钥的交互式算法，参与者可通过认证算法检验自己的子密明是否有效。可验证密钥共享可以分为条件安全可验证密明共享和无条件安全可验证密钥共享两大类。下面我们介绍几个比较有代表性可验证秘密共享方案。

#### 3.1 Feldman 的方案

Feldman 在 Shamir 的密钥共享方案基础上提出了一种可验证的密朗共享方案。下面我们介绍一下这个算法的详细过程：

##### **3.1.1 初始化阶段**

设 p 是一个大素数，q 为 p -1 的一个大素数因子，g 属于 Z*p 且为 q 阶元素，三元组 (p, q, g) 是公幵的，k 是门限值，n 是参与者的数目，s 为要共享的密钥。

##### **3.1.2 子密明分发阶段**

密朗分发者（dealer）选取一个 k-1 次的随机多项式 f(x) 属于 Zq(x)，并使得 f(0) = s。即在 Zq 任意选取个随机数 a1, a2, ..., ak-1，构造多项式

![enter image description here](https://images.gitbook.cn/2a7642d0-3e50-11e9-acbf-6f04514d907d)

随后，计算并密销发送子密钥 mi = f(i) mod (q) 给参与者 Pi，并且广播验证信息。
![enter image description here](https://images.gitbook.cn/416e3c40-3e50-11e9-acbf-6f04514d907d)。


##### **3.1.3 验证阶段**

参与者Pi（i = 1, 2, ..., n）在收到子密钥之后，可通过检查等式

![enter image description here](https://images.gitbook.cn/821f35a0-3e50-11e9-acbf-6f04514d907d)

是否成立来验证子密朗的正确性。若等式成立相等则说明参与者Pi拥有的子密明是正确的，否则说明收到的子密销是不正确的。

##### **3.1.4 密明恢复阶段**

当 k 个参与者，不妨假设为 P1, P2, ..., Pn 合作恢复密朗时，每一个参与者 Pi 都要公开他的子密钥份额 mi。此时任何一个参与者都可以通过验证上述等式来验证其他参与者的子密钥的正确性。若经检验，所有公开的子密朗都是正确的，那么密钥可以由拉格朗日插值函数来恢复。

可以看到，在 Feldman 的方案中，验证子密朗的正确性的关键是密钥分发者公布了验证信息 aj = gaj mod p，j = 1, 2, 3, ..., k。其中 g 与 p 是公幵的，验证信息 aj 是 aj 的离散对数。基于离散对数问题的困难性，由验证信息 aj 和 (g, p) 无法计算出。由此可见，Feldman 的方案的安全性是建立在离散对数问题的困难性基础上的，所以它是条件安全的。另外，从密钥恢复的阶段我们还可以看到，当参与者公开自己的子密钥后，所有的参与者都能够利用密钥分发阶段的信息来验证其他参与者的子密钢的正确性，这实际上是解决了参与者在密朗恢复过程中的欺骗问题。

#### 3.2 Benaloh 方案

Benaloh 的可验证密明共享方案也是建立在 Shamir 的密朗共享方案基础上的。与 Feldman 的方案不同，Benaloh 的方案是无条件安全的。首先我们介绍一下 Benaloh 的可验算法的主要思路。在的密钥共享方案中，所有的参与者的子密明都是来自一个 k - 1 次的线性多项式，如果密钥分发者分发出一个或者多个错误的子密钥，那么这些 n 个子密钥必然会不一致，它们的插值多项式的次数在很大的概率上会大于 k -1。换句话说，如果我们能过在不泄露子密钥信息的前提下得出这些子密明的插值多项式的次数，那么就可以验证出子密朗的有效性。Benaloh 的方案正是利用这一性质对 Shamir 的密钥共享方案进行了验证，具体的算法如下：

##### **3.2.1 初始化阶段**

设 q 是一个大素数，s 属于 Zq 是将要分享的密钥。k 是门限值，n 是参与者的数目。

##### **3.2.2 子密钥分发阶段**

密钥分发者 (dealer) 选取一个 k -1 次的随机多项式 f(x) = Zq(x)，并使得 f(0) = s。随后，计算并密明发送子密钥mi = f(i) mod (q)给参与者 Pi。

接下来密钥分发者又随机选择多个 (不妨假设为 100) Zq(x) 上的 k-1 次多项式，f1(x), f2(x), ..., f100(x)。并且为每一位参与者 Pi 计算并且发送 100 个验证子密钥mij（mij 表示 mi 的 j 次方），j = 1, 2, … 100，其中。mij = fj(i)。

##### **3.2.3 验证阶段**

所有参与者合作随机选取 50 组（一组包含 n 个）验证子密钥，将其公开后分别验证这 50 组验证子密朗是否都是出自 k-1 次的多项式。由于这 50 组验证子密钥是由参与者随机选取，如果它们全都源于 k-1 次的多项式，那么参与者可以认为剩下的 50 组未公开的子密钥也都来源于是 k-1 次的多项式。

接下来，所有参与者将子密朗与剩下的任意一个未公开的验证子密钥的和公开，并且验证这 n 个值是否来源于 k-1 次的多项式。如果是，那么根据插值多项式的线性性质可以推断出这个 n 子密明也是来源于一个 k-1 次的多项式。从而验证出子密钥的有效性。反之，这个子密明是不一致的，密朗分发者在计算和分发子密朗的过程中出错。

##### **3.2.4  密钥恢复阶段**

当子密钥的有效性被验证过后，任意 k 个参与者利用拉格朗日插值公式可以将密钥恢复出来。


由以上的算法我们可以看到，在 Benaloh 的方案中，密钥分发者没有公布任何验证信息，而整个验证算法也没有依靠任何困难问题假设，所以 Benaloh  的可验证密钥共享方案是无条件安全的。但是，每个参与者为了要验证子密钥的有效性，他们要存储 100 个验证子密钥，这就对每个参与者的存储空间提出了很高的要求。另外，从验证的效果上来分析，Benaloh  的方案只能够验证出是否存在错误的子密朗，却无法判断哪一个子密钥是错误的。相对于 Feldman 的方案，该方案在验证的效果上是要弱一些，并且参与者需要更大的存储空间，这会引起一定程度的安全问题。不过这也是达到无条件安全所必须要付出的代价。


### 去中心化秘密共享方案

自从密钥共享方案诞生以来，大量的不同环境下的密钥共享方案己经被提了出来。大部分的方案中都假设存在一个可信中心密钥分发者，负责将密钥分割成为子密钥，并且安全密钥的将子密钢发送给参与者。但是在实际环境中，可信中心往往是不存在的。所以一种新的无可信中心的密胡共享协议被提了出来以适应没有可信中心的环境。

在无可信中心的密钥共享中，子密朗的产生和分配都是由参与者本身合作完成的。在实际应用中，有可信中心的密朗共享可能存在可信中心的“权威欺骗”，并且在现实中需要成员具有较高的可信度也不是明智的假设。因此，和有可信中心的密钥共享相比，无可信中心的密钥共享安全性更高，实用性更强。

对无可信中心密钥共享研究的主要目的就是：寻找合适的方案来保证信息能够安全，有效地发布和传输。此外，无可信中心密明共享中的子密钥如何分发，是人们研究的热点问题，其发展空间还很大。因此，无可信中心密钥共享不仅存在着重要的理论价值，更在实际应用中存在着广泛的应用前景。目甜对于无可信中心的密明共享的应用主要集中在数字签名方面。对无可信中心的密明共享的加密研究并不多。下面是笔者个人提出的一种去中心化秘密共享方案。

去中心的化密钥共享方案实际上就是把密钥拆分成 n 份之后，对每一份秘密进行加密，然后将他们存储到区块链上去，这样可以解决密钥的分发存储。密钥发送到相应的节点后，该节点先对密钥做二次加密，签名，然后写到区块链上，当密钥恢复者需要恢复密钥时，它可以全网广播一条恢复密钥的信息，然后付给密钥段存储节点一定的  token，密钥存储节点验证密钥并解密之后发送给恢复密钥的客户端。这样就可以达到去中心的秘密共享的目标。

###（t，n）门限的动态秘密共享方案

1979 年 Shamir 和 Blakley 分别提出了一个（t，n）门限秘密共享方案，Shamir 的（t，n）门限方案是基于 Lagrange（拉格朗日）插值法来实现的，它通过构造一个 t-1 次多项式，并将需要共享的秘密作为该多项式的常数项，每个份额（子秘密）为满足该多项式的一个坐标点，由 Lagrange 插值定理可知，任意 t 个份额（子秘密）可以重构该多项式从而恢复秘密，而 t-1 个或更少的份额（子秘密）不能重构该多项式，因而得不到关于秘密的任何信息。

动态秘密共享体制的提出主要源于秘密共享方案的安全性问题。在（t，n）门限秘密共享方案中，方案的安全性是建立在攻击者不可能在秘密的生命周期内获取 t 个子秘密的前提之下的。然而实际上很难保证这一点，尤其是在秘密的生命周期较长的情况下，这一点就更难以保证。可验证秘密共享方案主要用来解决传统秘密共享方案中存在的分发者不诚实性问题和子秘密持有者的不诚实性问题，而面对敌手的破坏性攻击，可验证秘密共享方案并没有更好的安全性。

当然，对于周期上的安全性，可以通过不断更换秘密的办法得到解决，但是更换秘密并不总是可行的（比如说该秘密是一个重要文件或是一些军事、商业秘密等）。动态秘密共享方案通过在不改变秘密的情况下解决了秘密共享方案在周期上的安全性问题。动态秘密共享方案在保证秘密不变的情况下周期性地更换子秘密，从而使得每次更换子秘密时攻击者在前一个周期内所获得的信息完全失效。

这样一来，就可以根据可能受攻击程度的不同来相应地决定子秘密更换周期的长短，以保证在每一个周期内秘密的安全性。动态秘密共享还要保证过期的子秘密所包含的信息不会对未来秘密的构造产生不安全的影响。

####5.1 Amir Herzberg 方案

有关动态秘密共享的方案已有不少，Amir Herzberg 提出的方案是很经典的一个，方案是对 Shamir 的秘密共享方案实现动态化。

分发者 D 选择一个有限域 GF(q)（q 为大素数），为了方便说明，用 i 代替 Shamir 方案中的 xi的。在第 k 个时段，Pi 持有的子秘密用 si(k)(si 的 k 次方) 表示。

子秘密更新协议：每个时段开始时要进行子秘密更新，进入第 k 时段后，Pi 持有的子秘密要从 si(k-1) =f(k-1)（i）更新至 si(k) ，其中 f(k-1) (0) = s。整个过程如下：

   ![enter image description here](https://images.gitbook.cn/a3e42e10-3e65-11e9-b565-378070432200)

更新后的子秘密显然符合门限秘密共享的要求，任意大于或等于 t 个参与者利用 Lagrange 插值法可恢复秘密。之后 Amir Herzberg 等人在他们的这篇文章中进一步提出了一个防止主动攻击的子秘密更新方案，并增加了可验证性，进一步加强了方案的安全性。

#### 5.2 Amir Herzberg 方案的改进

事实上 Amir Herzberg 的子秘密更新方案相当于 n 个参与者协商了一个常数项为零的 t-1 次多项式，事实上少于 n 个参与者也可以进行子秘密更新，步骤和原方案相同，如果参与子秘密更新的参与者少于门限值 t 时，可以对此方案进行改进，使它具有更好的灵活性和执行效率，方案描述如下：
![enter image description here](https://images.gitbook.cn/edf6bc20-3e65-11e9-9e3c-c5b76bc0f4a1)

##### **5.2.1 Amir Herzberg 方案的改进分析**

![enter image description here](https://images.gitbook.cn/32725210-3e66-11e9-9e3c-c5b76bc0f4a1)

这样 k（k<t）个参与者就实现了子秘密的更新，并且这个方案有很大的灵活性，在步骤（3）中，只需对 si′=si+χ·i ic 中 i 的次数进行修改，使次数大于 t-k 就可以提高门限值，如 si′=si+χ·iit-k+θ，方案中的门限值就是 t+θ，这相当于把储存秘密 s 的多项式变为 t+θ-1 次多项式。由于参与子秘密更新的成员只需选择一随机数，并进行简单的直和分解运算，与原方案相比执行效率很高。由于传递信息是通过安全信道，安全性可以得到保证。Amir Herzberg 的子秘密更新方案相当于 n 个参与者协商了一个常数项为零的 t-1 次多项式，给出参与子秘密更新的参与者少于门限值 t 也可以进行子秘密更新，并具有更好的灵活性和执行效率。进一步考虑，对于参与子秘密更新的人数大于或等于门限值时，即 k≥t 时，此方案仍可以更新子秘密，但是门限值却会发生变化，不太适合需要保持门限值不变的场合，没有 k<t 时方案更加灵活。

###  门限密钥共享代码实现（Java）

#### 6.1 代码的 pom 文件
```
	<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
		<modelVersion>4.0.0</modelVersion>
		<groupId>cn.beeKey.cryptography</groupId>
		<artifactId>beeKey</artifactId>
		<version>0.1</version>
		<packaging>jar</packaging>
	
		<dependencies>
			<dependency>
				<groupId>junit</groupId>
				<artifactId>junit</artifactId>
				<version>4.8.2</version>
				<type>jar</type>
				<scope>test</scope>
			</dependency>
		</dependencies>
	
		<build>
			<defaultGoal>package</defaultGoal>
		    <finalName>${project.artifactId}-${project.version}</finalName>
			<plugins>
				<plugin>
					<groupId>org.apache.maven.plugins</groupId>
					<artifactId>maven-compiler-plugin</artifactId>
					<version>2.3.2</version>
					<configuration>
						<source>1.7</source>
						<target>1.7</target>
						<encoding>UTF-8</encoding>
					</configuration>
				</plugin>
			</plugins>
		</build>
	
		<properties>
			<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		</properties>
	
	
		<name>Threshold Secret Sharing</name>
		<url></url>
		<description>Threshold Secret Sharing Impl</description>
		<scm>
			<url></url>
			<developerConnection>guoshijiang2012@163.com</developerConnection>
		</scm>
		<issueManagement>
			<url></url>
		</issueManagement>
	</project>
```
#### 6.2 核心代码
```
	package cn.beeKey.cryptography.core;
	
	import java.util.Arrays;
	import java.util.Random;
	
	public class ThresholdSecretSharing {
		public final static int MAX_SECRET_BYTES = 65536;
		public final static int MAX_SHARES = 255;
		private static int[] EXP_OP = { 0x01, 0x03, 0x05, 0x0f, 0x11, 0x33, 0x55, 0xff, 0x1a, 0x2e, 0x72, 0x96, 0xa1, 0xf8, 0x13, 0x35, 0x5f, 0xe1, 0x38, 0x48,
				0xd8, 0x73, 0x95, 0xa4, 0xf7, 0x02, 0x06, 0x0a, 0x1e, 0x22, 0x66, 0xaa, 0xe5, 0x34, 0x5c, 0xe4, 0x37, 0x59, 0xeb, 0x26, 0x6a, 0xbe, 0xd9, 0x70,
				0x90, 0xab, 0xe6, 0x31, 0x53, 0xf5, 0x04, 0x0c, 0x14, 0x3c, 0x44, 0xcc, 0x4f, 0xd1, 0x68, 0xb8, 0xd3, 0x6e, 0xb2, 0xcd, 0x4c, 0xd4, 0x67, 0xa9,
				0xe0, 0x3b, 0x4d, 0xd7, 0x62, 0xa6, 0xf1, 0x08, 0x18, 0x28, 0x78, 0x88, 0x83, 0x9e, 0xb9, 0xd0, 0x6b, 0xbd, 0xdc, 0x7f, 0x81, 0x98, 0xb3, 0xce,
				0x49, 0xdb, 0x76, 0x9a, 0xb5, 0xc4, 0x57, 0xf9, 0x10, 0x30, 0x50, 0xf0, 0x0b, 0x1d, 0x27, 0x69, 0xbb, 0xd6, 0x61, 0xa3, 0xfe, 0x19, 0x2b, 0x7d,
				0x87, 0x92, 0xad, 0xec, 0x2f, 0x71, 0x93, 0xae, 0xe9, 0x20, 0x60, 0xa0, 0xfb, 0x16, 0x3a, 0x4e, 0xd2, 0x6d, 0xb7, 0xc2, 0x5d, 0xe7, 0x32, 0x56,
				0xfa, 0x15, 0x3f, 0x41, 0xc3, 0x5e, 0xe2, 0x3d, 0x47, 0xc9, 0x40, 0xc0, 0x5b, 0xed, 0x2c, 0x74, 0x9c, 0xbf, 0xda, 0x75, 0x9f, 0xba, 0xd5, 0x64,
				0xac, 0xef, 0x2a, 0x7e, 0x82, 0x9d, 0xbc, 0xdf, 0x7a, 0x8e, 0x89, 0x80, 0x9b, 0xb6, 0xc1, 0x58, 0xe8, 0x23, 0x65, 0xaf, 0xea, 0x25, 0x6f, 0xb1,
				0xc8, 0x43, 0xc5, 0x54, 0xfc, 0x1f, 0x21, 0x63, 0xa5, 0xf4, 0x07, 0x09, 0x1b, 0x2d, 0x77, 0x99, 0xb0, 0xcb, 0x46, 0xca, 0x45, 0xcf, 0x4a, 0xde,
				0x79, 0x8b, 0x86, 0x91, 0xa8, 0xe3, 0x3e, 0x42, 0xc6, 0x51, 0xf3, 0x0e, 0x12, 0x36, 0x5a, 0xee, 0x29, 0x7b, 0x8d, 0x8c, 0x8f, 0x8a, 0x85, 0x94,
				0xa7, 0xf2, 0x0d, 0x17, 0x39, 0x4b, 0xdd, 0x7c, 0x84, 0x97, 0xa2, 0xfd, 0x1c, 0x24, 0x6c, 0xb4, 0xc7, 0x52, 0xf6, 0x01, 0x03, 0x05, 0x0f, 0x11,
				0x33, 0x55, 0xff, 0x1a, 0x2e, 0x72, 0x96, 0xa1, 0xf8, 0x13, 0x35, 0x5f, 0xe1, 0x38, 0x48, 0xd8, 0x73, 0x95, 0xa4, 0xf7, 0x02, 0x06, 0x0a, 0x1e,
				0x22, 0x66, 0xaa, 0xe5, 0x34, 0x5c, 0xe4, 0x37, 0x59, 0xeb, 0x26, 0x6a, 0xbe, 0xd9, 0x70, 0x90, 0xab, 0xe6, 0x31, 0x53, 0xf5, 0x04, 0x0c, 0x14,
				0x3c, 0x44, 0xcc, 0x4f, 0xd1, 0x68, 0xb8, 0xd3, 0x6e, 0xb2, 0xcd, 0x4c, 0xd4, 0x67, 0xa9, 0xe0, 0x3b, 0x4d, 0xd7, 0x62, 0xa6, 0xf1, 0x08, 0x18,
				0x28, 0x78, 0x88, 0x83, 0x9e, 0xb9, 0xd0, 0x6b, 0xbd, 0xdc, 0x7f, 0x81, 0x98, 0xb3, 0xce, 0x49, 0xdb, 0x76, 0x9a, 0xb5, 0xc4, 0x57, 0xf9, 0x10,
				0x30, 0x50, 0xf0, 0x0b, 0x1d, 0x27, 0x69, 0xbb, 0xd6, 0x61, 0xa3, 0xfe, 0x19, 0x2b, 0x7d, 0x87, 0x92, 0xad, 0xec, 0x2f, 0x71, 0x93, 0xae, 0xe9,
				0x20, 0x60, 0xa0, 0xfb, 0x16, 0x3a, 0x4e, 0xd2, 0x6d, 0xb7, 0xc2, 0x5d, 0xe7, 0x32, 0x56, 0xfa, 0x15, 0x3f, 0x41, 0xc3, 0x5e, 0xe2, 0x3d, 0x47,
				0xc9, 0x40, 0xc0, 0x5b, 0xed, 0x2c, 0x74, 0x9c, 0xbf, 0xda, 0x75, 0x9f, 0xba, 0xd5, 0x64, 0xac, 0xef, 0x2a, 0x7e, 0x82, 0x9d, 0xbc, 0xdf, 0x7a,
				0x8e, 0x89, 0x80, 0x9b, 0xb6, 0xc1, 0x58, 0xe8, 0x23, 0x65, 0xaf, 0xea, 0x25, 0x6f, 0xb1, 0xc8, 0x43, 0xc5, 0x54, 0xfc, 0x1f, 0x21, 0x63, 0xa5,
				0xf4, 0x07, 0x09, 0x1b, 0x2d, 0x77, 0x99, 0xb0, 0xcb, 0x46, 0xca, 0x45, 0xcf, 0x4a, 0xde, 0x79, 0x8b, 0x86, 0x91, 0xa8, 0xe3, 0x3e, 0x42, 0xc6,
				0x51, 0xf3, 0x0e, 0x12, 0x36, 0x5a, 0xee, 0x29, 0x7b, 0x8d, 0x8c, 0x8f, 0x8a, 0x85, 0x94, 0xa7, 0xf2, 0x0d, 0x17, 0x39, 0x4b, 0xdd, 0x7c, 0x84,
				0x97, 0xa2, 0xfd, 0x1c, 0x24, 0x6c, 0xb4, 0xc7, 0x52, 0xf6 };
		private static int[] LOG_OP = { 0x00, 0x00, 0x19, 0x01, 0x32, 0x02, 0x1a, 0xc6, 0x4b, 0xc7, 0x1b, 0x68, 0x33, 0xee, 0xdf, 0x03, 0x64, 0x04, 0xe0, 0x0e,
				0x34, 0x8d, 0x81, 0xef, 0x4c, 0x71, 0x08, 0xc8, 0xf8, 0x69, 0x1c, 0xc1, 0x7d, 0xc2, 0x1d, 0xb5, 0xf9, 0xb9, 0x27, 0x6a, 0x4d, 0xe4, 0xa6, 0x72,
				0x9a, 0xc9, 0x09, 0x78, 0x65, 0x2f, 0x8a, 0x05, 0x21, 0x0f, 0xe1, 0x24, 0x12, 0xf0, 0x82, 0x45, 0x35, 0x93, 0xda, 0x8e, 0x96, 0x8f, 0xdb, 0xbd,
				0x36, 0xd0, 0xce, 0x94, 0x13, 0x5c, 0xd2, 0xf1, 0x40, 0x46, 0x83, 0x38, 0x66, 0xdd, 0xfd, 0x30, 0xbf, 0x06, 0x8b, 0x62, 0xb3, 0x25, 0xe2, 0x98,
				0x22, 0x88, 0x91, 0x10, 0x7e, 0x6e, 0x48, 0xc3, 0xa3, 0xb6, 0x1e, 0x42, 0x3a, 0x6b, 0x28, 0x54, 0xfa, 0x85, 0x3d, 0xba, 0x2b, 0x79, 0x0a, 0x15,
				0x9b, 0x9f, 0x5e, 0xca, 0x4e, 0xd4, 0xac, 0xe5, 0xf3, 0x73, 0xa7, 0x57, 0xaf, 0x58, 0xa8, 0x50, 0xf4, 0xea, 0xd6, 0x74, 0x4f, 0xae, 0xe9, 0xd5,
				0xe7, 0xe6, 0xad, 0xe8, 0x2c, 0xd7, 0x75, 0x7a, 0xeb, 0x16, 0x0b, 0xf5, 0x59, 0xcb, 0x5f, 0xb0, 0x9c, 0xa9, 0x51, 0xa0, 0x7f, 0x0c, 0xf6, 0x6f,
				0x17, 0xc4, 0x49, 0xec, 0xd8, 0x43, 0x1f, 0x2d, 0xa4, 0x76, 0x7b, 0xb7, 0xcc, 0xbb, 0x3e, 0x5a, 0xfb, 0x60, 0xb1, 0x86, 0x3b, 0x52, 0xa1, 0x6c,
				0xaa, 0x55, 0x29, 0x9d, 0x97, 0xb2, 0x87, 0x90, 0x61, 0xbe, 0xdc, 0xfc, 0xbc, 0x95, 0xcf, 0xcd, 0x37, 0x3f, 0x5b, 0xd1, 0x53, 0x39, 0x84, 0x3c,
				0x41, 0xa2, 0x6d, 0x47, 0x14, 0x2a, 0x9e, 0x5d, 0x56, 0xf2, 0xd3, 0xab, 0x44, 0x11, 0x92, 0xd9, 0x23, 0x20, 0x2e, 0x89, 0xb4, 0x7c, 0xb8, 0x26,
				0x77, 0x99, 0xe3, 0xa5, 0x67, 0x4a, 0xed, 0xde, 0xc5, 0x31, 0xfe, 0x18, 0x0d, 0x63, 0x8c, 0x80, 0xc0, 0xf7, 0x70, 0x07 };
	
		private int add(int a, int b) {
			return a ^ b;
		}
	
		private int mul(int x, int y) {
			if (x == 0 || y == 0)
				return 0;
			int v = LOG_OP[0xff & x] + LOG_OP[0xff & y];
			assert v >= 0 && v < 512;
			return EXP_OP[v];
		}
	
		private int div(int x, int y) {
			if (x == 0)
				return 0;
			if (y == 0)
				throw new IllegalArgumentException("division by 0");
			int v = 0xff + LOG_OP[0xff & x] - LOG_OP[0xff & y];
			assert v >= 0 && v < 512;
			return EXP_OP[v];
		}
	
		public byte[][] createShares(byte[] secret, int shares, int threshold, Random rnd) {
			if (secret == null)
				throw new IllegalArgumentException("null secret");
			int m = secret.length;
			if (m == 0)
				throw new IllegalArgumentException("invalid secret length: 0");
			if (m > MAX_SECRET_BYTES)
				throw new IllegalArgumentException("invalid secret length: " + m + "(gt " + MAX_SECRET_BYTES + " bytes)");
			if (shares < 1)
				throw new IllegalArgumentException("not enought shares: " + shares);
			if (shares > MAX_SHARES)
				throw new IllegalArgumentException("too many shares: " + shares + "(gt" + MAX_SHARES + ")");
			if (threshold > shares)
				throw new IllegalArgumentException("threshold > shares: " + threshold + " > " + shares);
			byte[][] share = new byte[shares][m + 1];
			for (int i = 0; i < shares; i++)
				share[i][0] = (byte) (i + 1);
	
			byte[] a = null;
			try {
				a = new byte[threshold];
				for (int i = 0; i < m; i++) {
					rnd.nextBytes(a);
					a[0] = secret[i];
					for (int j = 0; j < shares; j++)
						share[j][i + 1] = (byte) eval(share[j][0], a);
				}
			} finally {
				if (a != null)
					Arrays.fill(a, (byte) 0);
			}
			return share;
		}
	
		private int eval(byte x, byte[] a) {
			assert x != 0;
			assert a.length > 0;
			int r = 0;
			int xi = 1;
			for (byte b : a) {
				r = add(r, mul(b, xi));
				xi = mul(xi, x);
			}
			return r;
		}
	
		public byte[] recoverSecret(byte[]... shares) {
			if (shares == null)
				throw new IllegalArgumentException("null shares");
			int threshold = shares.length;
			if (threshold == 0)
				throw new IllegalArgumentException("not enought shares:" + threshold);
			if (threshold > MAX_SHARES)
				throw new IllegalArgumentException("too many shares:" + threshold);
			int m = shares[0].length - 1;
			if (m <= 0)
				throw new IllegalArgumentException("invalid share length:" + (m + 1) + " (<=0)");
			if (m > MAX_SECRET_BYTES)
				throw new IllegalArgumentException("invalid share length:" + (m + 1) + " (>" + (MAX_SECRET_BYTES + 1) + ")");
	
			for (int i = 1; i < shares.length; i++) {
				if (shares[i] == null)
					throw new IllegalArgumentException("share " + i + " is null");
				if (shares[i].length != m + 1)
					throw new IllegalArgumentException("shares are not equal length, inconsistent input");
	
			}
			byte[] u = null;
			byte[] v = null;
			try {
				u = new byte[threshold];
				for (int i = 0; i < threshold; i++) {
					u[i] = shares[i][0];
					if ((0xff & u[i]) == 0)
						throw new IllegalArgumentException("invalid share index: " + shares[i][0]);
					for (int j = 0; j < i; j++)
						if (u[i] == u[j])
							throw new IllegalArgumentException("duplicated share index: " + u[i]);
	
				}
				byte[] secret = new byte[m];
				v = new byte[threshold];
				for (int j = 0; j < m; j++) {
					for (int i = 0; i < threshold; i++)
						v[i] = shares[i][j + 1];
					secret[j] = (byte) lagrange(u, v);
				}
				return secret;
			} finally {
				if (u != null)
					Arrays.fill(u, (byte) 0);
				if (v != null)
					Arrays.fill(v, (byte) 0);
			}
		}
	
		private int poly(int i, byte[] u) {
			int r = 1;
			for (int j = 0, m = u.length; j < m; j++)
				if (j != i)
					r = mul(r, div(u[j], add(u[j], u[i])));
			return r;
		}
	
		private int lagrange(byte[] u, byte[] v) {
			int m = u.length;
			assert m == v.length;
			int r = 0;
			for (int i = 0; i < m; i++)
				r = add(r, mul(poly(i, u), v[i]));
			return r;
		}
	}
```
#### 6.3 代码的工具类

##### **6.3.1  Combination 代码**
```
	package cn.beeKey.cryptography.util;
	
	import java.util.Arrays;
	import java.util.Iterator;
	import java.util.NoSuchElementException;
	
	public class Combination implements Iterable<int[]> {
		private final int n;
		private final int k;
		private final int[] data;
	
		public Combination(int n, int k) {
			if (n < 0)
				throw new IllegalArgumentException("n<0");
			if (k < 0)
				throw new IllegalArgumentException("k<0");
			if (n < k)
				throw new IllegalArgumentException("n<k");
			this.n = n;
			this.k = k;
			this.data = new int[k];
			for (int i = 0; i < k; ++i)
				this.data[i] = i;
		}
	
		public Combination(int n, int k, int[] a) {
			if (k != a.length)
				throw new IllegalArgumentException("Array length does not equal k");
	
			this.n = n;
			this.k = k;
			this.data = new int[k];
			for (int i = 0; i < a.length; ++i)
				this.data[i] = a[i];
	
			if (!isValid())
				throw new IllegalArgumentException("Bad value from array");
		}
	
		private boolean isValid() {
			if (this.data.length != this.k)
				return false;
	
			for (int i = 0; i < this.k; ++i) {
				if (this.data[i] < 0 || this.data[i] > this.n - 1)
					return false;
	
				for (int j = i + 1; j < this.k; ++j)
					if (this.data[i] >= this.data[j])
						return false;
			}
	
			return true;
		}
	
		@Override
		public String toString() {
			return "{" + Arrays.toString(data) + "}";
		}
	
		public Combination sucessor() {
			if (this.data[0] == this.n - this.k)
				return null;
	
			Combination ans = new Combination(this.n, this.k);
	
			int i;
			for (i = 0; i < this.k; ++i)
				ans.data[i] = this.data[i];
	
			for (i = this.k - 1; i > 0 && ans.data[i] == this.n - this.k + i; --i)
				;
	
			++ans.data[i];
	
			for (int j = i; j < this.k - 1; ++j)
				ans.data[j + 1] = ans.data[j] + 1;
	
			return ans;
		}
	
		private int choose(int n, int k) {
			if (n < 0 || k < 0)
				throw new IllegalArgumentException("Invalid negative parameter in choose()");
			if (n < k)
				return 0;
			if (n == k)
				return 1;
	
			int delta, iMax;
	
			if (k < n - k) {
				delta = n - k;
				iMax = k;
			} else {
				delta = k;
				iMax = n - k;
			}
	
			int ans = delta + 1;
	
			for (int i = 2; i <= iMax; ++i)
				ans = (ans * (delta + i)) / i;
	
			return ans;
	
		}
	
		public Combination element(int m) {
			int[] ans = new int[this.k];
	
			int a = this.n;
			int b = this.k;
			int x = (choose(this.n, this.k) - 1) - m;
	
			for (int i = 0; i < this.k; ++i) {
				ans[i] = largestV(a, b, x);
				x = x - choose(ans[i], b);
				a = ans[i];
				b = b - 1;
			}
	
			for (int i = 0; i < this.k; ++i)
				ans[i] = (n - 1) - ans[i];
	
			return new Combination(this.n, this.k, ans);
		}
	
		private int largestV(int a, int b, int x) {
			int v = a - 1;
	
			while (choose(v, b) > x)
				--v;
	
			return v;
		}
	
		@Override
		public Iterator<int[]> iterator() {
			return new Iterator<int[]>() {
				private Combination current = null;
				private Combination next = Combination.this;
	
				@Override
				public boolean hasNext() {
					return next != null;
				}
	
				@Override
				public int[] next() {
					if (next == null)
						throw new NoSuchElementException();
					current = next;
					next = current.sucessor();
					return current.data;
				}
	
				@Override
				public void remove() {
					throw new UnsupportedOperationException("cannot remove items from combination");
				}
	
			};
		}
	
	}
```
##### **6.3.2 Hex 代码**
```
	package cn.beeKey.cryptography.util;
	
	
	public final class Hex {
		private final static char[] HEX = { '0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'A', 'B', 'C', 'D', 'E', 'F' };
		private final static int[] ORD = { -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1,
				-1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, -1, -1, -1, -1, -1, -1, -1, 10, 11, 12, 13,
				14, 15, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, 10, 11, 12, 13, 14, 15, -1, -1, -1,
				-1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1,
				-1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1,
				-1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1,
				-1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1,
				-1 };
	
		public static String convert(byte[] bytes) {
			int n = bytes.length;
			char[] chars = new char[n << 1];
			for (int j = 0; j < n; j++) {
				int v = bytes[j] & 0xFF;
				chars[j << 1] = HEX[v >>> 4];
				chars[(j << 1) + 1] = HEX[v & 0x0F];
			}
			return new String(chars);
		}
	
		public static byte[] convert(String s) {
			int len = s.length();
			byte[] bytes = new byte[len >> 1];
			for (int i = 0; i < len; i += 2)
				bytes[i >> 1] = (byte) ((ORD[s.charAt(i) & 0xff] << 4) + ORD[s.charAt(i + 1) & 0xff]);
			return bytes;
		}
	}
```
#### 6.4 代码的目录结构

![enter image description here](https://images.gitbook.cn/7c6405f0-3e4b-11e9-a98d-5dc2d0f56a42)

如果有问题，请直接联系我！邮箱：`guoshijiang2012@163.com`或者`20123762@s.hlju.edu.cn`



