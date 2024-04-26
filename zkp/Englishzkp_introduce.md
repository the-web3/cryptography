[![Chinese](https://img.shields.io/badge/Chinese-README-red)](zkp_introduce.md)

## Chapter 14: Introduction to Zero-Knowledge Proofs

### 1. What is zero-knowledge proof?

Zero-knowledge proof simply means that a person can prove something he knows to others without revealing it to others. In order to facilitate the understanding of zero-knowledge proof, Alibaba has a very classic example. Alibaba was able to prove to the thief that he knew the magic word without revealing it.

In the lecture video of Stanford professor Dan Boneh, he gave a vivid example describing zero-knowledge proof: Professor Dan tried to introduce zero-knowledge proof to kindergarten children, using the game-"Where's Waldo". Where's Waldo is a classic board game that requires players to find a specific character - Waldo - in a picture filled with people. As shown below:

![100.jpeg](https://github.com/guoshijiang/cryptography/blob/master/img/100.jpeg)

How to use zero-knowledge proof to prove that you know where Waldo is?

First, you need a pair of scissors. Next, turn around and cut Waldo's figure from behind so that the challenger can't see it. Then rip off the rest of the board. And hand over the image of Waldo to the challenger. This perfectly proves that you know Waldo's location without giving it away. The knowledge used in this example is called "Waldo's location".

### 2. The school of zero-knowledge proof

#### 1. Common zero-knowledge proof schools
Before introducing the zero-knowledge proof genre, everyone should note that what we often call ZK-SNARK is not an algorithm, but a genre. ZK-STARK is the name of a specific zero-knowledge algorithm.
##### 1.1 STARK and SNARK

Just a quick aside, zero-knowledge proof techniques allow one party to prove to another party that they know something without the prover having to convey the information themselves to prove their knowledge. They are both a privacy-enhancing technology because they reduce the amount of information that needs to be provided between users, and a scaling technology because they allow proofs to be verified faster because they do not encompass the full number of non-private systems Information.

Two of the most compelling zero-knowledge technologies on the market today are zk-STARKs and zk-SNARKs. Both are abbreviations for methods by which two parties prove their knowledge: zk-STARK stands for Zero-Knowledge Scalable Transparent Argument of Knowledge, and zk-SNARK stands for Zero-Knowledge Succinct Non-Interactive Argument of Knowledge. This article will delve into the core differences between these two different zero-knowledge technologies from both a cultural and technical perspective. Additionally, both zero-knowledge technologies are non-interactive in nature, meaning code can deploy and act autonomously.
Below, we have several tables describing some of the high-level differences between these two technologies. We’ll also delve into the differences in paragraph formatting.
![101.png](https://github.com/guoshijiang/cryptography/blob/master/img/101.png)

![102.png](https://github.com/guoshijiang/cryptography/blob/master/img/102.png)

##### 1.2. SNARK
In January 2012, a UC Berkeley professor named Alessandro Chiesa co-authored a paper that coined the term zk-SNARK for the first zero-knowledge proof they had built. Zk-SNARK relies on elliptic curves for its security. Elliptic curves in cryptography operate under the fundamental assumption that finding the discrete logarithm of a random elliptic curve element with respect to a well-known base point is infeasible.

While there has been significant controversy over whether there are backdoors to the elliptic curve random number generator, the algorithm as a whole remains generally secure. Although there are several popular vulnerabilities in side-channel attacks, they are easily mitigated through a variety of techniques. Quantum attacks do loom over elliptic curve-based cryptography, but the quantum computing required to break its security model is not yet widely available.

In addition to being based on elliptic curves, zk-SNARKs also require a trustworthy setup. Trusted setup refers to the initial creation event of the keys used to create the proofs required for private transactions and to verify those proofs. Initially, when these keys are created, there is a hidden parameter between the verification key and the key used to send private transactions. If the secrets used to create these keys in a trusted setup event are not compromised, these secrets can be used to forge transactions with false verifications, allowing the holder to do things like create new tokens out of thin air and use them Operations are used for transactions. Due to the privacy properties of zk-SNARKs, there is no way to verify that tokens created out of thin air are actually created out of thin air. That being said, only a trusted setup is required initially.

Users of SNARK-based networks must therefore rely on the fact that the trusted setup was performed correctly, meaning that the secrets associated with the trusted setup key were compromised and not held by the individual overseeing the ceremony. The reliance on trusted settings has been one of the biggest areas of concern for SNARK critics. Having said that, developers only need to use the trusted setup initially, not on an ongoing basis.

Another important area of ​​criticism of SNARKs is that they are not quantum resistant. Once quantum computing becomes available to a large extent, the privacy technology behind SNARKs will be broken. Of course, SNARK proponents rightly point out that we will face more problems when using quantum computers, such as the destruction of RSA and most wallet infrastructure.

That being said, despite the issues associated with trusted setups, SNARK adoption is actually much faster than STARK for a number of reasons. SNARK was discovered several years before STARK, giving the technology a significant head start in adoption. Zcash is one of the older digital asset projects that popularized the use of SNARKs in the blockchain development community. Thanks to the adoption of Zcash and other SNARKs, SNARKs have the largest developer library, published code, projects, and developers actively working on the technology. In addition to Zcash, the emerging DEX Loopring also uses SNARK. If developers want to start using zero-knowledge technology, they will have more support using SNARKs than STARKs.

Additionally, it is estimated that SNARK requires only 24% of the gas required by STARK, meaning that trading with SNARK is much cheaper for end users. Finally, the proof size of SNARKs is much smaller than STARKs, meaning it requires less on-chain storage.

##### 1.3. STARKs
While SNARKs have some clear advantages over STARKs in terms of documentation and developer support, STARKs do offer some unique advantages. But first, let’s dig into what STARK is from a technical perspective.
Eli Ben-Sasson, Iddo Bentov, Yinon Horeshy, and Michael Riabzev wrote the first paper describing STARK in 2018. Unlike SNARKs, the underlying technology of STARKs relies on hash functions. Right off the bat, relying on hash functions provides some benefits, such as quantum resistance. Additionally, no trusted setup is required to start using STARK on your network.

Having said that, the proof size of STARKs is much larger than that of SNARKs, which means that verifying STARKs takes more time than SNARKs, and also causes STARKs to require more gas.
Additionally, developers will have a hard time using STARK due to a lack of developer documentation and community. While there are a few projects that create scaling solutions based on STARKs, such as STARKWARE, the SNARKs community is still much larger.
While both developer communities support SNARK and STARK, the Ethereum Foundation specifically expressed support for using Starks' STARKware. In fact, the Ethereum Foundation provided a $12 million grant to STARKware, clearly demonstrating their commitment to the emerging technology.

##### 1.4. ZK-SNARK

Our most common one is probably ZK-SNARK. The abbreviation of SNARK is succinct non-interactive arguments of knowledge. The most special point of SNARK is its N, non-interactivity.
- Simplicity (Succinct): The computing resources required for verification are much smaller than re-running the program that needs to be proved.
- Non-interactive: The prover and the verifier do not need to communicate in every round. They only need to complete Trust Setup at the beginning. Other validators can also join the verification after trusted initialization
- Argument: If the prover has extremely powerful computing power, then he can generate a false proof. If this happens, the mainstream public-private key encryption model is no longer secure.
- Knowledge: The prover needs to know some secrets that others do not know in order to generate a proof

The biggest problem with ZK-SNARK is that it requires trusted initialization. Trusted initialization generates a reference string. If RS is leaked, anyone can generate false proofs. In addition, how to design trusted initialization involving multiple people is also very challenging. RS can only be used for pinned programs. For other programs, we need additional trusted initialization. Therefore ZK-SNARK is not possible for general purpose computation. Another thing, the RS cannot be upgraded. If we upgrade the program, trusted initialization needs to be re-run.
The problem with ZK-SNARK is the trust-building phase. The reference string is generated during the trust establishment phase. If the reference string is leaked, anyone can make a fake proof. Additionally, how to coordinate this trust setting phase among multiple parties is complex. Reference strings can only be used within one program (circuit). Therefore, in general computing, it is impossible to have a single trust setting for ZK-SNARK. Another problem is that reference strings are not upgradeable. If we upgrade the program we need to re-run the trust setup phase

In order to solve this series of problems, scientists have found two directions

- Transparent Setup: Trusted initialization generates a common reference string (Common Reference String). CRS is public and does not require confidentiality. Fractal, Halo, ZK-STARK, and SuperSonic have all taken this route. The problem with this route is that the generated proof takes up too much storage, reaching the kB level. Storage is very expensive for blockchain.
- Universal Setup: Trusted initialization generates a Structure Reference String, but it needs to be kept secret. SRS allows trusted initialization to be used in different programs, which makes proofs of general computation possible. Marlink, SuperSonic-RSA and Plonk have all gone this route.

### 3. Common zero-knowledge proof algorithms

- Groth16: Zcash used this algorithm from the beginning. It is the benchmark benchmark in zero-knowledge proofs because it has the characteristics of fast proof and small generated proof. Its disadvantage is that it requires trusted initialization, and a trusted initialization can only target one program.
- Sonic: supports universal setup. The size of SRS is linearly related to the program size. The generated proof is of fixed size, but verification requires a lot of computing resources. Sonic makes zero-knowledge proofs of general computing possible
- Fractal: supports recursion. The generated proof takes up more space
- Halo: supports recursion, but does not satisfy succinct (Succinct) because the proof time is non-linear
- SuperSonic: The first practical, working Transparent ZK-SNARK
- Marlin: The program can be upgraded. Performance is between Sonic and Groth16
- Plonk: The program can be upgraded; participants join trusted initialization in order. This makes holding trusted initializations with many people less complex; Plonk uses Kate commitments instead of polynomial commitments. (The first step in ZK-SNARK is to transform the computational problem into a polynomial problem)
