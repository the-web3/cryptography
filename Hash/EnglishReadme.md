[![Chinese](https://img.shields.io/badge/Chinese-README-red)](README.md)


# Chapter 4: One-way hash function

## 1. Introduction
One-way hash function, also known as one-way Hash function and hash function, is a function that changes an input message string of any length into a fixed-length output string and makes it difficult to obtain the input string from the output string. This output string is called the hash value of the message. Generally used to generate message digests, key encryption, etc.


## 2. MD5 algorithm

### 1. Introduction to MD5

MD5: It is a one-way hash algorithm developed by RSA Data Security Company. MD5 is widely used and can be used to cryptographically operate data blocks of different lengths into a 128-bit value. Different values produce different results.

### 2.MD5 algorithm process

A brief description of the MD5 algorithm can be as follows: MD5 processes input information in 512-bit groups, and each group is divided into 16 32-bit sub-groups. After a series of processing, the output of the algorithm consists of four 32-bit sub-groups. Composed of groups, concatenating these four 32-bit groups will generate a 128-bit hash value.

The first step, filling: If the length (bit) of the input information is not equal to 448 after the remainder of 512, you need to fill it so that the result of the remainder of 512 is equal to 448. The filling method is to fill a 1 and n 0s. After filling, the length of the information is N*512+448 (bit)

The second step is to record the information length: use 64 bits to store the information length before filling. These 64 bits are added after the result of the first step, so that the information length becomes N*512+448+64=(N+1)*512 bits.

The third step is to load the standard magic numbers (four integers): The standard magic numbers (physical order) are (A=(01234567)16, B=(89ABCDEF)16, C=(FEDCBA98)16, D=( 76543210)16). If defined in the program, it should be: (A=0X67452301L, B=0XEFCDAB89L, C=0X98BADCFEL, D=0X10325476L).


Step 4, four rounds of loop operation: the number of loops is the number of groups (N+1)

1) Subdivide each 512 bytes into 16 subgroups, each subgroup is 64 bits (8 bytes)

2) First understand the four linear functions (& is AND, | is OR, ~ is NOT, ^ is XOR)

```
F(X,Y,Z)=(X&Y)|((~X)&Z)
G(X,Y,Z)=(X&Z)|(Y&(~Z))
H(X,Y,Z)=X^Y^Z
I(X,Y,Z)=Y^(X|(~Z))
3) Let Mj represent the j-th subgroup of the message (from 0 to 15)

FF(a,b,c,d,Mj,s,ti) means a=b+((a+F(b,c,d)+Mj+ti)<<<s)
GG(a,b,c,d,Mj,s,ti) means a=b+((a+G(b,c,d)+Mj+ti)<<<s)
HH(a,b,c,d,Mj,s,ti) means a=b+((a+H(b,c,d)+Mj+ti)<<<s)
II(a,b,c,d,Mj,s,ti) means a=b+((a+I(b,c,d)+Mj+ti)<<<s)
```

4) Four rounds of operations
  first round
 
```
a=FF(a,b,c,d,M0,7,0xd76aa478)
b=FF(d,a,b,c,M1,12,0xe8c7b756)
c=FF(c,d,a,b,M2,17,0x242070db)
d=FF(b,c,d,a,M3,22,0xc1bdceee)
a=FF(a,b,c,d,M4,7,0xf57c0faf)
b=FF(d,a,b,c,M5,12,0x4787c62a)
c=FF(c,d,a,b,M6,17,0xa8304613)
d=FF(b,c,d,a,M7,22,0xfd469501)
a=FF(a,b,c,d,M8,7,0x698098d8)
b=FF(d,a,b,c,M9,12,0x8b44f7af)
c=FF(c,d,a,b,M10,17,0xffff5bb1)
d=FF(b,c,d,a,M11,22,0x895cd7be)
a=FF(a,b,c,d,M12,7,0x6b901122)
b=FF(d,a,b,c,M13,12,0xfd987193)
c=FF(c,d,a,b,M14,17,0xa679438e)
d=FF(b,c,d,a,M15,22,0x49b40821)
```

second round

```
a=GG(a,b,c,d,M1,5,0xf61e2562)
b=GG(d,a,b,c,M6,9,0xc040b340)
c=GG(c,d,a,b,M11,14,0x265e5a51)
d=GG(b,c,d,a,M0,20,0xe9b6c7aa)
a=GG(a,b,c,d,M5,5,0xd62f105d)
b=GG(d,a,b,c,M10,9,0x02441453)
c=GG(c,d,a,b,M15,14,0xd8a1e681)
d=GG(b,c,d,a,M4,20,0xe7d3fbc8)
a=GG(a,b,c,d,M9,5,0x21e1cde6)
b=GG(d,a,b,c,M14,9,0xc33707d6)
c=GG(c,d,a,b,M3,14,0xf4d50d87)
d=GG(b,c,d,a,M8,20,0x455a14ed)
a=GG(a,b,c,d,M13,5,0xa9e3e905)
b=GG(d,a,b,c,M2,9,0xfcefa3f8)
c=GG(c,d,a,b,M7,14,0x676f02d9)
d=GG(b,c,d,a,M12,20,0x8d2a4c8a)
```

third round

