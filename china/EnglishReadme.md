[![Chinese](https://img.shields.io/badge/Chinese-README-red)](README.md)


# Chapter N: State Secrets

### 1. About this article

National Cryptozoology refers to the domestic cryptographic algorithm recognized by the State Cryptozoology Bureau. Mainly include SM1, SM2, SM3 and SM4. The key length and block length are both 128 bits. SM1 is symmetric encryption, SM2 is asymmetric encryption, SM3 message digest, SM4 block cipher algorithm. This article will introduce in detail the implementation principles of the four major national secrets, as well as the actual Java code, and will analyze the application scenarios of the four major national secret algorithms; this article is aimed at those in the industry who have a certain foundation in cryptography or are interested in cryptography. friend

### 2. Structure of this article

The article introduces the principles and code practice of SM1, SM2, SM3, and SM4 algorithms in order. After letting everyone understand the national secret algorithm, we will then introduce the application scenarios of the national secret SM1, SM2, SM3, and SM4 algorithms to complete the introduction of the application scenarios. , we will analyze the current situation of national secrets and the future development direction of national secrets.

### 3. SM1 algorithm principle and code practice

#### 1. Introduction to SM1

SM1 is a symmetric encryption, and the algorithm implementation principle of the cover algorithm has not been disclosed. Its encryption strength is equivalent to AES, and it needs to call the interface of the encryption chip to use it. SM1's key length of up to 128 bits and the strength and non-disclosure of the algorithm itself ensure the security of communications. Since the SM1 encryption algorithm is not public, we cannot know its internal principles, so we cannot implement the code here.

#### 2. SM1 application scenarios

SM 1 is packaged into a chip by a specific organization certified by the State Secretariat Office, and sold to designated manufacturers. The SM1 algorithm has been widely used in various fields such as e-commerce, government affairs, and national economy and people's livelihood (such as national government affairs, police and other institutional fields). Currently, the series of chips, smart IC cards, encryption cards, encryption machines and other security products on the market all use the SM1 algorithm. Data encryption includes software encryption and hardware encryption. Software encryption refers to relying solely on code to protect software without requiring specific hardware services. The most prominent advantages of software encryption are its low cost, simple implementation, and good flexibility and portability. However, software-implemented encryption requires the full participation of the CPU, which may cause unnecessary waiting and interruptions, leading to a waste of system resources. Especially when using software encryption to process massive amounts of data, there is a risk of hard disk read and write bottlenecks. Hardware encryption is implemented using an encryption chip integrated on the CPU chip. The encryption process is independent of the CPU and completed within the chip, which can effectively prevent data from being tampered with.
Hard encryption is used by most banks, and the underlying algorithm often contains SM1.

An encryption card integrates encryption and authentication algorithms such as AES, DES, and MDS on a chip. The chip is made into a support card (i.e., encryption card). All operations involved in data encryption, decryption, and authentication are completed on the card. This in turn speeds up the encryption and decryption process and improves the overall performance of the device. At present, encryption cards are generally divided into two categories, one is encryption cards that implement universal encryption, decryption and verification algorithms, and the other is encryption cards that implement the national secret algorithm (SM1).

### 4. SM2 algorithm principle and code practice

National secret SM2 is asymmetric encryption, also known as public key cryptography; the essence of the national secret algorithm is elliptic curve encryption. For more information about symmetric encryption and asymmetric encryption, please refer to the article "In-depth Understanding of Symmetric Encryption and Asymmetric Encryption" written by the author. The SM2 elliptic curve public key cryptography (ECC) algorithm is my country's public key cryptography algorithm standard. The main contents of the SM2 algorithm include 3 parts: digital signature algorithm; key exchange protocol and public key encryption algorithm.

#### 1. Formation process of SM2

Among all public key cryptography, ECC and RSA are more widely used; and under the same security strength, the private key bit length and system parameters of ECC are much smaller than that of RSA, which means that the storage space required for applying ECC is much smaller. Much smaller, the bandwidth requirements of the transmission station are lower, the number of logic gates of the logic circuit required for hardware implementation of ECC is much less than that of RSA, and the power consumption is lower. This makes ECC more suitable than RSA for implementation into devices with severely limited resources, such as mobile communication devices, wireless communication devices and smart cards with low power consumption requirements.

The advantages of ECC make it the public key cryptography algorithm with the most development potential and application prospects. By 2000, many countries and industry organizations in the world had adopted ECC as the public key cryptography algorithm standard. In this context, our country has organized research on ECC with independent intellectual property rights since 2001. By using public-key cryptographic algorithm design and security analysis theories and methods recognized by the international cryptography community, we have absorbed existing ECC research results at home and abroad. , the SM2 algorithm was developed in 2004. The SM2 algorithm was first publicly released in December 2010, became China's commercial encryption standard in March 2012 (standard number is GM/T0003-2012), and became China's national encryption standard in August 2016 (standard number is GB/T 32918-2016 ).

#### 2. Elliptic curve

On the finite field K, the following equation forms:

![enter image description here](https://images.gitbook.cn/74a9f450-705f-11e9-aa97-d52fde2e3e58)

The equation of is called the Weierstrass equation, where O=[0,1,0] is the only point whose Z coordinate is zero, called the infinity point. Let x=X/Z, y=Y/Z, and the equation can be written as:

![enter image description here](https://images.gitbook.cn/df7bb020-705f-11e9-b46a-41726d193891)

And there is still an infinite point O.
For the coefficients in the equation, define

![enter image description here](https://images.gitbook.cn/3a4e1d80-7060-11e9-b46a-41726d193891)

in:

![enter image description here](https://images.gitbook.cn/5da2c330-7060-11e9-aa97-d52fde2e3e58)

When Δ ≠ 0, the elliptic curve is non-singular [1], that is, for all projective points P=(X ∶ Y ∶ Z) that satisfy F(X,Y,Z)=0, F is at 3 of the P points Partial derivative 
![enter image description here](https://images.gitbook.cn/8cfa5c60-7060-11e9-be31-a34bfde053f0) must not be all 0.

When the characteristic of K is not 2 or 3, the Weierstrass equation has the following form:

![enter image description here](https://images.gitbook.cn/bd867df0-7060-11e9-83ce-bf64b45f6e99)

Among them: E:y2=x3+Ax2+B is the elliptic curve recommended by the State Cryptozoology Bureau. This article also implements the algorithm based on this curve.

#### 3. Basic operations on elliptic curves

![enter image description here](https://images.gitbook.cn/55229ef0-72ff-11e9-a8ef-33cfb90ae5eb)

On the elliptic curve, the addition operation can be defined in the following way: take two points P and Q on the elliptic curve, draw a straight line passing through P and Q and intersect the elliptic curve at R'..., draw a parallel line passing through R' to the y-axis and intersect the elliptic curve at R. If P and Q coincide, then the tangent line to the curve drawn through P intersects the elliptic curve at R’…, and the parallel line drawn through R’… to the y-axis intersects the elliptic curve at R. It is stipulated that R=P+Q. As shown in Figure 1. For an infinite point O and a point P on an elliptic curve, O+P=P+O=P. For the above simplified Weierstrass equation ![enter image description here](https://images.gitbook.cn/956c7210-72ff-11e9-b7db-d127bed921dc)  order ![enter image description here](https://images.gitbook.cn/c6058bf0-72ff-11e9-a8ef-33cfb90ae5eb)

If R=P+Q, then:

![enter image description here](https://images.gitbook.cn/ee86cf30-72ff-11e9-a8ef-33cfb90ae5eb)

The elliptic curve cryptosystem is a cryptosystem based on the Abel group composed of the above-mentioned addition operations and curves. The main operation involved in the elliptic curve cryptosystem is the point multiplication calculation on the elliptic curve: Q=kP. Q and P are points on the elliptic curve, and k is an integer.

#### 4. Mathematical basis of large number operations on elliptic curves

##### 4.1 Modular operation and prime number field

Congruence is an equivalence relationship in number theory. For a positive integer m, if a=b+km (a, b, k are all integers), then record b=a mod (m), then a and b are said to be congruent with respect to m. . When m=p (p is a prime number), we define that the prime field FP can be composed of P elements in {0, 1, 2, 3...p-1}, and the modular operation on P is called the modular operation on the prime field.

##### 4.2 Design and implementation of modular operations on finite fields

Modular operations on finite fields are the basis of the SM2 elliptic curve public key cryptographic algorithm, which mainly include modular addition and modular subtraction operations, modular multiplication operations, modular exponentiation and modular inversion operations. The modular inverse operation is the most complex operation with the largest amount of calculations among the modular operations. The modular inverse operation can be obtained through Fermat's little theorem (when n is a prime number, the formula an-1=1modn holds for an integer a that is relatively prime with n). , that is, when p is a prime number, ap-1=1mod p, then the modular inverse operation a-1=ap-2mod p can be obtained, so that the modular exponentiation operation can be used to express the modular inverse operation.

##### 4..3 Design and implementation of scalar multiplication operation on finite fields

The mathematical form of scalar multiplication, P = (xp, yp) is the point on the elliptic curve E (FP), k is a positive integer, and the k times point of P is Q. Q=[k]P=P+P+…+P (k p’s). The scalar multiplication operation is the most time-consuming operation among all operations. It is mainly generated by point addition and point multiplication. The operation rules of point addition and point multiplication operations are different in different coordinate systems. The operation rules under the mixed affine and Jacobian coordinate systems are adopted:
![enter image description here](https://images.gitbook.cn/df0ad060-7395-11e9-98d2-ebcf245f223d) , where a and b are integers on the elliptic curve, and △= ![enter image description here ](https://images.gitbook.cn/19a23420-7396-11e9-b02d-058b823f7d15).

The infinity point of the three-dimensional coordinates P (x1, y1, z1) and Q (x2, y2, 1) is (1, 1, 0). Double point operation P+P = (x3, y3, z3) is declared as Padd1 (x1, y1, z1, x3, y3, z3), store the value of 2P in (x3, y3, z3), and point addition operation P+ Q=(x3, y3, z3) is declared as Padd2(x1, y1, z1, x2, y2, x3, y3, z3), and the value of P+Q is stored in (x3, y3, z3). Finally, the results (x3, y3, z3) need to be converted from the Jacobian weighted photographic coordinate system to the affine coordinate system. The parameters need to be converted: x3=x3/z12, y3=y3/z13, and the results are obtained. The required two-dimensional coordinate point (x3, y3).

With point addition and point multiplication operations, scalar multiplication operations can be performed. The algorithm of scalar multiplication from right to left is: Input: point P∈E (Fp) integer k = (k 31k30-k 0) (ki is an 8-bit integer Model number)

Output: Q=［k］P
  Initialize Q=O as an infinite point
Loop i: 0~31
b=k (i b is an 8-bit integer)
Loop j: 0~7
If (b&1)=1, then Q=Q+P
b=b>>1
P=P+P
ReturnQ

#### 5. SM2 public key encryption algorithm

Parameters of elliptic curves in the prime field: modulo P of the prime field, elliptic curve E (FP)
Coefficients: a, b; the base point G (Gx, Gy) on E (FP) ≠ 0, the solution of the base point G is n remainder
Factor h=1, user A holds the public key of user B, PB, and user B holds the private key dB.

##### 5.1 SM2 encryption algorithm

(1) Use a random number generator to generate random numbers ![enter image description here](https://images.gitbook.cn/511015c0-7ac7-11e9-a023-5dfd4cad8c57)

(2) Calculate points on the elliptic curve ![enter image description here](https://images.gitbook.cn/5a7f17f0-7ac7-11e9-bfe0-2d8b1a11ad74)

(3) Calculate elliptic curve points ![enter image description here](https://images.gitbook.cn/64e7e370-7ac7-11e9-a23c-35b15700507e), if S is an infinity point, an error will be reported and exited. h is the cofactor, which is taken as 1 here.

(4) Calculate points on the elliptic curve ![enter image description here](https://images.gitbook.cn/a8f9e220-7ac7-11e9-99f3-43e3454a8bb7).

(5) Calculate ![enter image description here](https://images.gitbook.cn/af24dce0-7ac7-11e9-bfe0-2d8b1a11ad74), if t is all 0, return 1.

(6) Calculation ![enter image description here](https://images.gitbook.cn/b91f7d40-7ac7-11e9-a023-5dfd4cad8c57).

(7) Calculate ![enter image description here](https://images.gitbook.cn/c0d5d2f0-7ac7-11e9-bfe0-2d8b1a11ad74).

(8) Calculate the ciphertext ![enter image description here](https://images.gitbook.cn/c9029120-7ac7-11e9-bfe0-2d8b1a11ad74).

##### 5.2. SM2 decryption algorithm

(1) Take out C1 from the ciphertext and verify whether C1 satisfies the elliptic curve equation. If not, an error will be reported and exit.

(2) Calculate ![enter image description here](https://images.gitbook.cn/1a2745a0-7ac8-11e9-a023-5dfd4cad8c57), if S is an infinity point, an error will be reported and exit.

(3) Calculate ![enter image description here](https://images.gitbook.cn/21efc3c0-7ac8-11e9-bfe0-2d8b1a11ad74).

(4) Calculate ![enter image description here](https://images.gitbook.cn/2867a600-7ac8-11e9-a23c-35b15700507e).

(5) Take out C2 from C and calculate ![enter image description here](https://images.gitbook.cn/2fa7e150-7ac8-11e9-a023-5dfd4cad8c57).

(6) Calculate ![enter image description here](https://images.gitbook.cn/35bac030-7ac8-11e9-a23c-35b15700507e), if u is not equal to C3, an error will be reported and exit.

(7) Output plaintext m.

#### 6 SM2 code implementation

https://github.com/guoshijiang/NationalSecret


#### 7. SM2 Summary

The SM2 algorithm is an ECC algorithm with independent intellectual property rights developed by my country on the basis of absorbing international advanced results. It is equivalent to or slightly better than similar international ECC algorithms in terms of security and implementation efficiency. It can replace RSA to meet various needs. The application has higher requirements for the security and implementation efficiency of public key cryptography algorithms, and has broad promotion and application prospects.

### 5. SM3 algorithm principle and code practice

#### 1. Introduction to SM3

The SM3 password hash algorithm is China's commercial password hash algorithm standard published by the State Cryptozoology Administration of China. This algorithm was designed by Wang Xiaoyun and others. It groups message bits and outputs hash value bits, using a Merkle Damgard structure. The compression function of the cryptographic hash algorithm has a similar structure to the compression function of . However, the structure of the compression function of the cryptographic hash algorithm and the design of the message expansion process are more complex. For example, each round of the compression function uses a message word, and the message expansion process Each round of the process uses a message word, etc.

The SM3 cryptographic hash algorithm message group length is 512b, and the digest length is 256b. Compression function state 256 b, 64 steps in total.

#### 2. Algorithm description of SM3

##### 2.1. Constants and functions in cryptographic hash algorithms

Initial value: The initial value of the SM3 password hash algorithm is 256 b in total, consisting of 8 32b concatenations.
The specific values are as follows:
![enter image description here](https://images.gitbook.cn/649a7b10-79e8-11e9-8dec-3dba4995d575)

constant
![enter image description here](https://images.gitbook.cn/69958150-79e8-11e9-91d6-116993cb37bb)

boolean function
![enter image description here](https://images.gitbook.cn/6ec50510-79e8-11e9-aee1-59a97a37cd88)

X and Y in the above formula are 32-bit words.

permutation function
![enter image description here](https://images.gitbook.cn/7611ea90-79e8-11e9-91d6-116993cb37bb)

X and Y in the above formula are 32-bit words.

##### 2.2. SM3 algorithm description

For a message M with a length of l (l is less than 2 to the power of 64) bits, the SM3 cryptographic hash algorithm generates a hash value through message filling and iterative compression, and the length of the hash value is 256 bits.

1. Message filling

It is assumed that the length of the message input is l (l is less than 2 raised to the power of 64) bits. First add the bit "1" to the end of the message, and then add k "0"s, where k is the smallest non-negative integer such that k + l + 1 = 448 mod 512. Then add a 64-bit bit string that is the binary representation of length l. The padded message M bit length is a multiple of 512.

For example: for the message 01100001 01100010 01100011, the length l =24, the bit string is obtained after padding:

![enter image description here](https://images.gitbook.cn/3880e3f0-79ea-11e9-8dec-3dba4995d575)

2. Iterative compression

Iterative compression is the main operation of the SM3 cryptographic hash algorithm, and this step produces the final hash value. The iterative compression process can be expressed as follows:

Group the filled message M into 512 bits: ![enter image description here](https://images.gitbook.cn/225fcd10-79eb-11e9-aee1-59a97a37cd88)   where: n = (k + 1 + l + 64) / 512

Iterate as follows:

![enter image description here](https://images.gitbook.cn/61aa0a80-79eb-11e9-8dec-3dba4995d575)

Among them, CF is the compression function, V (0) is the 256-bit initial value IV, B (i) is the filled message grouping, and the result of iterative compression is V (n), which is also the hash value of message M.

3.Message expansion

Group the message B (i) Expand to generate words W0, W1 ... W67; W0', W1' ... W63' according to the following method, which are used for the compression function CF:

![enter image description here](https://images.gitbook.cn/55974310-79ec-11e9-8dec-3dba4995d575)


![enter image description here](https://images.gitbook.cn/5b17cd00-79ec-11e9-8dec-3dba4995d575) ![enter image description here](https://images.gitbook.cn/5fb45f90-79ec-11e9-8dec-3dba4995d575)

4. Compression function

![enter image description here](https://images.gitbook.cn/9fb43160-79ec-11e9-969e-fb1e44586b50)

The characters are stored in big-endian format.

5.Hash value

![enter image description here](https://images.gitbook.cn/de678600-79ec-11e9-969e-fb1e44586b50)

Output a 256-bit hash value ![enter image description here](https://images.gitbook.cn/e4b23dc0-79ec-11e9-969e-fb1e44586b50)

#### 3. SM3 code implementation

https://github.com/guoshijiang/NationalSecret

#### 4. Summary of SM3

The design and application of hash functions have been developed for more than decades. Since the birth of the first directly constructed hash function, the cryptography community has generally believed that constructing a secure hash function is to construct a collision-resistant compression function. However, as Wang Xiaoyun and others successfully cracked MD5 and other hash functions, hash functions designed based on the traditional MD structure were proven to be unsafe. Therefore, the design and analysis of hash functions has become a major research hotspot in the cryptography community, especially the current research on the latest hash algorithms, which has promoted the climax of research on hash functions. The research on the number of SM3 rounds will be the climax. The SM3 algorithm that reduces the number of rounds will be used to conduct randomness analysis and the boomerang attack method of the 32-round, 33-round, 34-round and 35-round algorithms. However, how to analyze the primitive roots, collisions and second primitive roots of algorithms with more rounds is also an issue that requires further research.

### 6. SM4 algorithm principle and code practice

#### 1. Introduction to SM4

SM4 is a Feistel structure block cipher algorithm with a block length and a key length of 128 bits. Both the encryption and decryption algorithm and the key expansion algorithm adopt a 32-round nonlinear iteration structure. The decryption algorithm has the same structure as the encryption algorithm, except that the round keys are used in the reverse order, that is, the round keys used by the decryption algorithm are the reverse order of the round keys used by the encryption algorithm.

#### 2. SM4 algorithm description

##### 2.1. Encryption and decryption algorithm description

Defined as a vector set of e bits, <<< i is a 32bit circular left shift by i bits, and ⊕ is a 32bit XOR.

The SM4 decryption algorithm is now introduced in detail. The 128-bit plaintext or ciphertext input is divided into 4 bytes after initial transformation, and the round key is processed through the round function to complete the encryption and decryption operations through 32 rounds of iterations.

Suppose the plaintext input is ![enter image description here](https://images.gitbook.cn/cb3efb60-79fd-11e9-8dec-3dba4995d575) and the ciphertext output is ![enter image description here](https://images.gitbook.cn/d5ecbf20-79fd-11e9-8dec-3dba4995d575), the round key is
![enter image description here](https://images.gitbook.cn/e2c440b0-79fd-11e9-91d6-116993cb37bb), then the The encryption process of the algorithm is:

![enter image description here](https://images.gitbook.cn/1ad39a00-79fe-11e9-969e-fb1e44586b50)

In formula (1), F(.) is called the round function of the encryption algorithm; T (.) is ![enter image description here](https://images.gitbook.cn/573f4890-79fe-11e9-91d6-116993cb37bb)'s reversible transformation, by nonlinear transformation ![enter image description here](https://images.gitbook.cn/7394b390-79fe-11e9-8dec-3dba4995d575) and linear transformation L, that is ![enter image description here](https://images.gitbook.cn/91247350-79fe-11e9-91d6-116993cb37bb). The nonlinear transformation consists of 4 parallel S-boxes. Let the input be ![enter image description here](https://images.gitbook.cn/ee8e2d60-79fe-11e9-8dec-3dba4995d575) and the output be ![enter image description here](https://images.gitbook.cn/f53b9e90-79fe-11e9-8dec-3dba4995d575), then

![enter image description here](https://images.gitbook.cn/ff673a00-79fe-11e9-aee1-59a97a37cd88) (3)

Among them, ![enter image description here](https://images.gitbook.cn/0e00ddf0-79ff-11e9-91d6-116993cb37bb) is a fixed mapping table.

The input of linear transformation is the output of nonlinear transformation. Suppose the input is ![enter image description here](https://images.gitbook.cn/6dde0900-79ff-11e9-91d6-116993cb37bb) and the output is ![enter image description here](https://images.gitbook.cn/731247b0-79ff-11e9-969e-fb1e44586b50), then:   ![enter image description here](https://images.gitbook.cn/7947f0d0-79ff-11e9-8dec-3dba4995d575) (4)

The SMS decryption process is the same as the encryption transformation structure. The only difference is the order in which the round keys are used. The first round is used ![enter image description here](https://images.gitbook.cn/95154010-79ff-11e9-aee1-59a97a37cd88), use ![enter image description here](https://images.gitbook.cn/9d277160-79ff-11e9-8dec-3dba4995d575) in the second round, and so on.

##### 2.2. Key expansion algorithm

The round key of the encryption algorithm in this algorithm is generated from the encryption key through the key expansion algorithm. Let the encryption key be ![enter image description here](https://images.gitbook.cn/43320110-7a00-11e9-aee1-59a97a37cd88) . Let![enter image description here](https://images.gitbook.cn/4da37f20-7a00-11e9-aee1-59a97a37cd88), and the round key is ![enter image description here](https://images.gitbook.cn/529adbe0-7a00-11e9-91d6-116993cb37bb), then the round key generation method is: ![enter image description here](https://images.gitbook.cn/589f62e0-7a00-11e9-aee1-59a97a37cd88) (5)

Yes ![enter image description here](https://images.gitbook.cn/7cc4c610-7a00-11e9-aee1-59a97a37cd88)

![enter image description here](https://images.gitbook.cn/83f8cc60-7a00-11e9-8dec-3dba4995d575) (6)
Among them, the T* transformation is basically the same as the T transformation in the encryption algorithm round function, only the linear transformation L is modified to L*:

![enter image description here](https://images.gitbook.cn/a5805330-7a00-11e9-91d6-116993cb37bb) (7)

The parameter FKi in equation (5) and the parameter CKi in equation (6) are both fixed values. In addition, CKi can also be calculated. Let ckij be the j-th byte of CKi, where ![enter image description here](https://images.gitbook.cn/0f57a970-7a01-11e9-91d6-116993cb37bb), that is ![enter image description here]( https://images.gitbook.cn/1ac3db30-7a01-11e9-91d6-116993cb37bb), then

![enter image description here](https://images.gitbook.cn/255a1f50-7a01-11e9-91d6-116993cb37bb) (8)

#### 3. SM4 code implementation

https://github.com/guoshijiang/NationalSecret

#### 4. SM4 Summary

The SM4 cryptographic algorithm is China's first commercial cryptographic algorithm announced and designed by a professional cryptography agency. So far, no attack methods have been found to threaten the security of the SM4 algorithm.

### 7. Other national secret algorithms


### 1. SM7

A block cipher algorithm.

### 2. SM9

SM9 is an identification cryptography standard adopted by my country. It was released by the State Cryptozoology Administration on March 28, 2016. The relevant standard is "GM/T 0044-2016 SM9 identification cryptography algorithm". In commercial cryptography systems, SM9 is mainly used for user identity authentication. The SM9 algorithm does not require the application of a digital certificate and is suitable for security protection of various emerging applications on the Internet. According to a public report by Xinhuanet, the encryption strength of SM9 is equivalent to the RSA encryption algorithm with a 3072-bit key.


### 8. Summary of this article

Judging from the current cryptography research technology, the security of the existing national secret algorithms will not be subject to any offensive crisis for a period of time. However, with the development of cryptography technology and quantum computers, future national secret algorithms will face For greater challenges, the improvement of existing national secret algorithms, new cryptographic algorithms and research on anti-quantum cryptography will become hot topics in national secret research.