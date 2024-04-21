[![Chinese](https://img.shields.io/badge/Chinese-README-red)](README.md)

# Chapter M: Secret Sharing

The development of cryptography can be traced back to 400 BC, and humans have been using cryptography almost as long as writing. Before 400 BC, the Spartans invented the "Theta cipher". In ancient China, the shadow of cryptography also appeared. Everyone should know the ancient Chinese acrostic poems, which also fall into the category of cryptography. War has played a big role in the development of cryptography. From ancient times to the present, the technologies used by the military are the most advanced in the world, including cryptography. The cryptography system is already a complete subject system in today's era. There are many experts and scholars around the world who have contributed to the development of cryptography throughout their lives. The symmetric cryptography, asymmetric cryptography, digital signatures, single-term hash functions, PKI systems, shared passwords, etc. that we are now familiar with can all be a direction worthy of in-depth study. This article will lead you to understand some technologies related to shared secrets, and I hope you can learn some knowledge about shared passwords.

### The development history of shared keys

Secret sharing is an important branch of information security research. Passwords are mainly used to encrypt important information and ensure the security of information. However, secret sharing can ensure the security of keys. It provides a platform for the development of cryptography. Fresh ideas. The principle of secret sharing is to divide the secret into several parts and hand them over to different people for safekeeping. If a certain number of people manage the secret contribute their own secrets, the secret can be restored.

#### 1.1 The generation of secret sharing

The concept of secret sharing was first independently proposed by the famous cryptographers Shamir and Blakley in 1979 and gave their own solutions. Shamir's (t, n) threshold scheme is implemented based on Lagrnage (Lagrangian) interpolation method, and Blakley's (t, n) threshold scheme is established by utilizing the properties of multi-dimensional space points.

Once the concept of secret sharing was proposed, it received great attention and research from experts and scholars. A lot has been achieved over the years. It can be roughly divided into the following categories.

##### **1.1.1 Threshold secret sharing scheme**

In the (t, n) threshold secret sharing scheme, any set containing at least t participants is an authorized subset, while a set containing t-1 or less participants is an unauthorized subset, achieving (t, n ) Threshold secret sharing methods include Shamir and Blakley's scheme, the Asmuth-Bloom method based on the Chinese Remainder Theorem, and the Karnin-Greene Hellman method using matrix multiplication.

##### **1.1.2 Secret sharing scheme on general access structure**

The threshold scheme is a secret sharing scheme that implements a threshold access structure. It has limitations for other broader access structures, such as sharing secrets among four members A, B, C, and D, so that A and D or B and C can cooperate to restore Secret and threshold secret sharing schemes cannot solve such a situation. To address this type of problem, cryptography researchers proposed a secret sharing scheme based on a general access structure in 1987. In 1988, someone proposed a simpler and more effective method - the monotonic circuit construction method, and proved that any access structure can be realized through a complete secret sharing scheme.

##### **1.1.3 Multiple secret sharing scheme**

Only one sub-secret can be protected to share multiple secrets. In a multiple secret sharing scheme, each participant's sub-secret can be used multiple times, but only one secret can be shared in one secret sharing process.

##### **1.1.4 Multiple secret sharing scheme**

Multiple secret sharing solves the problem of participant's sub-secret reuse, but it can only share one secret during a secret sharing process.

##### **1.1.5 Verifiable secret sharing scheme**

Members participating in secret sharing can verify the correctness of the sub-secrets they own through public variables, thus effectively preventing mutual deception between distributors and participants, as well as between participants. Verifiable secret sharing schemes are divided into two types: interactive and non-interactive. The interactive verifiable secret sharing scheme means that each participant needs to exchange information with each other when verifying the correctness of the secret share; the non-interactive verifiable secret sharing means that each participant does not need to exchange information when verifying the correctness of the secret share. Information needs to be exchanged between each other. In terms of applications, non-interactive verifiable secret sharing can reduce network communication costs and reduce the chance of secret leaks, so the application fields are broader.

##### **1.1.6 Dynamic secret sharing scheme**

The dynamic secret sharing scheme was proposed in 1990. It has good security and flexibility. It allows adding or deleting participants, updating participants' sub-secrets regularly or irregularly, and recovering different secrets at different times, etc. . The above are several classic secret sharing schemes. It should be noted that a specific secret sharing scheme is often a collection of several types.

##### **1.1.7 Other secret sharing**

  Quantum secret sharing, visual secret sharing, secret sharing based on multi-resolution filtering, secret sharing based on generalized self-shrinking sequences.

### Introduction to the classic secret sharing scheme

#### 2.1 shamir threshold secret sharing scheme

Shamir's (t, n) threshold scheme is implemented based on the Lagrnage (Lagrange) interpolation method. Simply put, assume that the secret is distributed to members through the secret sharing algorithm, and each member holds a sub-key, also known as Shadow or Secret debris, if:

* Any valid member of not less than t can recover the secret using the correct fragment he holds.
* Any set with less than t members cannot recover the secret.

We call this scheme a (t,n) threshold secret sharing scheme, referred to as the threshold scheme, and t is called the threshold value of the scheme.

As the simplest and most practical threshold secret sharing scheme among various secret sharing schemes, the (k,n) threshold secret sharing scheme is also the most representative and widely used scheme among these schemes.

Below is a brief introduction to this solution.

##### **2.1.1 System parameters**

Assume that n is the number of participants, n is the threshold value, and p is a large prime number requiring p > n and greater than p. The maximum possible value of secret s; both the secret space and the share space are finite fields GF(p).

##### **2.1.2 Secret Distribution**

The process of secret distributor D allocating shares to n participants Pi (0 ≤ i ≤ n), that is, the allocation algorithm of the plan is as follows:

* Randomly select a polynomial of degree k - 1 on GF(p) such that f(0) = a0 = s The secret D to be shared among participants is kept secret from f(x).

* D selects n different non-zero elements x1, x2, …, xn in Zp and calculates (0≤ i ≤ n).

* Assign (xi, yi) to participant Pi(0 ≤ i ≤ n), the value xi is public, and yi is the secret share, which is not public.

##### **2.1.3 Secret Reconstruction**

Given any t points, let them be the first t points (x1, y1), (x2, y2),…, (xt, yt). By the interpolation formula:

![enter image description here](https://images.gitbook.cn/597d0a10-3de6-11e9-83a7-c387b6fac45c)

As a widely used threshold scheme, the Shamir scheme has the following advantages:

* t secret shares determine the entire polynomial, and other secret shares can be calculated.

* While the secret share of the original sharer remains unchanged, new sharers can be added, as long as the total number of new sharers does not exceed the number.

* You can also recalculate the share of the sharer's secret in the new round by constructing a second-order polynomial with new coefficients whose constant term is still the shared key before the original shared key is exposed, thereby invalidating the sharer's original secret share. .

But at the same time, the plan has the following problems

* During the secret distribution phase, dishonest secret distributors can distribute invalid secret shares to participants

* During the secret reconstruction phase, some participants may submit invalid secret shares making it impossible to recover the correct secret.

* A point-to-point secure channel is required between the secret distributor and participants.

#### 2.2 Secret sharing scheme based on Chinese Remainder Theorem

The Chinese Remainder Theorem first appeared in the ancient Chinese mathematics masterpiece "Sun Tzu Suan Jing", so it is also called Sun Tzu's Theorem. The Chinese Remainder Theorem is widely used in cryptography.

Let p1, p2,...,pm represent m pairwise relatively prime positive integers. Given any m integers, k1,k2,k3,...,km, there is a unique integer K belonging to GF(p1p2..., pm) that satisfies:

      K = K1 mod p1
   	K = K2 mod P2
   	......
   	K = Km mod Pm

In 1983, cryptography experts proposed two secret sharing schemes based on the Chinese Remainder Theorem. The overall ideas are as follows.

##### **2.2.1 Initialization phase**

Let P = {p1, p2, ... , Pn} be the set of participants. {p, d1, d2, ... dn} is a set of integers that satisfy the following conditions.

* s < p, s is the secret that needs to be shared.
* d1 < d2 < ... dn.
* For i = 1,2, ..., n, there is gcd(di, p) = 1, where gcd(x, y) represents the greatest common divisor of x and y.
* For all i not equal to j, gcd(di, dj) = 1.
* d1d2...dk > pdn-t+2dn-k+3...dn.

Article 5 means that the product of the smallest k di is greater than the product of p and the k-1 largest di.

##### **2.2.2 Secret Distribution Phase**
Let N = d1d2...dt, then N/p is greater than the product of any k-1 di. Let r be a random number in [0, N/p-1]. In order to divide the secret s into n parts, the secret distributor D calculates s' = s + rp, where s' is limited to [0, N - 1], then the subkey xi of each participant Pi is :

      xi = s' mod (di)


##### **2.2.3 Key reconstruction phase**

For any k participants, let's assume that P1, P2, ... Pk take out their k sub-keys x1, x2, ... xk, and the corresponding module can be obtained from the Chinese Remainder Theorem:

      N1 = d1d2 ...dk

Because N1 is greater than or equal to N, s' can be uniquely determined by the Chinese Remainder Theorem. The key can then be calculated from s', r, p:

      s = s'-rp
	

If we only know k-1 sub-milangs, although s' can be known from N2,
	
      N2 = d1d2 ...dk-1
However, since N/N2 > p, and gcd(N2, p) = 1, the number x that makes x greater than or equal to N and x=s'mod(p) is uniformly distributed on the congruence class modulo p, so there is no Enough information to decide s'. In this solution, the time complexity of the dense steel recovery algorithm is O(k) and the space complexity is O(n).

### Verifiable secret sharing

Common key sharing schemes assume that the key distributor is honest. This leads to a major security problem in basic key sharing: it cannot prevent the key distributor from being spoofed, that is, the distributor may distribute forged subkeys to one or more participants when distributing subkeys. To solve this problem, Chor et al. proposed the concept of verifiable key sharing. Verifiable key sharing is a common secret sharing scheme plus an interactive algorithm that allows participants to authenticate the subkeys they receive. Participants can use the authentication algorithm to verify whether their subkeys are valid. Verifiable key sharing can be divided into two categories: conditionally secure and verifiable secret sharing and unconditionally secure and verifiable key sharing. Below we introduce several representative verifiable secret sharing schemes.

#### 3.1 Feldman’s solution

Feldman proposed a verifiable Shamir sharing scheme based on Shamir's key sharing scheme. Below we introduce the detailed process of this algorithm:

##### **3.1.1 Initialization phase**

Suppose p is a large prime number, q is a large prime factor of p -1, g belongs to Z*p and is an element of order q, the triplet (p, q, g) is common, k is the threshold value, n is the number of participants and s is the secret key to be shared.

##### **3.1.2 Sub-secret distribution stage**

The Mirang dealer selects a random polynomial f(x) of degree k-1 belonging to Zq(x) such that f(0) = s. That is, randomly select random numbers a1, a2, ..., ak-1 in Zq and construct a polynomial

![enter image description here](https://images.gitbook.cn/2a7642d0-3e50-11e9-acbf-6f04514d907d)

Subsequently, the subkey mi = f(i) mod (q) is calculated and cryptographically sent to the participant Pi, and the verification information is broadcast.
![enter image description here](https://images.gitbook.cn/416e3c40-3e50-11e9-acbf-6f04514d907d).


##### **3.1.3 Verification Phase**After receiving the subkey, participant Pi (i = 1, 2, ..., n) can check Eq.

![enter image description here](https://images.gitbook.cn/821f35a0-3e50-11e9-acbf-6f04514d907d)

Whether it is established to verify the correctness of Zi Milang. If the equations are equal, it means that the sub-crypto owned by participant Pi is correct, otherwise it means that the sub-crypto received is incorrect.

##### **3.1.4 Secret Recovery Phase**

When k participants, let's say P1, P2, ..., Pn, cooperate to recover mi, each participant Pi must disclose his subkey share mi. At this time, any participant can verify the correctness of other participants' subkeys by verifying the above equation. If all public sub-mitrans are verified to be correct, then the key can be recovered by the Lagrangian interpolation function.

It can be seen that in Feldman's scheme, the key to verifying the correctness of the submilang is that the key distributor publishes the verification information aj = gaj mod p, j = 1, 2, 3, ..., k. Among them, g and p are common, and the verification information aj is the discrete logarithm of aj. Based on the difficulty of the discrete logarithm problem, aj and (g, p) cannot be calculated from the verification information. It can be seen that the security of Feldman's scheme is based on the difficulty of the discrete logarithm problem, so it is conditionally safe. In addition, we can also see from the key recovery stage that when participants disclose their own subkeys, all participants can use the information in the key distribution stage to verify the correctness of other participants' subkeys. , which actually solves the problem of deception among participants during the recovery process of Milang.

#### 3.2 Benaloh scheme

Benaloh's verifiable secret sharing scheme is also based on Shamir's secret sharing scheme. Unlike Feldman's scheme, Benaloh's scheme is unconditionally safe. First, we introduce the main idea of ​​Benaloh's verifiable algorithm. In the key sharing scheme, the subkeys of all participants come from a linear polynomial of degree k - 1. If the key distributor distributes one or more wrong subkeys, then these n subkeys will The keys will inevitably be inconsistent, and the degree of their interpolation polynomial will be greater than k -1 with a high probability. In other words, if we can find the degree of the interpolation polynomials of these sub-keys without revealing the sub-key information, then we can verify the validity of the sub-keys. Benaloh's scheme uses this property to verify Shamir's key sharing scheme. The specific algorithm is as follows:

##### **3.2.1 Initialization phase**

Let q be a large prime number, s belongs to Zq and be the key to be shared. k is the threshold and n is the number of participants.

##### **3.2.2 Subkey distribution phase**

The key distributor (dealer) chooses a random polynomial of degree k -1 f(x) = Zq(x) such that f(0) = s. Subsequently, the subkey mi = f(i) mod (q) is calculated and encrypted to the participant Pi.

Next, the key distributor randomly selects multiple (maybe 100) polynomials of degree k-1 on Zq(x), f1(x), f2(x), ..., f100(x). And calculate and send 100 verification subkeys mij (mij represents the jth power of mi) for each participant Pi, j = 1, 2, … 100, where. mij = fj(i).

##### **3.2.3 Verification Phase**

All participants collaborate to randomly select 50 groups (one group contains n) of verification subkeys, make them public, and verify whether these 50 groups of verification subkeys are all polynomials of degree k-1. Since these 50 sets of verification subkeys are randomly selected by participants, if they all originate from polynomials of degree k-1, then participants can think that the remaining 50 sets of undisclosed subkeys also originate from k-1 degree polynomial.

Next, all participants disclose the sum of the sub-mild and any remaining undisclosed verification sub-key, and verify whether the n values ​​are derived from a polynomial of degree k-1. If so, then according to the linear properties of the interpolation polynomial, it can be inferred that this n-sub secret is also derived from a polynomial of degree k-1. Thereby verifying the validity of the subkey. On the contrary, the sub-milang is inconsistent, and the min-rang distributor makes an error in the process of calculating and distributing the sub-milang.

##### **3.2.4 Key recovery phase**

After the validity of the subkey is verified, any k participants can recover the key using the Lagrangian interpolation formula.


From the above algorithm, we can see that in Benaloh's scheme, the key distributor does not publish any verification information, and the entire verification algorithm does not rely on any difficult problem assumptions, so Benaloh's verifiable key sharing scheme is unconditionally secure. . However, in order for each participant to verify the validity of the subkey, they need to store 100 verification subkeys, which places high demands on the storage space of each participant. In addition, from the perspective of verification effect, Benaloh's scheme can only verify whether there is an incorrect sub-key, but cannot determine which sub-key is incorrect. Compared with Feldman's scheme, this scheme is weaker in verification effect, and participants require larger storage space, which will cause a certain degree of security issues. But this is also the price that must be paid to achieve unconditional security.


### Decentralized secret sharing solution

Since the birth of key sharing schemes, a large number of key sharing schemes in different environments have been proposed. Most schemes assume the existence of a trusted central key distributor who is responsible for splitting the key into subkeys and sending the subkeys to the participants securely. However, in actual environments, trusted centers often do not exist. Therefore, a new secret sharing protocol without a trusted center is proposed to adapt to the environment without a trusted center.

In key sharing without a trusted center, the generation and distribution of sub-milangs are completed by the cooperation of the participants themselves. In practical applications, Milang sharing with a trusted center may have "authority deception" by the trusted center, and it is not a wise assumption to require members to have high credibility in reality. Therefore, compared with key sharing with a trusted center, key sharing without a trusted center is more secure and more practical.

The main purpose of research on key sharing without a trusted center is to find a suitable solution to ensure that information can be released and transmitted safely and effectively. In addition, how to distribute subkeys in secret sharing without a trusted center is a hot topic of research, and there is still a lot of room for development. Therefore, key sharing without a trusted center not only has important theoretical value, but also has broad application prospects in practical applications. Mutian's application for secret sharing without a trusted center mainly focuses on digital signatures. There are not many cryptographic studies on secret sharing without a trusted center. The following is a decentralized secret sharing solution proposed by the author personally.

The decentralized key sharing solution actually splits the key into n parts, encrypts each secret, and then stores them on the blockchain, which can solve the problem of key distribution and storage. After the key is sent to the corresponding node, the node first encrypts the key twice, signs it, and then writes it to the blockchain. When the key restorer needs to restore the key, it can broadcast a recovery key to the entire network information, and then pay a certain token to the key segment storage node. The key storage node verifies the key and decrypts it before sending it to the client who recovers the key. In this way, the goal of decentralized secret sharing can be achieved.

### (t,n) threshold dynamic secret sharing scheme

In 1979, Shamir and Blakley respectively proposed a (t, n) threshold secret sharing scheme. Shamir's (t, n) threshold scheme is implemented based on the Lagrange interpolation method, which constructs a t-1 degree polynomial, and the secret to be shared is used as the constant term of the polynomial. Each share (sub-secret) is a coordinate point that satisfies the polynomial. According to the Lagrange interpolation theorem, any t shares (sub-secrets) can reconstruct the The polynomial thus recovers the secret, while t-1 or fewer shares (sub-secrets) cannot reconstruct the polynomial and thus gain no information about the secret.

The proposal of dynamic secret sharing system mainly stems from the security issue of secret sharing scheme. In the (t, n) threshold secret sharing scheme, the security of the scheme is based on the premise that the attacker cannot obtain t sub-secrets within the life cycle of the secret. However, it is difficult to guarantee this in practice, especially when the life cycle of the secret is long. The verifiable secret sharing scheme is mainly used to solve the problem of distributor dishonesty and sub-secret holder dishonesty in traditional secret sharing schemes. However, in the face of destructive attacks by adversaries, the verifiable secret sharing scheme does not change. Good security.

Of course, periodic security can be solved by constantly changing secrets, but changing secrets is not always feasible (for example, if the secret is an important document or some military or commercial secrets, etc.). The dynamic secret sharing scheme solves the periodic security problem of the secret sharing scheme without changing the secret. The dynamic secret sharing scheme periodically replaces the sub-secret while ensuring that the secret remains unchanged, so that the information obtained by the attacker in the previous cycle is completely invalid every time the sub-secret is replaced.

In this way, the length of the sub-secret replacement cycle can be determined accordingly based on the degree of possible attacks to ensure the security of the secret in each cycle. Dynamic secret sharing also ensures that the information contained in expired sub-secrets will not have an unsafe impact on the construction of future secrets.

#### 5.1 Amir Herzberg Solution

There are many schemes for dynamic secret sharing. The scheme proposed by Amir Herzberg is a very classic one. The scheme is to make Shamir's secret sharing scheme dynamic.

Distributor D selects a finite field GF(q) (q is a large prime number). For convenience of explanation, i is used to replace xi in Shamir's scheme. At the kth period, the sub-secret held by Pi is represented by si(k)(si raised to the kth power).

Sub-secret update protocol: The sub-secret is updated at the beginning of each period. After entering the k-th period, the sub-secret held by Pi is updated from si(k-1) =f(k-1)(i) to si( k), where f(k-1) (0) = s. The whole process is as follows:

    ![enter image description here](https://images.gitbook.cn/a3e42e10-3e65-11e9-b565-378070432200)

The updated sub-secret obviously meets the requirements of threshold secret sharing, and the secret can be recovered by any number of participants greater than or equal to t using Lagrange interpolation. Later, Amir Herzberg and others further proposed a sub-secret update scheme to prevent active attacks in their article, and added verifiability, further strengthening the security of the scheme.

#### 5.2 Improvement of Amir Herzberg’s scheme

In fact, Amir Herzberg's sub-secret update scheme is equivalent to n participants negotiating a t-1 degree polynomial with a constant term of zero. In fact, less than n participants can also perform sub-secret update. The steps are the same as the original scheme. If the number of participants participating in sub-secret update is less than the threshold value t, this scheme can be improved to make it have better flexibility and execution efficiency. The scheme is described as follows:
![enter image description here](https://images.gitbook.cn/edf6bc20-3e65-11e9-9e3c-c5b76bc0f4a1)

##### **5.2.1 Improvement Analysis of Amir Herzberg’s Plan**

![enter image description here](https://images.gitbook.cn/32725210-3e66-11e9-9e3c-c5b76bc0f4a1)

In this way, k (k<t) participants can update the sub-secret, and this scheme has great flexibility. In step (3), it only needs to update i in si′=si+χ·i ic The threshold value can be increased by modifying the order so that the order is greater than t-k, such as si′=si+χ·iit-k+θ. The threshold value in the scheme is t+θ, which is equivalent to changing the polynomial storing the secret s. is a polynomial of degree t+θ-1. Since members participating in the sub-secret update only need to select a random number and perform a simple direct sum decomposition operation, the execution efficiency is very high compared with the original solution. Since information is transmitted through a secure channel, security can be guaranteed. Amir Herzberg's sub-secret update scheme is equivalent to n participants negotiating a t-1 degree polynomial with a constant term of zero. Given that the number of participants participating in the sub-secret update is less than the threshold value t, the sub-secret update can also be performed, and Have better flexibility and execution efficiency. Further consideration, when the number of people participating in the sub-secret update is greater than or equal to the threshold value, that is, when k ≥ t, this scheme can still update the sub-secret, but the threshold value will change, which is not suitable for keeping the threshold value unchanged. When the situation changes, the solution is more flexible when there is no k<t.

### Threshold key sharing code implementation (Java)

#### 6.1 Code pom file

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

#### 6.2 Core code

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

#### 6.3 Code tool class

##### **6.3.1 Combination code**

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

##### **6.3.2 Hex Code**

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

#### 6.4 Directory structure of code

![enter image description here](https://images.gitbook.cn/7c6405f0-3e4b-11e9-a98d-5dc2d0f56a42)

If you have any questions, please contact me directly! Email: `guoshijiang2012@163.com` or `20123762@s.hlju.edu.cn`