```
a=HH(a,b,c,d,M5,4,0xfffa3942)
b=HH(d,a,b,c,M8,11,0x8771f681)
c=HH(c,d,a,b,M11,16,0x6d9d6122)
d=HH(b,c,d,a,M14,23,0xfde5380c)
a=HH(a,b,c,d,M1,4,0xa4beea44)
b=HH(d,a,b,c,M4,11,0x4bdecfa9)
c=HH(c,d,a,b,M7,16,0xf6bb4b60)
d=HH(b,c,d,a,M10,23,0xbebfbc70)
a=HH(a,b,c,d,M13,4,0x289b7ec6)
b=HH(d,a,b,c,M0,11,0xeaa127fa)
c=HH(c,d,a,b,M3,16,0xd4ef3085)
d=HH(b,c,d,a,M6,23,0x04881d05)
a=HH(a,b,c,d,M9,4,0xd9d4d039)
b=HH(d,a,b,c,M12,11,0xe6db99e5)
c=HH(c,d,a,b,M15,16,0x1fa27cf8)
d=HH(b,c,d,a,M2,23,0xc4ac5665)
```

fourth round

```
a=II(a,b,c,d,M0,6,0xf4292244)
b=II(d,a,b,c,M7,10,0x432aff97)
c=II(c,d,a,b,M14,15,0xab9423a7)
d=II(b,c,d,a,M5,21,0xfc93a039)
a=II(a,b,c,d,M12,6,0x655b59c3)
b=II(d,a,b,c,M3,10,0x8f0ccc92)
c=II(c,d,a,b,M10,15,0xffeff47d)
d=II(b,c,d,a,M1,21,0x85845dd1)
a=II(a,b,c,d,M8,6,0x6fa87e4f)
b=II(d,a,b,c,M15,10,0xfe2ce6e0)
c=II(c,d,a,b,M6,15,0xa3014314)
d=II(b,c,d,a,M13,21,0x4e0811a1)
a=II(a,b,c,d,M4,6,0xf7537e82)
b=II(d,a,b,c,M11,10,0xbd3af235)
c=II(c,d,a,b,M2,15,0x2ad7d2bb)
d=II(b,c,d,a,M9,21,0xeb86d391)
```

5) After each cycle, add a, b, c, d to A, B, C, and D respectively, and then enter the next cycle.

### 3.MD5 purpose

#### 3.1. Consistency verification

A typical application of MD5 is to generate a message digest for a piece of text information to prevent it from being tampered with. We often see its MD5 value in the software information on some software download sites. Its function is that after downloading the software, we can use special software (such as Windows MD5 Check, etc.) to do an MD5 on the downloaded file. Verification to ensure that the file we get is the same file as provided by the site.

#### 3.2.Digital Certificate

If there is a third-party certification agency, using MD5 can also prevent "repudiation" of the file author. This is the so-called digital signature application.

#### 3.3.Security access authentication

In Unix systems, user passwords are stored in the file system after hashing using MD5 (or other similar algorithms). When the user logs in, the system performs an MD5 hash operation on the password entered by the user, and then compares it with the MD5 value stored in the file system to determine whether the entered password is correct. Through such steps, the system can determine the legitimacy of the user's login to the system without knowing the clear code of the user's password.


## 3. SHA algorithm

Secure Hash Algorithm (English: Secure Hash Algorithm, abbreviated as SHA) is a family of cryptographic hash functions that can calculate a fixed-length string (also called message digest) corresponding to a digital message. And if the input messages are different, the probability that they correspond to different strings is very high. The SHA family algorithms are SHA-0; SHA-1; SHA-224, SHA-256, SHA-384, SHA-512 and SHA3. SHA-224, SHA-256, SHA-384, SHA-512 are sometimes called SHA-2. SHA3 is the third generation secure hash algorithm (Secure Hash Algorithm 3), formerly known as the Keccak algorithm, in hardware implementation , this algorithm is significantly faster than other algorithms. Currently, SHA-0 and SHA-1 have been cracked.

### 1. Sha-0 and Sha-1

The originally specified algorithm was released in 1993 and was called the Secure Hash Standard, FIPS PUB 180. This version is now often called SHA-0. It was withdrawn by the NSA soon after its release and replaced by a revised version, FIPS PUB 180-1 (commonly known as SHA-1), released in 1995. The SHA-1 and SHA-0 algorithms only differ by one bit of cyclic displacement in the message conversion part of the compression function. According to the NSA, it fixes a weakness in the original algorithm that would make hashing less secure. However, the NSA did not provide any further explanation or prove that the vulnerability had been corrected. Then the weaknesses of SHA-0 and SHA-1 were broken one after another. SHA-1 seemed to be more resistant than SHA-0, which somewhat confirmed the NSA's original statement of modifying the algorithm to improve security.

SHA-0 and SHA-1 can convert a message of up to 264 bits into a string of 160-bit message digests; their design principles are similar to the cryptographic hash algorithms MD4 and MD5 designed by MIT professor Ronald L. Rivest.

#### 1.1.SHA-0 crack

At CRYPTO 98, two French researchers proposed an attack method on SHA-0: within a computational complexity of 261, a collision (that is, two different messages correspond to the same message digest) can be detected; This number is less than the 2^80 required for the birthday attack. In other words, there is an algorithm that makes it less secure than an ideal hash function should have to resist the attack.

In 2004, Biham and Chen also discovered an approximate collision of SHA-0, that is, two messages can hash almost the same value; 142 of the 162 bits are the same. They also discovered a complete collision of SHA-0 (as opposed to an approximate collision), reducing the complexity that originally required the 80th power to the 62nd power.

On August 12, 2004, Joux, Carribault, Lemuet, and Jalby announced a method to find a complete collision of the SHA-0 algorithm, which was the result of the attack accomplished by Chabaud and Joux. Finding a complete collision requires only 251 computational complexity. They used a supercomputer with 256 Itanium2 processors, which consumed approximately 80,000 CPU hours.

