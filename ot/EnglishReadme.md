[![Chinese](https://img.shields.io/badge/Chinese-README-red)](README.md)

## Inadvertent transmission

### 1. Development status of inadvertent transmission

1981: Rabin first proposed the concept of oblivious transmission. In this protocol, the sender sends a secret message m, and the receiver successfully obtains the message with 1/2 probability.

1985: Even et al. proposed 1 out of 2 casual transmission. In the protocol, the sender has two secret messages m1 and m2, where m1 and m2 belong to {0, 1}. The receiver selects and recovers one of the messages, and the sender cannot know The receiver chooses which message.

1986: G.Brassard and others proposed the n-out-of-1 oblivious transmission protocol. This protocol was actually designed on the basis of 2-out-of-1 oblivious transmission. The protocol implemented n-out-of-1 oblivious transmission by calling n rounds of 2 out of 1 oblivious transmission protocols. protocol; then G. Brassard and others discovered that there were some small bugs in the protocol, and then they further designed the oblivious transmission protocol where n takes 1 by calling log2 to the nth power 2 takes 1 oblivious transmission protocol. From then on, n takes 1 1's oblivious transfer protocols have become an important research topic. This research topic has attracted more and more researchers to join. Some have designed enhanced protocols based on this protocol, and based on the assumption of the Diffie-Hellman difficulty problem, implemented an oblivious transmission protocol where n is 1, and even some based on homomorphism. That is, no one considers the oblivious transmission protocol for n to k.

1989: A group of smart people led by Bellare proposed an n-take-n-1 oblivious transfer protocol, and then Naor designed a non-trivial n-take-k oblivious transfer protocol by calling the 2-take-1 oblivious transfer protocol. Naor further proposed an adaptive oblivious transfer protocol.

Since then, oblivious transmission has entered a prosperous era. Zhang proposed an n-out-k oblivious transmission protocol for universities, Chengkangchu proposed a protocol with adaptive and non-adaptive query, and Zhao Chunming designed an n-out-k oblivious transmission protocol based on hidden certificates. Wang Fenghe Lattice-based oblivious transfer protocol. There are also many excellent friends who have designed many excellent algorithms...


### 2. Inadvertent transmission concept

Oblivious transmission (OT) is a protocol used by communicating parties to transmit secret messages. There are generally two parties involved. One party is the message sender or message holder, who owns n secret messages, and the other party is the message receiver, hoping Get k (k < n) messages in the hands of the sender. The protocol requires that the receiver should correctly obtain its own messages, and the sender does not know which messages the receiver has received.

The oblivious transfer protocol should meet the following conditions:

- Correctness: After the protocol is executed, the receiver can receive the encrypted message sent by the sender and can also correctly decrypt the message he selected.
- Receiver's privacy: After the protocol is executed, the sender cannot know which messages the receiver has selected, thus ensuring the confidentiality of the receiver's selection.
- Privacy of the sender: After the protocol is executed, the receiver can only obtain the messages he selected and will not know the messages other than those he selected.
- Anti-impersonation attack: Only the recipient recognized by the sender can obtain the secret message sent by the sender
- Resistance to replay attacks: The data previously transmitted between the sender and the receiver was monitored by the attacker using network means. The attacker used the public parameters of the communicating parties and the intercepted data, and was unable to learn the secret data owned by the sender and the receiver. specific choices.
- Anti-man-in-the-middle attack: The attacker intercepts the communication data of both parties, pretends to be the receiver and communicates with the sender to obtain the sender's secret message, and pretends to be the sender and receiver to prevent the receiver from discovering the interception and using other methods to terminate the execution of the agreement. Secure oblivious transfer protocols need to be resistant to such attacks.

Inadvertent transmissions can generally be divided into the following categories:

#### 1. 1 pick 1 inadvertent transmission

The sender encrypts the secret message M and sends it to the receiver. The sender cannot confirm whether the receiver successfully recovered the secret message M.

#### 2. Choose 1 of 2 Unintentional Transmission

The sender encrypts the secret messages M1 and M2 and sends them to the receiver. The receiver can only successfully recover one of the secret messages Mi i, which belongs to {1, 2}. The sender cannot determine whether the message recovered by the receiver is M1 or M2.

#### 3. n Select 1 Unintentional transmission

The sender encrypts n secret messages M1, M2, M3...Mn and sends them to the receiver. The receiver can only successfully recover one of the secret messages Mi i, which belongs to Zn. The sender cannot be sure that the message recovered by the receiver is M1. , M2, M3 ... Mn which one.


#### 4. n choose k inadvertent transmission

The sender encrypts n secret messages M1, M2, M3...Mn and sends them to the receiver. The receiver can only successfully recover K secret messages among them.

Ma1, Ma2 ... Mak, a1, ak belong to {1, n}

The sender cannot determine which K of M1, M2, M3...Mn the received Ma1, Ma2...Mak are.


The n-choose-k oblivious transmission protocol has general properties, and our entire shared discussion is based on the n-choose-k protocol algorithm model.


### 3. Several common unintentional transmission algorithm designs

The designs of n-choose-k oblivious transmission protocols that are currently popular on the market mainly include oblivious transmission protocols based on AES, RSA-based oblivious transmission protocols, elliptic curve-based oblivious transmission protocols, IBE public key system-based oblivious transmissions, and NTRU-based oblivious transmission protocols. The inadvertent transmission and the inadvertent transmission of hidden certificates based on anonymous verification, etc.

#### 1. Oblivious transfer protocol based on AES


#### 2. Unintentional transmission based on RSA

The n-choose-K inadvertent transmission designed by the RSA encryption algorithm was designed by Hung et al. The execution flow of the entire protocol is as follows:

Alice has n secret messages m1, m2, m3 ... mn, and agrees to inadvertently transmit K messages {mσ1, mσ2, mσ3 ... mσk} to the receiver Bob, {σ1, σ2 ... σk} ∈ {1, 2 ... n} is a choice of Bob. At the same time, Alice's RSA public key system public key is (e, N), and the decryption private key is d. Alice and Bob complete the oblivious transmission protocol through the following steps:

.：
     ![.：
](https://github.com/guoshijiang/cryptography/blob/master/img/rsaot.jpeg)

##### 2.1. Security analysis of the protocol

The security of the ciphertext in the protocol is based on the security of the RSA encryption algorithm. According to the introduction of the RSA encryption algorithm in the previous chapter, the third party cannot obtain the message M1 through the interactive data between Alice and Bob without Alice's decryption key. To Mn.

###### Recipient’s privacy protection

According to the execution process of the protocol and the security of the RSA encryption algorithm, it is obvious that only Alice can calculate
.：
     ![.：
](https://github.com/guoshijiang/cryptography/blob/master/img/rsabjy01.png)

However, Si is randomly selected by Bob and is kept secret from Alice. Alice cannot know which message Zi is calculated from based on Zi, so Alice cannot know Bob's choice. The privacy of Bob's choices is guaranteed.

###### Sender’s privacy protection

In this protocol, since Bob does not have Alice’s decryption private key d, where e = 1 mod Φn, according to the security of the RSA algorithm, Bob cannot pass any encrypted ciphertext.
.：
     ![.：
](https://github.com/guoshijiang/cryptography/blob/master/img/rsabjy002.png)

Obtain message Mi, i=1, 2, 3,... n; Therefore Bob cannot obtain other n - k messages, because Alice only decrypted k secret messages.


#### 3. Oblivious transmission based on elliptic curve

Zhu Kongru used the elliptic curve discrete logarithm problem and still has not found the sub-exponential time-level cracking advantage. Combined with the elliptic curve discrete logarithm problem, he constructed a new unintentional transmission. The entire protocol execution process is as follows:

##### Initialization phase

In the preprocessing stage of the oblivious transmission protocol, first construct a finite field Fq, define the elliptic curve E on the finite field Fq, take the points P and M on the elliptic curve, and the sender Alice is in the interval [1, n-1](n is the order of electricity P on the elliptic curve and is a prime number), randomly select an integer p as the private key of the algorithm, and calculate the point K = pM, where K is the public key of the algorithm, and K is also a point on the elliptic curve, Its coordinates are on the finite field Fq, and then Alice sends the public key K and the generating element point M to the receiver Bob. At this time Bob randomly selects i ∈ {0,1} as his option.

##### Transmission phase
The agreement is executed according to the following steps

(1) The sender Alice sends the generator M public key K to the receiver Bob

(2) After receiving M and K, the receiver Bob performs the following steps:

- Randomly choose an integer ai ∈ Fq
- Randomly select an integer bi on the interval [1, n-1]
- Calculate point (x1, y1) = biM, (x2, y2) = biK (if x2=0, reselect bi until x2 is not equal to 0)
- Calculate si = ai * x1, then randomly select the ciphertext s1-i ∈ Fq, and finally send the ciphertext pair (s0, s1) and (x1, y1) to Alice


(3). Since Alice knows the private key p, the plaintext pair (a0, a1) can be calculated from the ciphertext (s0, s1). The specific calculation process is as follows

- Calculate (X2, y2) = p(x1, y1) using the private key p and the point (x1, y1);
- Let j = 0,1, and then calculate aj = sj * x2 to the -1 power to obtain the information of plaintext aj
- Let j = 0,1, let cj ^ i = cj xor Lj, where cj is the bit Alice inadvertently transmitted and Lj is the least significant bit of plaintext aj.
- Send c0 and c1 to Bob

(4) Since Bob knows aj, he can recover the content of ci by calculating the i-th power XOR Li of cj. The specific execution process is as follows:
.：
     ![.：
](https://github.com/guoshijiang/cryptography/blob/master/img/eccot4.jpeg)

From the execution process in the above figure, we can know that if the recipient is an honest participant, the plaintext a1-i cannot be guessed. The reason is that the discrete pair mathematics is difficult to understand. He guarantees that even if the receiver knows the ciphertext, points (x1, y1), M and K cannot calculate the values of b1-i and b1-i * K in polynomial time, which shows that the receiver can only Bits are obtained and the value of c1-i cannot be calculated. In addition, for the sender, the ciphertext pair (s0, s1) is completely equivalent, and there is no way to know whether the receiver chose c0 or c1.

Based on the above analysis, it can be known that if the participants of the protocol strictly follow the steps of the protocol, then the above protocol can inadvertently transmit bits c0 and c1 from the sender to the receiver.

#### 4. Unintentional transmission based on IBE public key system

This section will introduce the construction of an n-k oblivious transmission protocol based on the identity-based encryption system designed by Boneh. At the same time, the correctness, security analysis of the protocol, and protocol execution efficiency analysis are given.


#### 5. Inadvertent transmission of hidden certificates based on anonymous verification



#### 6. NTRU-based inadvertent transmission



### 4. Applications of inadvertent transmission

A protocol in MPC, mainly used for data privacy protection.


### 5. Summary

Oblivious Transfer Protocol is a privacy-preserving communication protocol that enables communicating parties to transmit messages between each other in a selectively obfuscated manner. OT is a basic protocol in cryptography. It allows the recipient of the service to obtain certain messages input by the sender of the service in an inadvertent way. This way, the privacy of the recipient can be protected from being known by the sender and the recipient is not known either. The sender specifically sent what message.
