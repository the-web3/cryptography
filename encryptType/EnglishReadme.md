[![Chinese](https://img.shields.io/badge/Chinese-README-red)](README.md)


# Chapter 3: Symmetric encryption and asymmetric encryption

Encryption methods in cryptography can be divided into symmetric encryption and asymmetric encryption from the direction of the number of keys. Symmetric encryption only uses one key to encrypt and decrypt data, while asymmetric encryption uses two keys to encrypt. They are public key and private key respectively. There are many very famous algorithms for symmetric encryption and asymmetric encryption. For example, the more famous algorithms for symmetric encryption are DES and AES, and the more famous algorithms for asymmetric encryption are RSA and ECC. Symmetric encryption and asymmetric encryption each have their own advantages and disadvantages, so how do we take advantage of their advantages and disadvantages? In this chapter, we will analyze symmetric encryption and asymmetric encryption from a theoretical and practical perspective respectively, making it easier to understand symmetric encryption and asymmetric encryption encryption.

### 1. About symmetric encryption and asymmetric encryption

We all know that there are two types of cryptography systems: symmetric cryptography (also called single-key cryptography) and asymmetric cryptography (also called dual-key cryptography or public-key cryptography). Symmetric cryptography uses the same key (secret key) to encrypt/decrypt messages. The confidentiality of the system is mainly determined by the security of the key, and has nothing to do with whether the algorithm is confidential.

The center of the design and implementation of symmetric cryptosystems is: which method to use to generate a key that meets confidentiality requirements and which method to use to distribute the key to the communicating parties safely and reliably. Symmetric cryptosystems can be implemented through block ciphers or stream ciphers, which can be used for both data encryption and message authentication. Asymmetric cryptography uses the public key to encrypt messages and the private key to decrypt them. The security of communication can be enhanced by using asymmetric cryptography.

In the cryptography system, symmetric encryption, asymmetric encryption, one-way hash functions, message authentication codes, digital signatures and pseudo-random number generators are collectively referred to as the cryptographer's toolbox. Among them, symmetric encryption and asymmetric encryption are mainly used to ensure confidentiality; one-way hash function is used to ensure the integrity of the message; the function of the message authentication code is mainly authentication; digital signature ensures the non-repudiation of the message. What this article is going to talk about is symmetric cryptography and asymmetric cryptography to ensure the confidentiality of messages.


### Symmetric encryption

Symmetric encryption, also known as single-key encryption, uses only one key in the entire encryption process. The so-called symmetry actually means using one key to encrypt and using the same key to decrypt. Symmetric encryption uses the same key algorithm for encryption and decryption, so it is faster in the encryption and decryption process and is suitable for encryption and decryption of relatively large amounts of data.

The main advantages of symmetric encryption are that the algorithm is public, the amount of calculation is small, the encryption speed is fast, and the encryption efficiency is high; however, it also has strong disadvantages. The disadvantage is that once the key is leaked during the key negotiation process, others can obtain the key. This can also decrypt ciphertext. In addition, every time each pair of users uses a symmetric encryption algorithm, they need to use a unique key that is unknown to others. This will make the number of keys owned by both the receiving and sending parties huge, and key management becomes a burden for both parties.

Commonly used symmetric encryption algorithms include DES, 3DES, AES, TDEA, Blowfish, RC2, RC4 and RC5, etc.

#### Two classic symmetric encryption algorithms

##### **DES**

The DES encryption and decryption algorithm was originally designed and invented by researchers from IBM in the United States. It is the first public commercial encryption algorithm standard and has been unanimously recognized by ISO since its inception. DES is a typical representative of block cipher algorithms. Its plaintext block length is 64 bits, and the key length is 64 bits, including an 8-bit parity check, so the effective key length is 56 bits. The DES encryption and decryption algorithm uses the same process and can be changed at any time. A very small number of them are considered to be weak keys that can be cracked, but it is easy to discard them without using them, so their own security mainly relies on valid keys.

The DES algorithm encryption process first operates on plaintext groups. The plaintext to be encrypted is divided into fixed sizes of 64 bits per block. The left and right parts shown in the figure below are the 64bits plaintext block encryption process and its 16 sub-key generation process.

![enter image description here](https://images.gitbook.cn/0f3891c0-40b3-11e9-b80c-abcbb40d7013)

###### **DES core algorithm module**

* IP initial replacement


	The initial IP replacement is performed before the first round of operation. The following numbers are used for the initial IP transformation of the input packets, and the replacement is performed from left to 	right and from top to bottom.
	
		58 50 42 34 26 18 10 2 
		60 52 44 36 28 20 12 4 
		62 54 46 38 30 22 14 6 
		64 56 48 40 32 24 16 8 
		57 49 41 33 25 17  9 1 
		59 51 43 35 27 19 11 3 
		61 53 45 37 29 21 13 5 
		63 55 47 39 31 23 15 7

* Subkey acquisition process

	The process of obtaining the subkey is as follows:
	![enter image description here](https://images.gitbook.cn/3219e6c0-40b4-11e9-b80c-abcbb40d7013)

	Here, the user enters a 64-bit key. According to the key permutation table PC-1, the 64-bit key is turned into a 56-bit key (the parity bit is removed here).
	
	The 56-bit key obtained by PC-1 permutation. Here the key is divided into the first 28 bits C0 and the last 28 bits D0. Perform a circular left shift on them respectively, C0 is shifted left to obtain C1, and D0 is 	shifted left to obtain D1.
	
	Combine C1 and D1 into 56 bits. Then perform compression permutation through the PC-2 table to obtain the 48-bit subkey K1 of this round.
	
	Then perform the same left shift and compression permutation on C1 and D1 to obtain the next round of subkeys... A total of 16 rounds are performed, so 16 48-bit subkeys can be obtained.

* E box extension

	E-box extended permutation is to arrange the 32 bits in the right half according to 8 rows and 4 columns to obtain a two-dimensional matrix of `8*4`, and then expand it to `8*6` (according to the E-box extended 		permutation table shown in Table 2.) two-dimensional matrix.

		32  1  2  3  4  5 
		4   5  6  7  8  9 
		8   9 10 11 12 13 
		12 13 14 15 16 17 
		16 17 18 19 20 21 
		20 21 22 23 24 25 
		24 25 26 27 28 29 
		28 29 30 31 32  1

* XOR operation

	The result of the P-box permutation is XORed with the left half of the original 64bits group, then the left and right halves are swapped, and another round begins.

* S box extension

	After the 48-bit key is generated, it can be XORed with the plain text to obtain the 48-bit cipher text. Then start the next round of S-box iteration operation, whose function is to change 6-bit data into 4-bits data. Each S-box is a table with 4 rows and 16 columns. The usage method of each S box is: the S box receives 6 bits of input, the 2-bit binary composed of the first bit and the last bit of the 6 bits is the row number of the S box, and the 4-bit binary in the middle is the column of the S box. number, and then check the S box definition table according to the row number and column number to obtain the corresponding value (usually decimal). This value is the output of the S box transformation and is converted into binary.

* P box replacement

	After the S-box replacement operation, 32 bits are output as the input of the P-box replacement, the last transformation of the F function. Perform P-box replacement on the 32-bit data, and obtain a result that is still 32 bits after the replacement. The output value of the F function can be obtained here.

* Inverse initial permutation

	After DES completes 16 rounds of transformation, 64bits data is obtained as the input of the IP-1 inverse initial permutation. After passing through the IP-1 inverse initial permutation table (as shown in Table 3), the 64bits input data positions are rearranged, and the 64bits ciphertext is obtained.
	
		40 8 48 16 56 24 64 32 39 7 47 15 55 23 63 31
		38 6 46 14 54 22 62 30 37 5 45 13 53 21 61 29
		36 4 44 12 52 20 60 28 35 3 43 11 51 19 59 27
		34 2 42 10 50 18 58 26 33 1 41  9 49 17 57 25


##### **AES**

The AES encryption algorithm is a block cipher. The block length is 128 bits or 16 bytes. The key length is 128, 192 or 256 bits. Depending on the key length, the number of encryption rounds is also different. This article uses a 128-bit key length. Key, the number of encryption rounds is 10. The AES encryption algorithm is not only compact in coding and simple in design, but also resistant to multiple types of attacks. Its basic structure includes 4 parts. These four parts are byte replacement, row displacement, column mixing and round key addition.

###### **Byte Substitution (SubBytes)**

Byte replacement is a non-linear transformation of byte elements through S-BOX. S-BOX is derived from the multiplicative inversion operation and affine transformation operation on the finite field GF (2 to the 8th power). Through table lookup The byte elements before and after the transformation can be directly obtained by Come. The specific replacement rule is that assuming one byte is xy, then the element corresponding to the xth row and yth column in S-BOX is the replaced element.

###### **Row displacement (ShiftRows)**

Row shift is a simple linear operation in the AES encryption algorithm, that is, in a 4 x 4 state matrix, the i-th row is cyclically shifted to the left by i bytes (i=0, 1, 2, 3).

###### **Column Mixing (MixColumns)**

Column mixing is to treat each column in the state matrix as a polynomial, multiply it by a fixed polynomial a(x), and then perform the operation of the modular polynomial m(x) = x4 (the fourth power of x) + 1 , where a(x)='03'x3 (the third power of x) + '01'x2 (the square of x) + '01'x + '02'.

###### **Round Key Add (AddRoundKey)**

The round key addition transformation is to perform an XOR operation on the state matrix and the subkey obtained after key expansion. Therefore, the inverse transformation of the round key addition transformation is itself, where the subkey is the original key through the key expansion algorithm. owned.

###### **AES algorithm process**

The figure below is the flow chart of the entire algorithm

![enter image description here](https://images.gitbook.cn/1ecf72b0-40b9-11e9-9708-f529efc309cf)

The AES encryption algorithm first groups the 128-bit plaintext to obtain a 4x4 plaintext state matrix as the input of the algorithm, then selects the key matrix and performs a round of key addition transformation on the plaintext state matrix, and then undergoes 10 rounds of round function encryption. , the round function operations are byte replacement, row displacement, column mixing and round key addition. Since the column mixing in the last round will not improve security, but will slow down the algorithm operation speed, column mixing is discarded in this round. Transform. The decryption algorithm still has 10 rounds. Since the four rounds of the algorithm are all reversible transformations, the decryption process uses the same key as the encryption process to reverse the encryption operations of each round.


### Asymmetric encryption

Asymmetric encryption is also called public key cryptography. This technology was proposed to address the shortcomings of the private key cryptography system (symmetric encryption algorithm). Asymmetric encryption will generate two keys, namely the public key and the private key. Private Key, one key is used for encryption and the other key is used for decryption. Asymmetric encryption is characterized by complex algorithm strength and security that depends on the algorithm and key. However, due to the complexity of the algorithm, the encryption and decryption speed is not as fast as that of symmetric encryption and decryption. There is only one key in the symmetric cryptosystem, and it is non-public. If you want to decrypt, you must let the other party know the key. Therefore, ensuring its security is to ensure the security of the key. The asymmetric key system has two keys, one of which is public, so that there is no need to transmit the other party's key like a symmetric encryption. This way the security is much higher.

Commonly used asymmetric encryption algorithms include RSA, Elgamal, backpack algorithm, Rabin, D-H, ECC (elliptic curve encryption algorithm), etc.

#### Two classic asymmetric encryption algorithms

##### **RSA**

The RSA algorithm is a relatively mature and complete public key cryptography system in theory so far, and is a typical representative of asymmetric cryptography systems. The RSA algorithm is used in many aspects such as network and information security. In particular, the RSA algorithm is typically used in digital signatures in communications, which can realize the opponent's identity and non-repudiation verification. It has broad application prospects in identity authentication, information security, and e-commerce.

###### **RSA algorithm process**

The RSA algorithm consists of three parts: key generation, encryption algorithm and decryption algorithm.

The key generation process is as follows:

1. Generate two large prime numbers p and q;2. Calculate $n = p \times q$, Euler function $\varphi(n) =(p - 1)(q - 1)$
3. Select the integer e so that it meets the conditions: 1 < e < φ(n), and gcd(e,φ(n)) = 1 (Note: The gcd () function calculates the greatest common divisor of two numbers);
4. Calculate the inverse element d of e: d∙e ≡ 1 mod φ(n) (Note: Since gcd(e,φ(n)) = 1, d must exist);
5. The sequence pair (e, n) is the public key, which can be made public; (d, n) is the private key, which is kept secret.

The encryption algorithm process is as follows

Split the string to be sent into groups of length m < n, and then perform an encryption operation on the group m to obtain the ciphertext c: $c ≡(m)^e mod n$

The decryption algorithm process is as follows

After receiving the ciphertext c, the recipient uses his own private key to perform a decryption operation and obtains the plaintext m: $m ≡(c)^d mod n$

###### **RSA detailed algorithm design process**

Generation and testing of large prime numbers

The Miller-Rabin algorithm is a probability-based prime number testing method. In the generation of prime numbers in cryptography, because of its fast speed, simple principle, and easy implementation, it has become the best choice for prime number detection.

The Miller-Rabin algorithm is an improvement on Fermat's algorithm. Its operation steps are as follows:

1. Calculate m to satisfy n = (2r 2 to the rth power) m + 1;

2. Select a random number a ∈[1,n];

3. If am mod n = 1, or satisfy aim mod n = n - 1, then n passes the test of random number a;

4. Then test n t = 5 times with different desired values of a. If the result of each test is that n is a prime number, it will be determined with a high probability that n is a prime number. Assuming n passes t tests, the probability of an error in the determination result is 1/4t; if it passes only one test, the probability of an error in the prime number determination is 25%.

The flow chart is as follows:

![enter image description here](https://images.gitbook.cn/98eda050-40bc-11e9-a862-810d44501c84)

key e generation module

Through the large prime number generation module above, we can get the large prime number p and the large prime number q. According to the Euler function φ(n) =(p - 1)(q - 1), at the same time, the key e and φ(n) are relatively prime. , the key e can be calculated according to the Chinese Remainder Theorem.

The process is as follows:

![enter image description here](https://images.gitbook.cn/c0a467a0-40bc-11e9-8d0d-7b692d25b020)

Key d generation module

The large prime numbers p and q are obtained through the large prime number generation module and the key e generation module, according to $1 = ed mod ( p - 1) (q - 1)$ . Manual implementation generally uses linear inverse elements, and computers generally use the extended Euclidean method to find multiplicative inverse elements in the modular sense.

fast exponential algorithm

> Also known as: Matrix fast exponentiation

After getting e, you can encrypt it with the public key (e,n) to get the ciphertext C. In the RSA encryption process, in order to calculate ci ≡(mi)e mod n , a fast exponential algorithm is used. Describe the fast exponential algorithm as a triplet (M,E,Y) whose initial value is (M,E,Y) =(mi,e,1). Repeat the following steps:

①If E is an odd number, then Y = M*Y mod n, E = E - 1;
②If E is an even number, then X = X*X mod n, E = E/2.
Finally, when E = 0, then Y = X^E mod n.

RSA encryption and decryption algorithm design

The process is as follows:

![enter image description here](https://images.gitbook.cn/ff15f850-40bc-11e9-a862-810d44501c84)

##### **ECC**

Elliptic curve cryptography (ECC) is an asymmetric cryptographic algorithm based on elliptic curve mathematics. It is a cryptographic system based on the discrete logarithm problem of elliptic curves. With the advancement of large integer decomposition methods and the improvement of various aspects, the RSA algorithm is gradually unable to meet the current situation, and the demand for the ECC algorithm is gradually increasing. ECC has been widely used due to its obvious "short key" advantage, and has gradually been established as the digital signature standard for many encoding methods. Of course, ECC still has many unsolved problems, but this algorithm that references rich mathematical theories also confirms the feasibility of applying more mathematical theories to the field of cryptography.

First, the algorithm encryption principle is explained from a mathematical perspective. The mathematical basis of the ECC elliptic curve encryption algorithm is to utilize the computational difficulty of the elliptic curve discrete logarithm problem (ECDLP) in a finite field. The so-called elliptic curve refers to the Weierstraa equation. Its elliptic curve equation is as follows:

	y2 + a1xy + a2 y = x3 + a3x2 + a4 x + a5

The following is an illustration of the elliptic curve method

![enter image description here](https://images.gitbook.cn/afc83140-40bd-11e9-a862-810d44501c84)

Among them, the coefficient ai is defined in a certain domain (in the cryptographic algorithm, the previous continuous curve needs to be turned into a point on the finite domain, so ai is also defined in the finite domain). All points on the curve and an infinite point form a set together with the definition of addition (eg: a+b≡c (mod p)) to form the Abelian group. Since every point on the curve is a non-singular point, two points P and Q can be found on the elliptic curve, and the following relationship exists:

![enter image description here](https://images.gitbook.cn/c7d32150-40bd-11e9-a862-810d44501c84)

It can be seen that it is easier to find Q when m and P are known, but it is more difficult to find m and P from Q in reverse. Elliptic curve cryptography is designed and applied based on this mechanism.

###### **ECC series algorithm secp256k1 **

* 1 Introduction

secp256k1 is the most commonly used elliptic curve algorithm in blockchain projects. It originated from applications in Bitcoin and is used by most subsequent blockchain projects such as Ethereum. The first three letters sec in the name represent Standards for Efficient Cryptography (SEC), and the following p256K1 refers to the parameter 256-bit prime field. Secp256k1 is an elliptic curve based on the Fp finite field (also known as the Galois field). Due to the particularity of its special structure, its optimized implementation can achieve 30% higher performance than other curves. It has the following two obvious advantages:

1) Occupies very little bandwidth and storage resources, and the length of the key is very short.
2) Allow all users to use the same operations to complete domain operations.

Elliptic curve graph y^2 = x^3 + 7


Addition on an elliptic curve in the plane is defined geometrically in terms of where the line intercepts the curve. We won't discuss geometry here, except to say that it boils down to a set of equations involving real numbers. But we are not working in the field of real numbers, but in the finite field. Finite field p, where

p = 2^256 - 2^32 - 977

The choice of p here is relatively close to 2^256. It is not the largest prime number smaller than 2^256; there are many prime numbers between p and 2^256. Other factors also influence the choice of p. Note that we are not working on the integer mod p itself, but on an Abelian group whose addition laws are defined by elliptic curves on the integer mod p.


2. Compressed format and non-compressed format of key

Next, we select a base point g on the elliptic curve. The standard that defines secp256k1 says that g is 0279BE667EF9DCBBAC55A06295CE870B07029BFCDB2DCE28D959F2815B16F81798
in "compressed form" or

040x79BE667EF9DCBBAC55A06295CE870B07029BFCDB2DCE28D959F2815B16F81798483ADA7726A3C4655DA4FBFC0E1108A8FD17B448A68554199C47D08FFB10D4B8

In "uncompressed form".
The base point is a specially chosen point on the elliptic curve, so it is a pair of numbers mod p, rather than a single number.

This compression takes the form: given only x, you should solve for y. gives you x and y in uncompressed form. However, the numbers are slightly coded. In compressed form, the string begins with "02" or "03" and the remainder of the string is the hexadecimal representation of x. two values of y that will satisfy

y² = x³ + 7 mod p

And "02" or "03" tells you which one to choose. If the packed form starts with 02, the root with an even number of least significant bits is chosen. If the packed form starts at 03, the root whose least significant bit is an odd number is chosen. (Two roots will be added to p, and p is odd, so one of the roots will be even and one will be odd.)
Uncompressed form: Uncompressed will always start with 04. After this, follow the hexadecimal representation of x and y concatenated together.

Whatever the case, we have
x = 79BE667EF9DCBBAC55A06295CE870B07029BFCDB2DCE28D959F2815B16F81798 and y = 483ADA7726A3C4655DA4FBFC0E1108A8FD17B448A68554199C47D08FFB10D4B8


###### **ECC series algorithm curve25519/ed25519/x25519 **

1: Several famous elliptic curve equations and corresponding practical applications
1. Weierstrass curve and several elliptic curve public key algorithms based on Weierstrass curve

y^2 = x^3 + ax + b

2. Montgomery curve https://en.wikipedia.org/wiki/Montgomery_curve and Curve25519 key agreement algorithm based on Montgomery curve https://en.wikipedia.org/wiki/Curve25519

\begin{align} Montgomery curve By^2 &= x^3+Ax^2+x where A, B ∈ K and B(A^2 − 4) ≠ 0 \\ Curve25519 curve y^2 &= x^{ 3} + 486662x^{2} + x, the prime number domain is defined by the prime number 2^{255}-19\end{align}



3. Edwards Curve https://en.wikipedia.org/wiki/Edwards_curve and Ed25519 digital signature algorithm based on Edwards Curve https://ed25519.cr.yp.to/index.html

\begin{align} Edward curve x^2 + y^2 &= 1 + dx^{2}y^{2} \\ Ed25519 curve-x^{2}+y^{2} &= 1 - {\ frac {121665}{121666}} x^{2}y^{2} \end{align}



Two: 25519 curve
Curve25519 (X25519) is an elliptic curve algorithm for Montgomery Curve Diffie-Hellman key exchange. Ed25519 is an elliptic curve algorithm for Edwards Curve digital signature. They differ in the curve formula from the Weierstrass Curve specified by SECG, so they are incompatible. The algorithms of Montgomery Curve and Edward Curve can be "Time-constant", that is to say, no matter what the values they operate on, they take the same time, so "Time side channel" attack It has no effect on them.


Three: Introduction to Curve25519 and Diffie-Hellman key exchange
Curve25519 is currently the highest level Diffie-Hellman function, suitable for a wide range of scenarios, and was designed by Professor Daniel J. Bernstein. In cryptography, Curve25519 is an elliptic curve providing 128-bit security, designed for use in the Elliptic Curve Diffie-Hellman (ECDH) key agreement scheme. It is one of the fastest ECC curves and is not covered by any known patent.

Given a user's 32-byte key, curve25519 computes the user's 32-byte public key. Given the user's 32-byte key and another user's 32-byte public key, curve25519 calculates a 32-byte shared key for use by both users. This secret can then be used to authenticate both users and encrypt information. The equation is:

The prime number field p=2 is 255 minus 19, which is also the origin of the name 25519. The group rank is 2 raised to the 255th power +27742317777372352535851937790883648493,

The construction of Curve25519 avoids many potential implementation pitfalls. It is not subject to timing attacks, can accept any 32-byte string as a valid public key (except 0 in actual engineering applications), and does not need to verify whether a given point belongs to a curve. Or whether it is generated by base points. After the Snowden incident in 2013, it received a lot of attention and use. It is now widely used, including ssh, tls, OpenSSL, Libsodium, etc., and has actually become a substitute for the NIST P-256 elliptic curve algorithm (the former is widely suspected to have a backdoor ( back door))



1. Diffie-Hellman key exchange

1.1 Introduction

Diffie–Hellman key exchange, abbreviated as D-H, is a security protocol used by two parties to establish a shared secret key on an insecure communication network. With the shared secret key, this key can be used to encrypt interactive messages. . Since the keys ultimately used by both communicating parties are the same, it can be considered that the goal of the protocol is to create a symmetric key (symmetric keys and asymmetric keys can be learned by themselves). This protocol is also called Diffie-Hellman key agreement. The name is named after the inventor, which is in line with convention and has no other special meaning.

Diffie-Hellman key exchange itself is an anonymous (authentication-free) key exchange protocol. It is the basis of many authentication protocols and is used to provide forward security in the ephemeral mode of the Transport Layer Security Protocol. .


1.2 Exchange process

First has its own private key a, and Second has its own private key b. Both a and b are smaller than p, and the private key is absolutely confidential.

The exchange process is as follows:

1. First use the private key a to generate A. The process is as follows: A = g^a mod p, and then send it through the channel.

2. Second uses private key b to generate B. The process is as follows: B= g^b mod p, and then sends it through the channel.

3. After Frist receives B, execute B^a mod p = Fkey.

4. After Second receives A, execute A^b mod p =Skey.

  5.Fkey = Skey (Because the overall execution is Fkey = (g^b)^a mod p, and Skey=(g^a)^b mod p, so they are equal.)


To achieve the purpose of sharing the secret key, the communication between the two can encrypt the subsequent communication content through the public key Fkey. In the whole process, only g, p, A, and B are public and the private keys a and b are kept secret. Therefore, based on discrete logarithm operation, it is difficult for the enemy to crack the public key.



1.3 Security

The Diffie-Hellman key exchange itself does not provide authentication services for the communicating parties, so it may be attacked by a man-in-the-middle. An intermediary can successfully pretend to be B to A and A to B by performing two Diffie-Hellman key exchanges with A and B respectively in the middle of the channel. At this point an attacker can read any one person's information and re-encrypt the information before passing it to another person. Therefore, a mechanism that can verify the identity of both communicating parties is usually needed to prevent such attacks. There are many secure authentication solutions that use Diffie-Hellman key exchange. When A and B share a public key infrastructure, they can sign their return keys; STS and the IKE component of the IPsec protocol have become part of the Internet protocol.


Four: ED25519 signature process
Ed25519 uses the Twisted Edward curve. The biggest difference between the signature process and the signature process is that no random numbers are used. The signature result generated in this way is deterministic, that is, the result of signing the same message is the same every time. Generally speaking, random numbers are an important method in security measures, but the generation of random numbers is also a security risk. The famous Sony product PS3 key leak incident was caused by the problem of random number generation. If you are familiar with Schnorr, secp256k1, sm2 and other signature processes, you will easily understand that if the same random number r appears during the signature process, the private key will be easily calculated and leaked.



1. Ed25519 public key generation algorithm process

(1).Select 256 bit private key sk=(sk255, sk253,···, sk1, sk0)

(2) Perform SHA-512 operation on sk, that is, H(sk) = (h511,h510,···,h1,h0)2;

(3) Take the lower 256 bits of H(sk) and organize them into s=(0,1,h253,h252,···,h3,0,0,0)2;

(4) Do scalar multiplication A=sB=(x,y), where x=(x254,x253,···,x1,x0)2, y=(y254,y253,···,y1,y0)2 ;

(5) Compress the sB result and obtain the public key pk = (x0, y254, y253,···,y1,y0)2.



2. Ed25519 signature algorithm process

(1) Take the high 256 bits of H(sk) h=(h511,h510,···,h257,h256)2;

(2) Perform SHA-512 operation, r=H(h||M) mod L;

(3) Do scalar multiplication R'=rB=(x,y), where x=(x254,x253,···,x1,x0)2, y=(y254, y253,···,y1,y0) 2;

(4) Compress the rB result and get R=(x0,y254,y253,···,y1,y0)2;

(5) Perform SHA-512 operation, k=H(R||pk||M) mod L;

(6) Calculate S= (r+k·s) mod L;

(7) Return the signature result (R||S).



3. Ed25519 verification signature algorithm process


(1) Decompress R to point coordinate R’;

(2) Decompress pk to point coordinate A;

(3) Perform SHA-512 operation, k=H(R||pk||M) mod L;

(4) Verify whether SB=R’+kA is established. If it is established, the signature verification is successful.


### Hybrid encryption - practical application scenarios of symmetric encryption and asymmetric encryption

The so-called hybrid encryption is to combine symmetric encryption and asymmetric encryption in practical applications. We all know that asymmetric encryption algorithms are thousands of times slower than symmetric encryption algorithms, but in terms of protecting communication security, asymmetric encryption algorithms have advantages that symmetric encryption cannot match. Therefore, in actual applications, symmetric encryption and asymmetric encryption are used together. Take its advantages and remove its dross to achieve the purpose of perfect use.

Symmetric encryption technology, that is, dedicated key encryption technology or single-key encryption technology, the encryption key and the decryption key are the same, and the sender and receiver use the same set of public and private keys to encrypt or decrypt information. A key requirement for data encryption is having the same key to decrypt it. Because both communicating parties share a key, if the key is lost or leaked, the person who obtains the key can encrypt or decrypt the data. Therefore, the security of the key must be ensured to ensure the confidentiality of the message. This algorithm is relatively simple and has a relatively small amount of calculation. It is open to the network and can be encrypted efficiently. At the same time, there are shortcomings. First, the communicating parties negotiate a common key in a non-face-to-face manner, so the security of the negotiation process cannot be guaranteed. Second, both communicating parties use a unique key every time they transmit data. This makes symmetric encryption technology need to use and generate a large number of keys in an open network, and the management of keys becomes a great burden for users. Third, the symmetric encryption algorithm can only encrypt and decrypt data to ensure the confidentiality of the data, but it cannot verify the true identity of the communicating parties and cannot determine the integrity of the data.

Asymmetric key encryption technology consists of a public key and a private key to form a key pair. The public key is disclosed to the public and the private key is kept solely by the key holder. When communicating parties use asymmetric keys to encrypt and decrypt data, they must use matching public and private keys. It has two methods: one is that the sender uses the receiver's public key to encrypt the information, and the receiver uses its private key to decrypt the information. In this way, the receiver can receive encrypted data from multiple senders, and this encrypted data Only one user on the receiving end can interpret it; the other is that the sender uses its own private key to encrypt the information, and the receiver uses the other party's public key to decrypt the information. Such a message may be decrypted by multiple receivers. The advantage of asymmetric key encryption technology is that it simplifies the process of key issuance and management, and supports security authentication technologies such as digital signatures. The disadvantage is that the calculation process of encryption and decryption is particularly complex, and the speed of running data encryption and decryption is relatively slow.