On August 17, 2004, at the CRYPTO 2004 Rump conference, Wang Xiaoyun, Feng Dengguo, Lai Xuejia, and Yu Hongbo announced the preliminary results of attacking MD5, SHA-0 and other hash functions. The computational complexity of their attack on SHA-0 is 2^40, which means their attack is better than what Joux and others have done. See MD5 security. In February 2005, Wang Xiaoyun, Yin Yiqun, and Yu Hongbo once again published an algorithm for decrypting SHA-0, which can find collisions within the computational complexity of 2 to the 39th power.#### 1.2.SHA-1 crack

In light of SHA-0's crypto-breaking success, experts suggest that those planning to implement cryptographic systems using SHA-1 should also reconsider. After the results of the 2004 CRYPTO conference were announced, NIST announced that they would gradually reduce the use of SHA-1 and replace it with SHA-2.

In 2005, Rijmen and Oswald published an attack on a weaker version of SHA-1 (53 encryption cycles instead of 80): finding collisions within a computational complexity of 2^80.

In February 2005, Wang Xiaoyun, Yin Yiqun and Yu Hongbo published an attack on the full version of SHA-1, which requires less than 2 to the 69th power of computational complexity to find a set of collisions. (Using the birthday attack method to find the collision requires a computational complexity of 2 to the power of 80.)

The authors of the paper write: "Our encryption analysis is based on differential attacks against SHA-0, approximate collisions, multi-block collision techniques, and message modification techniques to find collisions in the MD5 algorithm. None of these With powerful analysis tools, SHA-1 cannot be cracked. "In addition, the author also demonstrated a decryption of 58 encryption cycles of SHA-1, and found a set of collisions within 2 33rd power unit operations. A paper describing the complete attack method was published at the CRYPTO conference in August 2005.

Yin Yiqun stated in an interview: "Roughly speaking, we have found two weaknesses: one is that the pre-processing is not complex enough; the other is that some mathematical operations in the first 20 loops will cause unexpected security issues. ”

At the end of the CRYPTO conference on August 17, 2005, Wang Xiaoyun, Yao Qizhi, and Yao Chufeng once again published a more efficient SHA-1 attack method, which can find collisions within the computational complexity of 2 to the power of 63.

At the 2006 CRYPTO conference, Christian Rechberger and Christophe De Cannière announced that they could find a collision of SHA-1 while allowing the attacker to determine part of the original message.

In the academic theory of cryptography, any attack method whose computational complexity is less than the computational complexity required by the brute force search method can be regarded as a method for breaking the password of the cryptosystem; but this does not mean that This decryption method can already enter the stage of practical application.

As far as application considerations are concerned, the emergence of a new encryption method suggests that a more efficient and practical improved version may appear in the future. Although these practical versions of encryption methods have not yet been invented, it is necessary to develop stronger hashing algorithms to replace the old algorithms. In addition to the "collision" attack method, there is also a pre-image attack, which is to infer the original message from the hashed string. The seriousness of the pre-image attack is even greater than the collision attack, but it is It's also more difficult. In many scenarios where password hashing is applied (such as the storage of user passwords, digital signatures of files, etc.), the impact of collision attacks is not very great. For example, an attacker may not just want to forge an identical document, but may want to modify the original document and attach a legitimate signature to fool the verifier who holds the private key. On the other hand, if the unencrypted user password can be deduced from the ciphertext, the attacker can use the obtained password to log into other users' accounts, which is not allowed in a cryptographic system. However, if there is a reverse translation attack, as long as the hashed string of the specified user's password can be obtained (usually stored in a shadow file, and the original password information may not be revealed), it is possible to obtain the user's password.

#### 1.3.SHA-1 algorithm

The steps of the algorithm are roughly the same as the MD5 algorithm, but the operation is more complicated.

#### 3.1. Expanded data

Expand the data to a multiple of 512 bits (64 bytes), and these n segments of 512bits (64 bytes) data will be processed as original information.

### 3.2. The processing of this step is the same as the MD5 algorithm.

#### 3.3. Loop operation of each piece of 512bits (64 bytes) data (MainLoop)

#### 3.4. Difference from MD5 algorithm: Expand 512bits data (16*4 bytes) to 80*4 bytes and enter the main loop, and perform 80 cycles (4 groups * 20 times), the same as the MD5 algorithm. Divide operations into 4 groups:

F(X,Y,Z)=(X & Y) | ((~X) & Z)

G(X,Y,Z)=X ⊕ Y ⊕ Z

H(X,Y,Z)=(X & Y) | (X & Z) | (Y & Z)

I(X,Y,Z)=X ⊕ Y ⊕ Z

Among them, & is the AND operation, | is the OR operation, ~ is the negation operation, and ⊕ is the XOR operation.

That is to say, the function F is used in the first 20 cycles, the G function is used in the 21 to 40 cycles, the H function is used in the 41 to 60 cycles, and the I function is used in the last 20 cycles.

A, B, C, D, and E are the five integers left after the 512bits processing in the previous section (these five numbers are fixed constants during the first operation).

These 5 integers need to be temporarily stored before operating on the 512bits data (will be used later).

A'=A;

B'=B;

C'=C;

D'=D;

E'=E;

Start entering the operation of 512bits data. F represents the four groups of operation functions mentioned above, and the three numbers B, C, and D are the parameters of the four groups of operation functions respectively. Represents a 32 bits (4 bytes) input data (32bits of the 512bits data), and represents a 32bits constant (this is also fixed).

Summarize the operation into a formula:

temp = shift(A, 5) + F() + E + + ;

E = D;

D = C;

C = shift(B, 30);

B = A;

A = temp;

