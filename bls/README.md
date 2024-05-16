# BLS 算法

BLS (Boneh-Lynn-Shacham) 签名算法是一种基于双线性配对（bilinear pairing）和椭圆曲线密码学的数字签名算法，由Dan Boneh, Ben Lynn, 和 Hovav Shacham在2001年提出。BLS签名以其简洁、短签名和强安全性著称，被广泛应用于区块链和其他分布式系统中。

## 1.基本原理

BLS签名算法基于以下数学结构和问题：

### 双线性配对

给定两个椭圆曲线群 $G_1$ 和 $G_2$ 以及一个目标群 $G_T$，存在一个双线性映射 $e: G_1 \times G_2 \to G_T$ 满足：

- **双线性性**：$e(aP, bQ) = e(P, Q)^{ab}$ 对所有 $P \in G_1$, $Q \in G_2$ 和 $a, b \in \mathbb{Z}_p$。
- **非退化性**：如果 $P \neq O$ 且 $Q \neq O \)，则 \( e(P, Q) \neq 1$。
- **有效性**：计算 $e(P, Q)$ 在有限时间内是可行的。