The latest 5 numbers A, B, C, D, and E obtained after each set of operations are used as the A, B, C, D, and E of the next set of operations until the 4 sets of operations (80 cycles) are completely completed. After a period of 80 cycles of 512 bits ends, new A, B, C, D, and E need to be prepared for the next period of 80 cycles of 512 bits. Compare the A, B, C, D, and E finally obtained after 80 loops in the previous section (that is, the last 5 numbers obtained in the above step) with the initial values A', B', C', and the ones saved before the loop. D' and E' correspond to addition.

A=A' + A;

B=B' + B;

C=C' + C;

D=D' + D;

E=E' + E;

The superposition operation ends, marking the completion of processing of the 512bits data in this segment.

#### 3.5. After the last 512bits operation, the final A, B, C, D, E are obtained, which is the final 160bits number. Because we need to get the last 160bits (40-digit hexadecimal) string, we need to convert each Convert a 4-byte number into an 8-digit hexadecimal string.

C++ code implementation:
```
#include<iostream>
#include<string>
using namespace std;
#define shift(x, n) (((x) << (n)) | ((x) >> (32-(n))))//When shifting right, the high bits must be filled with zeros instead of Supplementary sign bit
#define F(x, y, z) (((x) & (y)) | ((~x) & (z)))
#define G(x, y, z) ((x) ^ (y) ^ (z))
#define H(x, y, z) (((x) & (y)) | ((x) & (z)) | ((y) & (z)))
#define I(x, y, z) G(x, y, z)

#define A 0x67452301
#define B 0xefcdab89
#define C 0x98badcfe
#define D 0x10325476
#define E 0xC3D2E1F0

//The length of strBaye
unsigned int strlength;
//Temporary variables of A,B,C,D
unsigned int atemp;
unsigned int btemp;
unsigned int ctemp;
unsigned int dtemp;
unsigned int etemp;

const unsigned int k[]={0x5A827999,0x6ED9EBA1,0x8F1BBCDC,0xCA62C1D6};

const char str16[]="0123456789abcdef";
void mainLoop(unsigned int M[])
{
     unsigned int f,g;
     unsigned int a=atemp;
     unsigned int b=btemp;
     unsigned int c=ctemp;
     unsigned int d=dtemp;
   unsigned int e=etemp;
     for (unsigned int i = 0; i < 80; i++)
     {
         if(i<20){
             f=F(b,c,d);
         }else if (i<40){
             f=G(b,c,d);
         }else if(i<60){
             f=H(b,c,d);
         }else{
             f=I(b,c,d);
         }
         g=k[i/20];

         unsigned int tmp=shift(a, 5)+f+e+g+M[i];
         e=d;
         d=c;
         c=shift(b, 50);
         b=a;
         a=tmp;
     }
     atemp=a+atemp;
     btemp=b+btemp;
     ctemp=c+ctemp;
     dtemp=d+dtemp;
     etemp=e+etemp;
}
/*
*fill function
*After processing, it should satisfy bits≡448 (mod512), and the bytes are bytes≡56 (mode64)
*The filling method is to add a 1 first and fill the other bits with zeros
*Finally add the original length of 64 bits
*/
unsigned int* add(string str)
{
     unsigned int num=((str.length()+8)/64)+1;//512 bits, 64 bytes as a group
     unsigned int *strByte=new unsigned int[num*16]; //64/4=16, so there are 16 integers
     strlength=num*16;
     for (unsigned int i = 0; i < num*16; i++)
         strByte[i]=0;
     for (unsigned int i=0; i <str.length(); i++)
     {
         strByte[i>>2]|=(str[i])<<((i%4)*8);//An integer stores four bytes, i>>2 represents i/4 and an unsigned int corresponds to 4 bytes, save 4 character information
     }
     strByte[str.length()>>2]|=0x80<<(((str.length()%4))*8);//Add 1 at the end. An unsigned int stores 4 character information, so use 128 left shift
     /*
     *Add the original length. The length refers to the length of the bit, so it needs to be multiplied by 8, and then it is in little endian order, so it is placed in the second to last one. The length here only uses 32 bits.
     */
     strByte[num*16-2]=str.length()*8;
     return strByte;
}
string changeHex(int a)
{
     int b;
     string str1;
     string str="";
     for(int i=0;i<4;i++)
     {
         str1="";
         b=((a>>i*8)%(1<<8))&0xff; //Process each byte in reverse order
         for (int j = 0; j < 2; j++)
         {
             str1.insert(0,1,str16[b%16]);
             b=b/16;
         }
         str+=str1;
     }
     return str;
}
string getSHA1(string source)
{
     atemp=A; //Initialization
     btemp=B;
     ctemp=C;
     dtemp=D;
   etemp=E;
     unsigned int *strByte=add(source);
     for(unsigned int i=0;i<strlength/16;i++) //512bits data segmentation
     {
         unsigned int num[80];
         unsigned int j;
         for(j=0;j<16;j++)
             num[j]=strByte[i*16+j]; //Get 512bits data

         for(j=16;j<80;j++)
             num[j]=shift((num[j-3]^num[j-8]^num[j-14]^num[j-16]), 1); //Expand to 80
         mainLoop(num); //Enter the main loop
     }
     return changeHex(atemp).append(changeHex(btemp)).append(changeHex(ctemp))
                    .append(changeHex(dtemp)).append(changeHex(etemp));
}
unsigned int main()
{
     string ss;
//cin>>ss;
     string s=getSHA1("abc");
     cout<<s;
     return 0;
}
```


### 2. SHA-2

SHA-256, SHA-384 and SHA-512 all three functions map messages to longer message digests. They are named with their digest length (in bits) appended to the original name. They were published in a 2001 draft of FIPS PUB 180-2 and immediately passed review and comment. FIPS PUB 180-2, which includes SHA-1, was released as an official standard in 2002. In February 2004, a change notice to FIPS PUB 180-2 was released, adding an additional variant "SHA-224", which is defined to comply with the key length required for dual-key 3DES. SHA-256 and SHA -512 is a very new hash function. The former defines a word as 32 bits, and the latter defines a word as 64 bits. They use different offsets or different constants. However, in fact, they use different offsets. The structure of the two is the same, and they only differ in the number of loop executions. SHA-224 and SHA-384 are truncated versions of the two aforementioned hash functions, using different initial values for calculations. It has not undergone detailed testing by the public cryptography community like SHA-1, so its cryptographic security is not widely trusted. Gilbert and Handschuh did some research on these new variants in 2003, claiming that they were not. No weaknesses have been found. We can probably divide SHA-2 into two categories. The two categories use different offsets, different exposures, different number of cycles, and different data lengths, but the operation structure of the two types of SHA is the same. -256 and SHA-224: SHA-224 is a truncated version of SHA-256. The operation data is 32 bits (4 bytes), and the number of core cycles is 64. SHA-512 and SHA-384: SHA. -384 is a truncated version of SHA-512. The calculated data are all 64 bits (8 bytes), and the number of core cycles is 80.

#### 2.1 SHA-256 algorithm

##### 2.1.1.Expanded data

Similar to the MD5 algorithm and SHA-1 algorithm, the first step is to fill the data into an integer multiple of 512 bits, which is an integer multiple of 64 bytes. These n pieces of 512bits (64 bytes) data will be processed as original information.

##### 2.1.2. Loop operation of each piece of 512bits (64 bytes) data (MainLoop)

Expand 512bits data (16*4 bytes) to 64*4 bytes. For the SHA-256 algorithm, it is 64 cycles, which will expand 16 * 4 bytes (32 bits) to 64 * 4 bytes (32 bits). . In comparison, the SHA-512 algorithm is 80 cycles, so 16 * 8 bytes (64 bits) will be expanded to 80 * 8 bytes (64 bits).

Here is the pseudocode for the SHA-256 extension:

```
Extend the sixteen 32-bit words into sixty-four 32-bit words:
for i from 16 to 63
     s0 := (w[i-15] rightrotate 7) xor (w[i-15] rightrotate 18) xor(w[i-15] rightshift 3)
     s1 := (w[i-2] rightrotate 17) xor (w[i-2] rightrotate 19) xor(w[i-2] rightshift 10)
     w[i] := w[i-16] + s0 + w[i-7] + s1
 
```

Expanding from the 17th one, expressed in C code as:

Enter the main loop and perform 64 loops. The 64 loops here are somewhat different from the MD5 algorithm and the SHA-1 algorithm. They will not be divided into several groups, but the same operation 64 times.

But 4 functions are still needed:

```
Sigma0(x)=shift(x, 30) ⊕ shift(x, 19) ⊕ shift(x, 10);
Sigma1(x)=shift(x, 26) ⊕ shift(x, 21) ⊕ shift(x, 7);
Maj(x,y,z)=(x & y) ⊕ (x & z) ⊕ (y & z);
Ch(x,y,z)=(x & y) ⊕ (~x & z);
```

Among them, & is the AND operation, | is the OR operation, ~ is the negation operation, and ⊕ is the XOR operation.

The specific operation process is shown in the figure below:

![image](https://user-images.githubusercontent.com/19474106/119256608-14c80800-bbf4-11eb-92fe-84ca5db9156b.png)


A, B, C, D, E, F, G, and H are the 8 integers left after the 512bits processing in the previous section (these 8 numbers are fixed constants during the first operation). These 8 integers need to be temporarily stored before operating on the 512bits data (will be used later). Represents a 32 bits (4 bytes) input data (32bits of the 512bits data), and represents a 32bits constant (this is also fixed).

Summarize the operation in the above figure into a formula:

```
s0 = Sigma0(A);

maj = Ma(A, B, C);
s1 = Sigma1(E);
ch = Ch(E, F, G);
t1 = H + s1 + ch + k[i] + M[i];
H = G;
G = F;
F = E;
E = D + t1;
D = C;
C = B;
B = A;

A = t1 + s0 + maj;
```


The latest 8 numbers A, B, C, D, E, F, G, H obtained after each set of operations are used as the initial values of the next set of operations until the 64th cycle is completed. After the 64 cycles of a section of 512bits are completed, new A, B, C, D, E, F, G, H need to be prepared for the next section of 512bits. Add the A, B, C, D, E, F, G, H finally obtained after the previous 64 cycles (that is, the last 8 numbers obtained in the previous step) to the initial values saved before the cycle. .

##### 2.1.3. After the last 512bits operation, the final A, B, C, D, E are obtained, which is the final 160bits number. Because we need to get the last 256bits (64-bit hexadecimal) string, so Convert each 4-byte number into an 8-digit hexadecimal string.

##### 2.1.4. SHA-224 and SHA-256

SHA-224 is basically the same as SHA-256, except that the 8 initial values are different. SHA-224 truncates the H value when outputting to obtain the final 56-bit hexadecimal string. SHA-512 has the same structure as SHA-256, but all numbers in SHA-512 are 64 bits. SHA-512 runs 80 cycles. The initial value and constant value of SHA-512 are both 64 bits. SHA-512 is biased The displacement amount is also different from the displacement amount in the cycle


##### 2.1.5 initial values are different

When SHA-384 is output, the F and H values are truncated to obtain the final 96-bit hexadecimal string.


##### 2.1.6. SHA-256 algorithm implemented in C code

````

#include<iostream>
#include<string>
using namespace std;
#define shift(x, n) (((x) << (n)) | ((x) >> (32-(n))))//When shifting right, the high bits must be filled with zeros instead of Supplementary sign bit
#define S0(x) ((shift(x, 25)) ^ (shift(x, 14)) ^ ((x) >> 3))
#define S1(x) ((shift(x, 17)) ^ (shift(x, 19)) ^ ((x) >> 10))

#define Sigma0(x) ((shift(x, 30)) ^ (shift(x, 19)) ^ (shift(x, 10)))
#define Sigma1(x) ((shift(x, 26)) ^ (shift(x, 21)) ^ (shift(x, 7)))
#define Ma(x,y,z) (((x) & (y)) ^ ((x) & (z)) ^ ((y) & (z)))
#define Ch(x,y,z) (((x) & (y)) ^ ((~x) & (z)))

#define A 0x6a09e667
#define B 0xbb67ae85
#define C 0x3c6ef372
#define D 0xa54ff53a
#define E 0x510e527f
#define F 0x9b05688c
#define G 0x1f83d9ab
#define H 0x5be0cd19

//The length of strBaye
unsigned int strlength;
//Temporary variables of A,B,C,D
unsigned int atemp;
unsigned int btemp;
unsigned int ctemp;
unsigned int dtemp;
unsigned int etemp;
unsigned int ftemp;
unsigned int gtemp;
unsigned int htemp;

static const uint32_t k[64] = {
     0x428a2f98, 0x71374491, 0xb5c0fbcf, 0xe9b5dba5, 0x3956c25b,
     0x59f111f1, 0x923f82a4, 0xab1c5ed5, 0xd807aa98, 0x12835b01,
     0x243185be, 0x550c7dc3, 0x72be5d74, 0x80deb1fe, 0x9bdc06a7,
     0xc19bf174, 0xe49b69c1, 0xefbe4786, 0x0fc19dc6, 0x240ca1cc,
     0x2de92c6f, 0x4a7484aa, 0x5cb0a9dc, 0x76f988da, 0x983e5152,
     0xa831c66d, 0xb00327c8, 0xbf597fc7, 0xc6e00bf3, 0xd5a79147,
     0x06ca6351, 0x14292967, 0x27b70a85, 0x2e1b2138, 0x4d2c6dfc,
     0x53380d13, 0x650a7354, 0x766a0abb, 0x81c2c92e, 0x92722c85,
     0xa2bfe8a1, 0xa81a664b, 0xc24b8b70, 0xc76c51a3, 0xd192e819,
     0xd6990624, 0xf40e3585, 0x106aa070, 0x19a4c116, 0x1e376c08,
    0x2748774c, 0x34b0bcb5, 0x391c0cb3, 0x4ed8aa4a, 0x5b9cca4f,
    0x682e6ff3, 0x748f82ee, 0x78a5636f, 0x84c87814, 0x8cc70208,
    0x90befffa, 0xa4506ceb, 0xbef9a3f7, 0xc67178f2};

const char str16[]="0123456789abcdef";
void mainLoop(unsigned int M[])
{
    unsigned int s0, maj, s1, ch, t;

    unsigned int a = atemp;
    unsigned int b = btemp;
    unsigned int c = ctemp;
    unsigned int d = dtemp;
    unsigned int e = etemp;
    unsigned int f = ftemp;
    unsigned int g = gtemp;
    unsigned int h = htemp;

    for (unsigned int i = 0; i < 64; i++)
    {
        s0 = Sigma0(a);
        maj = Ma(a, b, c);
        s1 = Sigma1(e);
        ch = Ch(e, f, g);
        t1 = h + s1 + ch + k[i] + M[i];

        h = g;
        g = f;
        f = e;
        e = d + t1;
        d = c;
        c = b;
        b = a;
        a = t1 + s0 + maj;
    }
    atemp=a+atemp;
    btemp=b+btemp;
    ctemp=c+ctemp;
    dtemp=d+dtemp;
    etemp=e+etemp;
    ftemp=f+ftemp;
    gtemp=g+gtemp;
    htemp=h+htemp;
}/*
*fill function
*After processing, it should satisfy bits≡448 (mod512), and the bytes are bytes≡56 (mode64)
*The filling method is to add a 1 first and fill the other bits with zeros
*Finally add the original length of 64 bits
*/
unsigned int* add(string str)
{
     unsigned int num=((str.length()+8)/64)+1;//512 bits, 64 bytes as a group
     unsigned int *strByte=new unsigned int[num*16]; //64/4=16, so there are 16 integers
     strlength=num*16;
     for (unsigned int i = 0; i < num*16; i++)
         strByte[i]=0;
     for (unsigned int i=0; i <str.length(); i++)
     {
         strByte[i>>2]|=(str[i])<<((i%4)*8);//An integer stores four bytes, i>>2 represents i/4 and an unsigned int corresponds to 4 bytes, save 4 character information
     }
    strByte[str.length()>>2]|=0x80<<(((str.length()%4))*8);//Add 1 at the end. An unsigned int stores 4 character information, so use 128 left shift
     /*
     *Add the original length. The length refers to the length of the bit, so it needs to be multiplied by 8, and then it is in little endian order, so it is placed in the second to last one. The length here only uses 32 bits.
     */
     strByte[num*16-2]=str.length()*8;
     return strByte;
}
string changeHex(int a)
{
    int b;
    string str1;
    string str="";
    for(int i=0;i<4;i++)
    {
        str1="";
        b=((a>>i*8)%(1<<8))&0xff;   //Process each byte in reverse order
        for (int j = 0; j < 2; j++)
        {
            str1.insert(0,1,str16[b%16]);
            b=b/16;
        }
        str+=str1;
    }
    return str;
}
string getSHA1(string source)
{
    atemp=A;   //initialization
    btemp=B;
    ctemp=C;
    dtemp=D;
    etemp=E;
    ftemp=F;
    gtemp=G;
    htemp=H;
    unsigned int *strByte=add(source);
    for(unsigned int i=0;i<strlength/16;i++) //512bits Data segmentation
    {
        unsigned int num[80];
        unsigned int j;
        for(j=0;j<16;j++)
            num[j]=strByte[i*16+j]; //Get 512bits data

      for(j=16;j<64;j++)
             num[j]=num[j-16] + S0(num[i-15]) + num[i-7] + S1(num[i-2]); //Extended to 64
         mainLoop(num); //Enter the main loop
    }
    return changeHex(atemp).append(changeHex(btemp)).append(changeHex(ctemp))
              .append(changeHex(dtemp)).append(changeHex(etemp)).append(changeHex(ftemp))
              .append(changeHex(gtemp)).append(changeHex(htemp));
}
unsigned int main()
{
    string ss;
//    cin>>ss;
    string s=getSHA1("abc");
    cout<<s;
    return 0;
}

````


### 3. Sha-3

The SHA-3 algorithm is the third generation standard hash function, implemented based on the Keccak algorithm. Different from previous hash algorithms, the SHA-3 algorithm is a permutation-based encryption function.

#### 3.1. Sha-3 algorithm process

The SHA-3 hash function with an output length of X bits is expressed as: SHA3-X(M)

The following takes a function with an output length of 256 bits as an example. In the standard, the SHA-3 function with an output length of 256 bits is expressed as SHA3-256(M), where M is the data that needs to be hashed. The process of data hashing is mainly based on sponge construction, so we will introduce the sponge structure first.

sponge structure

The sponge structure is capable of data transformation, converting arbitrarily long input into arbitrarily long output. The picture below is a schematic diagram of a sponge structure.

![image](https://user-images.githubusercontent.com/19474106/119256665-61abde80-bbf4-11eb-8af6-700be137048a.png)


As shown in the figure, the sponge structure consists of 3 important components:

A function f that performs equal-length mapping on data, that is, the length of the output string is the same as the length of the input string, denoted as b.

One parameter is called rate, denoted as r, which refers to the length of data in the string of length b to be absorbed in each round. The remaining part is called the capacity, denoted as c. Therefore, b = r + c.

A padding function, denoted pad(x,,m), returns a string of length m padded to a string that is an integer multiple of x. For example, pad(5,2)=010 means to fill a string of length 2 with an integer multiple of 5. You need to add a string of length 3. Any string of length 3 can be used. In this example, the return value is 010 , its length is 3.

Given the above composition, the data can be manipulated and the mapping results obtained. The formal definition is as follows:

SPONGE[f,pad,r]

Based on this sponge structure, a sponge function can be defined to convert the input into a string of specified length. Therefore, the function has two parameters: 1. Input string N, 2. Output length d. The function is defined as follows:

SPONGE[f,pad,r](N,d)

The following is a brief description of the execution process of the sponge function based on the figure:

1. First, pad the input N so that its length is an integer multiple of r. The result is P = N || pad(r, len(N)), "||" indicates string connection.

2. Record n =len(P)/r, divide P into n segments, record as P = P0||P2|| ...Pn-1, the length of each segment is rr.

3. Define S = 0^b to represent a string of 0s with length b. This S is also called a state, which will be introduced later.

4. Define i from 0 to n−1, and convert S sequentially, S =f(S⊕(Pi∣∣0^c)). The above process is called the absorbing process.

5. Define Z as an empty string.

6.Z = Z∣∣Truncr(S), where Truncr(S) refers to the string consisting of the first r characters of S.

7. If d≤len(Z) at this time, return Truncd(Z)

8. Let S=f(S) and return to step 6.



#### KECCAK sponge function

Defining a sponge structure requires specifying the three components of the sponge structure.

1. A function f that performs equal-length mapping on data.

2. One parameter is called the ratio r.

3. A padding function, denoted as pad(x,m).

The three components of the KECCAK sponge function used in SHA-3 are of the following form:

1. The mapping function KECCAK-p[b,nr](S) converts the string S of length b into a result of length b through nr rounds. It is also called the KECCAK-p permutation function. This function will be explained in detail later.

2. The ratio r is adjusted according to the output length.

3. The filling function is pad10∗1(x,m). In addition to returning a string of length m filled with a string that is an integer multiple of x, it also ensures that the returned string satisfies the expression 10∗1 form.



#### KECCAK-p replacement

KECCAK-p permutation rearranges the input string in multiple rounds to obtain output strings of the same length. Assume that the length of the input string S is b, and the permutation is performed in nr rounds of rearrangement, then the KECCAK-p permutation function is recorded as


![image](https://user-images.githubusercontent.com/19474106/119256679-75574500-bbf4-11eb-9db3-732ca3dbe4f9.png)


Among them, b∈{25,50,100,200,400,800,1600}


The substitution function can also be considered as performing state transition. As mentioned earlier, the input S of this function is also called the state. KECCAK-p substitution is to perform state transition on S. The following briefly introduces the concept of status.

state


An array of bits that is constantly updated is called a state. A state can be represented as a bit string or an array of states. The bit string refers to the binary string of the state, denoted as S, and the length is denoted as b; The state array represents the state as a 5×5×w three-dimensional array, where w = b/25, denoted as A. Both S and AA represent states and can be converted to each other.

Each bit in the state array can be represented by A[x, y, z], and the coordinate system of the state array is as follows:

![image](https://user-images.githubusercontent.com/19474106/119256687-7c7e5300-bbf4-11eb-9503-930b84c9532e.png)


Among them, the x and y directions have the center point as the origin. Below are the naming of the different sub-arrays in the status array.

![image](https://user-images.githubusercontent.com/19474106/119256690-856f2480-bbf4-11eb-870e-a2137dbfc2e3.png)


step mappings
There are a total of 5 mapping functions in the SHA-3 standard, which can arrange the state array A in different ways. They are briefly introduced below.

θ(A), rearrange columncolumn.

ρ(A), rearrange lanelane.

π(A), rearrange sliceslice.

χ(A), rearrange rowrow.

ι(A,ir), rearranges the A[0,0,z] part.

For nr rounds of transformation, use the function Rnd for each round:

![image](https://user-images.githubusercontent.com/19474106/119256694-8dc75f80-bbf4-11eb-8fc1-f943f80da618.png)

     note:(english version of above image)
     Rnd(A, i,r) = u(x(π(ρ(θ(A)))), i,r)
     where each round key i,r ∈ [12 + 2ℓ − n_r, 12 + 2ℓ − 1]



replacement process
The replacement process is summarized as follows:

![image](https://user-images.githubusercontent.com/19474106/119256699-94ee6d80-bbf4-11eb-8cd2-825c2518629d.png)

     note:(english version of above image)
     1.Convert “S” to “A.”
     2.For the case where i=r, take values from 12 + 2c − nr to 12 + 2c − 1, resulting in A = Rnd(A, i,r).
     3.Convert A back to S’, yielding O S’.


Definition SHA-3

The hash function in SHA-3 is implemented based on the Keccak sponge structure and sets some parameters as constants:

Set the KECCAK-p replacement input length to 1600 bits, which is also the length of the state.

Set KECCAK-p permutation for 24 rounds.

Parameter r = 1600 - c, and its value depends on the length of the hash result that needs to be output. Therefore, the sponge function used in SHA-3 is defined as:

![image](https://user-images.githubusercontent.com/19474106/119256708-9e77d580-bbf4-11eb-864f-9d4d53be89c6.png)


The parameter c depends on the output length. Based on the above definition, the SHA-3 hash function is defined as follows:

![image](https://user-images.githubusercontent.com/19474106/119256714-a46db680-bbf4-11eb-8b16-2e156ab84375.png)

Among them, c is set to 2 times the output length, and the input string needs to be added with a suffix of 01 as the input of the sponge function. The SHA-3 series of functions ultimately obtain hash results of a given length.


## 4. Blake and Blake2

We all know that the Hash Algorithm is an algorithm that maps data of any length to data of a fixed length, also called a message digest. In general, hashing algorithms have two characteristics. First, subtle changes in the original data (such as a bit flip) will lead to huge differences in the results; second, the operation process is irreversible, and theoretically it is impossible to restore the input data from the results. Therefore, hashing algorithms are mainly used for data integrity verification and encryption/signing.

The security of the hash algorithm lies in the difficulty of collision, that is, the difficulty of constructing input data with the same result given the result.

Common hashing algorithms include MD5, SHA-1, SHA-2, and SHA-3. Among them, MD5 can already complete the collision within 2^21 complexity (only 30 seconds on mainstream smartphones), and Google also completed it within 2^64 complexity (about 110 GPU-year calculations) earlier in 2017. The first SHA-1 collision occurred. At this point, MD5 and SHA-1 have been deprecated in the security community. Currently, in addition to SHA-2 and SHA-3, there is another hash algorithm series to choose from, that is BLAKE. The BLAKE2 series is faster than the common MD5, SHA-1, SHA-2, and SHA-3, and at the same time Provides security no lower than SHA-3. The BLAKE2 family is derived from the famous ChaCha algorithm and has two main versions BLAKE2b (BLAKE2) and BLAKE2s.

BLAKE2b is optimized for 64-bit CPUs (including ARM Neon) and can generate digests up to 64 bytes; BLAKE2s is designed for 8-32-bit CPUs and can generate digests up to 32 bytes.

Their derivatives, BLAKE2bp and BLAKE2sp, can perform multi-core parallel computing, further improving computing speed while maintaining the same security. Additionally, the BLAKE2 family has a special variant, BLAKE2x, that can generate "digests" of up to 4GiB and can be used for KDF (Key Derivation) and DRBG (Fixed Random Number Sequences).

The BLAKE2 algorithm is based on the BLAKE algorithm and was proposed in 2012, which means that the Blake series of algorithms had been produced before Blake2. The BLAKE algorithm was proposed in 2008. It contains two versions, one based on a 32-bit word to produce a hash result of up to 256 bits, and one based on a 64-bit word to produce a hash result of up to 512 bits. BLAKE The core operation of the algorithm is to continuously combine the 8 hash intermediate results and the 16 input words to produce the 8 intermediate results of the next round of combinations. According to the final truncated hash length, BLAKE-256 and BLAKE-224 use 32-bit words to produce 256-bit and 224-bit hash results (also called message digests) respectively, while BLAKE-512 and BLAKE-384 use 64-bit words and Produces 512-bit and 384-bit hash results.

Blake source code can be referred to: https://github.com/veorq/BLAKE

The source code of blake2 can be referred to: https://github.com/BLAKE2/BLAKE2