# 第四章：单向散列函数

## 一. 简介
单向散列函数，又称单向Hash函数、杂凑函数，就是把任意长度的输入消息串变化成固定长的输出串且由输出串难以得到输入串的一种函数。这个输出串称为该消息的散列值。一般用于产生消息摘要，密钥加密等.


## 二. MD5 算法

### 1. MD5 简介

MD5：是RSA数据安全公司开发的一种单向散列算法，MD5被广泛使用，可以用来把不同长度的数据块进行暗码运算成一个128位的数值。不同的值产生的结果不一样。

### 2.MD5 算法流程

对MD5算法简要的叙述可以为：MD5 以 512位分组来处理输入的信息，且每一分组又被划分为16个32位子分组，经过了一系列的处理后，算法的输出由四个32位分组组成，将这四个32位分组级联后将生成一个128位散列值。

第一步、填充：如果输入信息的长度(bit)对512求余的结果不等于448，就需要填充使得对512求余的结果等于448。填充的方法是填充一个1和n个0。填充完后，信息的长度就为N*512+448(bit)

第二步、记录信息长度：用64位来存储填充前信息长度。这64位加在第一步结果的后面，这样信息长度就变为N*512+448+64=(N+1)*512位。

第三步、装入标准的幻数（四个整数）：标准的幻数（物理顺序）是（A=(01234567)16，B=(89ABCDEF)16，C=(FEDCBA98)16，D=(76543210)16）。如果在程序中定义应该是:（A=0X67452301L，B=0XEFCDAB89L，C=0X98BADCFEL，D=0X10325476L）。


第四步、四轮循环运算：循环的次数是分组的个数（N+1）

1）将每一512字节细分成16个小组，每个小组64位（8个字节）

2）先认识四个线性函数(&是与,|是或,~是非,^是异或)

```
F(X,Y,Z)=(X&Y)|((~X)&Z)
G(X,Y,Z)=(X&Z)|(Y&(~Z))
H(X,Y,Z)=X^Y^Z
I(X,Y,Z)=Y^(X|(~Z))
3）设Mj表示消息的第j个子分组（从0到15）

FF(a,b,c,d,Mj,s,ti)表示a=b+((a+F(b,c,d)+Mj+ti)<<<s)
GG(a,b,c,d,Mj,s,ti)表示a=b+((a+G(b,c,d)+Mj+ti)<<<s)
HH(a,b,c,d,Mj,s,ti)表示a=b+((a+H(b,c,d)+Mj+ti)<<<s)
II(a,b,c,d,Mj,s,ti)表示a=b+((a+I(b,c,d)+Mj+ti)<<<s)
```

4）四轮运算
 第一轮
 
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

第二轮

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

第三轮

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

第四轮

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

5）每轮循环后，将A，B，C，D分别加上a，b，c，d，然后进入下一循环。

### 3.MD5 用途

#### 3.1.一致性验证

MD5的典型应用是对一段文本信息产生信息摘要，以防止被篡改。常常在某些软件下载站点的某软件信息中看到其MD5值，它的作用就在于我们可以在下载该软件后，对下载回来的文件用专门的软件（如Windows MD5 Check等）做一次MD5校验，以确保我们获得的文件与该站点提供的文件为同一文件。

#### 3.2.数字证书

如果有一个第三方的认证机构，用MD5还可以防止文件作者的“抵赖”，这就是所谓的数字签名应用。

#### 3.3.安全访问认证

在Unix系统中用户的密码是以MD5（或其它类似的算法）经Hash运算后存储在文件系统中。当用户登录的时候，系统把用户输入的密码进行MD5 Hash运算，然后再去和保存在文件系统中的MD5值进行比较，进而确定输入的密码是否正确。通过这样的步骤，系统在并不知道用户密码的明码的情况下就可以确定用户登录系统的合法性。


## 三.SHA 算法

安全散列算法（英语：Secure Hash Algorithm，缩写为SHA）是一个密码散列函数家族，能计算出一个数字消息所对应到的，长度固定的字符串（又称消息摘要）的算法。且若输入的消息不同，它们对应到不同字符串的机率很高。SHA家族算法分别是SHA-0；SHA-1；SHA-224、SHA-256、SHA-384，SHA-512和SHA3。SHA-224、SHA-256、SHA-384，SHA-512有时并称为SHA-2， SHA3是第三代安全散列算法(Secure Hash Algorithm 3)，之前名为Keccak 算法，在硬件实做上面，这个算法比起其他算法明显的快上很多，目前 SHA-0，SHA-1 已被破解。

### 1. Sha-0 和 Sha-1

最初载明的算法于1993年发布，称做安全散列标准（Secure Hash Standard），FIPS PUB 180。这个版本现在常被称为SHA-0。它在发布之后很快就被NSA撤回，并且由1995年发布的修订版本FIPS PUB 180-1（通常称为SHA-1）取代。SHA-1和SHA-0的算法只在压缩函数的消息转换部分差了一个比特的循环位移。根据NSA的说法，它修正了一个在原始算法中会降低散列安全性的弱点。然而NSA并没有提供任何进一步的解释或证明该弱点已被修正。而后SHA-0和SHA-1的弱点相继被攻破，SHA-1似乎是显得比SHA-0有抵抗性，这多少证实了NSA当初修正算法以增进安全性的声明。

SHA-0 和 SHA-1可将一个最大264比特的消息，转换成一串160位的消息摘要；其设计原理相似于MIT教授Ronald L. Rivest所设计的密码学散列算法MD4和MD5。

#### 1.1.SHA-0破解

在CRYPTO 98上，两位法国研究者提出一种对SHA-0的攻击方式：在261的计算复杂度之内，就可以发现一次碰撞（即两个不同的讯息对应到相同的讯息摘要）；这个数字小于生日攻击法所需的2的80次方，也就是说，存在一种算法，使其安全性不到一个理想的杂凑函数抵抗攻击所应具备的计算复杂度。

2004年时，Biham和 Chen也发现了SHA-0的近似碰撞，也就是两个讯息可以杂凑出几乎相同的数值；其中162位元中有142位元相同。他们也发现了SHA-0的完整碰撞（相对于近似碰撞），将本来需要80次方的复杂度降低到62次方。

2004年8月12日，Joux, Carribault, Lemuet和Jalby宣布找到SHA-0算法的完整碰撞的方法，这是归纳Chabaud和Joux的攻击所完成的结果。发现一个完整碰撞只需要251的计算复杂度。他们使用的是一台有256颗Itanium2处理器的超级电脑，约耗80,000 CPU工时。

2004年8月17日，在CRYPTO 2004的Rump会议上，王小云，冯登国、来学嘉，和于红波宣布了攻击MD5、SHA-0 和其他杂凑函数的初步结果。他们攻击SHA-0的计算复杂度是2的40次方，这意味着他们的攻击成果比Joux还有其他人所做的更好。请参见MD5 安全性。2005年二月，王小云和殷益群、于红波再度发表了对SHA-0破密的算法，可在2的39次方的计算复杂度内就找到碰撞。

#### 1.2.SHA-1破解

鉴于SHA-0的破密成果，专家们建议那些计划利用SHA-1实作密码系统的人们也应重新考虑。在2004年CRYPTO会议结果公布之后，NIST即宣布他们将逐渐减少使用SHA-1，改以SHA-2取而代之。

2005年，Rijmen和Oswald发表了对SHA-1较弱版本（53次的加密循环而非80次）的攻击：在2的80次方的计算复杂度之内找到碰撞。

2005年二月，王小云、殷益群及于红波发表了对完整版SHA-1的攻击，只需少于2的69次方的计算复杂度，就能找到一组碰撞。（利用生日攻击法找到碰撞需要2的80次方的计算复杂度。）

这篇论文的作者们写道；“我们的破密分析是以对付SHA-0的差分攻击、近似碰撞、多区块碰撞技术、以及从MD5算法中寻找碰撞的讯息更改技术为基础。没有这些强力的分析工具，SHA-1就无法破解。”此外，作者还展示了一次对58次加密循环SHA-1的破密，在2的33次方个单位操作内就找到一组碰撞。完整攻击方法的论文发表在2005年八月的CRYPTO会议中。

殷益群在一次面谈中如此陈述：“大致上来说，我们找到了两个弱点：其一是前置处理不够复杂；其二是前20个循环中的某些数学运算会造成不可预期的安全性问题。”

2005年8月17日的CRYPTO会议尾声中王小云、姚期智、姚储枫再度发表更有效率的SHA-1攻击法，能在2的63次方个计算复杂度内找到碰撞。

2006年的CRYPTO会议上，Christian Rechberger和Christophe De Cannière宣布他们能在容许攻击者决定部分原讯息的条件之下，找到SHA-1的一个碰撞。

在密码学的学术理论中，任何攻击方式，其计算复杂度若少于暴力搜寻法所需要的计算复杂度，就能被视为针对该密码系统的一种破密法；但这并不表示该破密法已经可以进入实际应用的阶段。

就应用层面的考量而言，一种新的破密法出现，暗示着将来可能会出现更有效率、足以实用的改良版本。虽然这些实用的破密法版本根本还没诞生，但确有必要发展更强的杂凑算法来取代旧的算法。在“碰撞”攻击法之外，另有一种反译攻击法（Pre-image attack），就是由杂凑出的字串反推原本的讯息；反译攻击的严重性更在碰撞攻击之上，但也更困难。在许多会应用到密码杂凑的情境（如用户密码的存放、文件的数位签章等）中，碰撞攻击的影响并不是很大。举例来说，一个攻击者可能不会只想要伪造一份一模一样的文件，而会想改造原来的文件，再附上合法的签章，来愚弄持有私密金钥的验证者。另一方面，如果可以从密文中反推未加密前的使用者密码，攻击者就能利用得到的密码登入其他使用者的帐户，而这种事在密码系统中是不能被允许的。但若存在反译攻击，只要能得到指定使用者密码杂凑过后的字串（通常存在影档中，而且可能不会透露原密码资讯），就有可能得到该使用者的密码。

#### 1.3.SHA-1算法

算法的步骤大概跟MD5算法 差不多，运算上更复杂一些。

#### 3.1、扩充数据

将数据扩充到512 bits(64 bytes)的倍数，这些n 段512bits(64字节)的数据会作为原始信息进行处理。

### 3.2.这一步的处理同MD5算法。

#### 3.3.循环运算每一段512bits(64 字节)的数据（MainLoop）

#### 3.4. 跟MD5算法的区别：将512bits数据（16*4字节）扩展为80*4字节进入主循环，进行80次(4组 * 20次)循环，同MD5算法，也是将运算分为4 组：

F(X,Y,Z)=(X & Y) | ((~X) & Z) 

G(X,Y,Z)=X ⊕ Y ⊕ Z

H(X,Y,Z)=(X & Y) | (X & Z) | (Y & Z)

I(X,Y,Z)=X ⊕ Y ⊕ Z

其中，& 是与运算， | 是或运算，~ 是取反运算，⊕ 是异或运算

也就是说函数F 是前20次循环使用的，G函数是21 至 40次循环使用，H 函数是41 至60次循环使用，I 函数是最后20次循环使用。

A、B、C、D 、E分别是上一段512bits 处理后留下来的5个整数(第一次运算的时候这5个数为固定的常数)。

在对该512bits 数据运算前需要先把这5个整数临时存起来（后面会使用到）。

A'=A;

B'=B;

C'=C;

D'=D;

E'=E;

开始进入512bits 数据的运算。F 代表上面提到的 4 组运算函数，B、C、D三个数分别是4组运算函数的参数。  表示一个32 bits(4个字节) 的输入数据(512bits 数据其中的32bits)，  表示一个32bits 的常数(这个也是固定的)。

将运算总结成公式：

temp = shift(A, 5) + F() + E +  + ;

E = D;

D = C;

C = shift(B, 30);

B = A;

A = temp;

将每一组运算后得到最新的5个数A、B、C、D、E作为下一组运算的A、B、C、D、E，一直到4组运算(80次循环) 彻底结束。一段512bits 的80 次循环结束之后，需要为下一段512bits 的80 次循环准备新的A、B、C、D、E。将上一段80 次循环后最终得到的A、B、C、D 、E(也就是上面一步得到的最后的5个数)与循环之前的保存下来的初始值A'、B'、C'、D'、E' 对应相加。

A=A' + A;

B=B' + B;

C=C' + C;

D=D' + D;

E=E' + E;

叠加运算结束，标志该段512bits数据处理完毕。

#### 3.5.最后一段512bits 运算后得到最终的A、B、C、D、E，即为最终的160bits数因为需要得到最后160bits(40 位16进制)的字符串，所以要将每个4字节的数转换成8位的16进制字符串。

C++ 代码实现：
```
#include<iostream>
#include<string>
using namespace std;
#define shift(x, n) (((x) << (n)) | ((x) >> (32-(n))))//右移的时候，高位一定要补零，而不是补充符号位
#define F(x, y, z) (((x) & (y)) | ((~x) & (z)))
#define G(x, y, z) ((x) ^ (y) ^ (z))
#define H(x, y, z) (((x) & (y)) | ((x) & (z)) | ((y) & (z)))
#define I(x, y, z) G(x, y, z)

#define A 0x67452301
#define B 0xefcdab89
#define C 0x98badcfe
#define D 0x10325476
#define E 0xC3D2E1F0

//strBaye的长度
unsigned int strlength;
//A,B,C,D的临时变量
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
*填充函数
*处理后应满足bits≡448(mod512),字节就是bytes≡56（mode64)
*填充方式为先加一个1,其它位补零
*最后加上64位的原来长度
*/
unsigned int* add(string str)
{
    unsigned int num=((str.length()+8)/64)+1;//以512位,64个字节为一组
    unsigned int *strByte=new unsigned int[num*16];    //64/4=16,所以有16个整数
    strlength=num*16;
    for (unsigned int i = 0; i < num*16; i++)
        strByte[i]=0;
    for (unsigned int i=0; i <str.length(); i++)
    {
        strByte[i>>2]|=(str[i])<<((i%4)*8);//一个整数存储四个字节，i>>2表示i/4 一个unsigned int对应4个字节，保存4个字符信息
    }
    strByte[str.length()>>2]|=0x80<<(((str.length()%4))*8);//尾部添加1 一个unsigned int保存4个字符信息,所以用128左移
    /*
    *添加原长度，长度指位的长度，所以要乘8，然后是小端序，所以放在倒数第二个,这里长度只用了32位
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
        b=((a>>i*8)%(1<<8))&0xff;   //逆序处理每个字节
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
    atemp=A;    //初始化
    btemp=B;
    ctemp=C;
    dtemp=D;
  etemp=E;
    unsigned int *strByte=add(source);
    for(unsigned int i=0;i<strlength/16;i++) //512bits 数据分段
    {
        unsigned int num[80];
        unsigned int j;
        for(j=0;j<16;j++)
            num[j]=strByte[i*16+j]; //得到512bits 数据

        for(j=16;j<80;j++)
            num[j]=shift((num[j-3]^num[j-8]^num[j-14]^num[j-16]), 1); //扩展到80个
        mainLoop(num); //进入主循环
    }
    return changeHex(atemp).append(changeHex(btemp)).append(changeHex(ctemp))
                   .append(changeHex(dtemp)).append(changeHex(etemp));
}
unsigned int main()
{
    string ss;
//    cin>>ss;
    string s=getSHA1("abc");
    cout<<s;
    return 0;
}
```


### 2. SHA-2

SHA-256，SHA-384和SHA-512 三个函数都将消息对应到更长的消息摘要。以它们的摘要长度（以位元计算）加在原名后面来命名。它们发布于2001年的FIPS PUB 180-2草稿中，随即通过审查和评论。包含SHA-1的FIPS PUB 180-2，于2002年以官方标准发布。2004年2月，发布了一次FIPS PUB 180-2的变更通知，加入了一个额外的变种SHA-224"，这是为了符合双金钥3DES所需的金钥长度而定义。SHA-256和SHA-512是很新的杂凑函数，前者以定义一个word为32位元，后者则定义一个word为64位元。它们分别使用了不同的偏移量，或用不同的常数，然而，实际上二者结构是相同的，只在循环执行的次数上有所差异。SHA-224以及SHA-384则是前述二种杂凑函数的截短版，利用不同的初始值做计算。这些新的杂凑函数并没有接受像SHA-1一样的公众密码社群做详细的检验，所以它们的密码安全性还不被大家广泛的信任。Gilbert和Handschuh在2003年曾对这些新变种作过一些研究，声称他们没有找到弱点。我们大概可以将SHA-2分为两类，两类使用不同的偏移量、不同的敞亮、不同的循环次数、不同的数据长度。但是两类的运算结构是相同的。SHA-256 和 SHA-224: 其中SHA-224是SHA-256 的截短版，运算的数据都是32位(4字节)，核心循环次数为64次。SHA-512 和 SHA-384:其中SHA-384是SHA-512 的截短版，运算的数据都是64位(8字节)，核心循环次数为80次。

#### 2.1 SHA-256 算法

##### 2.1.1.扩充数据

同MD5 算法、SHA-1 算法，第一步还是要将数据填充为512 bits 的整数倍，也就是64字节的整数倍。这些n 段512bits(64字节)的数据会作为原始信息进行处理

##### 2.1.2.循环运算每一段512bits(64 字节)的数据（MainLoop）

将512bits数据（16*4字节）扩展为64*4字节，对于SHA-256 算法是64次循环，会将16 * 4 字节(32位)扩展到64 * 4字节(32位)。相比，SHA-512 算法是80次循环，所以会将16 * 8字节(64位)扩展到80 * 8字节(64位)。

下面是SHA-256 扩展的伪代码：

```
Extend the sixteen 32-bit words into sixty-four 32-bit words:
for i from 16 to 63
    s0 := (w[i-15] rightrotate 7) xor (w[i-15] rightrotate 18) xor(w[i-15] rightshift 3)
    s1 := (w[i-2] rightrotate 17) xor (w[i-2] rightrotate 19) xor(w[i-2] rightshift 10)
    w[i] := w[i-16] + s0 + w[i-7] + s1
 
```

从第 17个开始进行扩展，用C 代码表示为：

进入主循环，进行64次循环,这里的64次循环跟MD5 算法、SHA-1 算法 有一些区别，这里不会再分几组，而是64次都是相同的操作。

但是还是需要4个函数：

```
Sigma0(x)=shift(x, 30) ⊕ shift(x, 19) ⊕ shift(x, 10);
Sigma1(x)=shift(x, 26) ⊕ shift(x, 21) ⊕ shift(x, 7);
Maj(x,y,z)=(x & y) ⊕ (x & z) ⊕ (y & z);
Ch(x,y,z)=(x & y) ⊕ (~x & z);
```

其中，& 是与运算， | 是或运算，~ 是取反运算，⊕ 是异或运算

具体的运算流程如下图所示：

![image](https://user-images.githubusercontent.com/19474106/119256608-14c80800-bbf4-11eb-92fe-84ca5db9156b.png)


A、B、C、D 、E、F、G、H分别是上一段512bits 处理后留下来的8个整数(第一次运算的时候这8个数为固定的常数)。在对该512bits 数据运算前需要先把这8个整数临时存起来（后面会使用到）。表示一个32 bits(4个字节) 的输入数据(512bits 数据其中的32bits)， 表示一个32bits 的常数(这个也是固定的)。

将上图运算总结成公式：

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


将每一组运算后得到最新的8个数A、B、C、D、E、F、G、H作为下一组运算的初始值，一直到64 次循环彻底结束。一段512bits 的64 次循环结束之后，需要为下一段512bits 准备新的A、B、C、D、E、F、G、H。将上一段64 次循环后最终得到的A、B、C、D、E、F、G、H(也就是上面一步得到的最后的8个数)与循环之前的保存下来的初始值对应相加。

##### 2.1.3.最后一段512bits 运算后得到最终的A、B、C、D、E，即为最终的160bits数因为需要得到最后256bits(64 位16进制)的字符串，所以要将每个4字节的数转换成8位的16进制字符串。

##### 2.1.4. SHA-224 与SHA-256

SHA-224 与SHA-256基本相同，除了8个初始值不同，SHA-224 输出时截掉H 值，得到最后的56位16进制字符串。SHA-512 与SHA-256结构是相同的，但是SHA-512所有数都是64位，SHA-512运行80次循环，SHA-512的初始值、常量值都是64位，SHA-512中偏移量和循环中的位移量也是不同的


##### 2.1.5个初始值不同

SHA-384输出时截掉F、H两个值，得到最后的96位16进制字符串


##### 2.1.6. SHA-256 算法用C 代码实现

````

#include<iostream>
#include<string>
using namespace std;
#define shift(x, n) (((x) << (n)) | ((x) >> (32-(n))))//右移的时候，高位一定要补零，而不是补充符号位
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

//strBaye的长度
unsigned int strlength;
//A,B,C,D的临时变量
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
}
/*
*填充函数
*处理后应满足bits≡448(mod512),字节就是bytes≡56（mode64)
*填充方式为先加一个1,其它位补零
*最后加上64位的原来长度
*/
unsigned int* add(string str)
{
    unsigned int num=((str.length()+8)/64)+1;//以512位,64个字节为一组
    unsigned int *strByte=new unsigned int[num*16];    //64/4=16,所以有16个整数
    strlength=num*16;
    for (unsigned int i = 0; i < num*16; i++)
        strByte[i]=0;
    for (unsigned int i=0; i <str.length(); i++)
    {
        strByte[i>>2]|=(str[i])<<((i%4)*8);//一个整数存储四个字节，i>>2表示i/4 一个unsigned int对应4个字节，保存4个字符信息
    }
    strByte[str.length()>>2]|=0x80<<(((str.length()%4))*8);//尾部添加1 一个unsigned int保存4个字符信息,所以用128左移
    /*
    *添加原长度，长度指位的长度，所以要乘8，然后是小端序，所以放在倒数第二个,这里长度只用了32位
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
        b=((a>>i*8)%(1<<8))&0xff;   //逆序处理每个字节
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
    atemp=A;    //初始化
    btemp=B;
    ctemp=C;
    dtemp=D;
    etemp=E;
    ftemp=F;
    gtemp=G;
    htemp=H;
    unsigned int *strByte=add(source);
    for(unsigned int i=0;i<strlength/16;i++) //512bits 数据分段
    {
        unsigned int num[80];
        unsigned int j;
        for(j=0;j<16;j++)
            num[j]=strByte[i*16+j]; //得到512bits 数据

        for(j=16;j<64;j++)
            num[j]=num[j-16] + S0(num[i-15]) + num[i-7] + S1(num[i-2]); //扩展到64个
        mainLoop(num); //进入主循环
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

SHA-3 算法是第三代标准的哈希函数，基于 Keccak 算法实现。与之前的哈希算法有所不同，SHA-3 算法是基于置换 ( permutation-based ) 的加密函数。

#### 3.1. Sha-3算法流程

输出长度为 X 位的 SHA-3 哈希函数表示为：SHA3-X(M)

下面以输出长度为 256 位的函数为例。标准中，输出长度为 256 位的 SHA-3 函数的表示为SHA3-256(M),其中 M 为需要进行哈希的数据。对数据哈希的过程主要基于海绵结构 ( sponge construction ) 进行，因此先介绍一下海绵结构。

海绵结构

海绵结构能够进行数据转换，将任意长的输入转换成任意长的输出。下图是一个海绵结构的示意图。

![image](https://user-images.githubusercontent.com/19474106/119256665-61abde80-bbf4-11eb-8af6-700be137048a.png)


如图所示，海绵结构包含 3 个重要的组成部分：

一个对数据进行等长映射的函数 f，即输出串长度与输入串长度相同，记为 b。

一个参数称为比率 ( rate )，记作 r，是指每轮要吸收的 长度为 b 的串中数据的长度，剩余部分称为容量，记为 c，因此，有 b = r + c。

一个填充 ( padding ) 函数，记作 pad(x,,m)，返回将长度为 m 的串填充为 x 的整数倍长度的串。例如 pad(5,2)=010，指将长度为 2 的串填充为 5 的整数倍长度，需要添加一个长度为 3 的串，任意长为 3 的串均可，本例中返回值为 010，其长度为 3。

给定上述组成后，可以对数据进行操作并得到映射结果。形式化定义如下：

SPONGE[f,pad,r]

基于该海绵结构可以定义海绵函数，用于将输入转换成指定长度的串，因此，函数有两个参数：1. 输入串 N，2. 输出长度 d。函数定义如下：

SPONGE[f,pad,r](N,d)

下面根据图，简要说明海绵函数的执行流程：

1.首先对输入 N 进行填充，使其长度为 r 的整数倍，结果为 P = N || pad(r, len(N)), “||” 表示串连接。

2.记 n =len(P)/r，将 P 分成 n 段，记为 P = P0||P2|| ...Pn-1, 每段长度为 rr。

3.定义 S = 0^b 表示长度为 b 的 0 串，这个 S 也被称为状态，之后进行介绍。

4.定义 i 从 0 到 n−1，对 S 依次进行转换，S =f(S⊕(Pi∣∣0^c))，上述过程称为吸收 (absorbing) 过程。

5.定义 Z 为空串。

6.Z = Z∣∣Truncr(S)，其中 Truncr(S) 指 S 前 r 个字符组成的串。

7.如果此时 d≤len(Z)，返回 Truncd(Z)

8.令 S=f(S)，返回步骤 6。



#### KECCAK 海绵函数

定义一个海绵结构需要指明海绵结构中的三个组成成分

1.一个对数据进行等长映射的函数 f。

2.一个参数称为比率 r。

3.一个填充 ( padding ) 函数，记作 pad(x,m)。

SHA-3 中使用的 KECCAK 海绵函数的三个组件形式如下：

1.映射函数 KECCAK-p[b,nr](S)，将长度为 b 的串 S，经过 nr 轮转换输出为长度为 b 的结果，也被称为 KECCAK-p 置换函数。该函数之后会详细说明。

2.比率 r 根据输出长度不同进行调整。

3.填充函数为 pad10∗1(x,m)，除了返回将长度为 m 的串填充为 x 的整数倍长度的串外，还保证返回的串满足表达式 10∗1 形式。



#### KECCAK-p 置换

KECCAK-p 置换将输入串进行多轮重新排列得到长度相同的输出串。设输入串 S 长度为 b，置换进行 nr 轮重新排列，则进行的 KECCAK-p 置换函数记为


![image](https://user-images.githubusercontent.com/19474106/119256679-75574500-bbf4-11eb-9db3-732ca3dbe4f9.png)


其中，b∈{25,50,100,200,400,800,1600}


置换函数也可以认为是在进行状态转移，前面提到，这个函数的输入 S 又称为状态，KECCAK-p 置换，就是对 S 进行状态转移。下面简要介绍一下状态的概念。

状态 ( state )


一个一直被更新的位数组称为一个状态。一个状态可以表示成一个位串或一个状态数组。位串就是指状态的二进制串，记为 S，长度记为 b；状态数组将状态表示为一个 5×5×w 的三维数组，其中 w = b/25，记为 A。S 和 AA都表示状态，可以互相转换。

状态数组中的每一位可以用 A[x, y, z]表示，状态数组的坐标系统如下所示：

![image](https://user-images.githubusercontent.com/19474106/119256687-7c7e5300-bbf4-11eb-9503-930b84c9532e.png)


其中，x，y 方向都以中心点为原点。下面是状态数组中不同子数组的命名。

![image](https://user-images.githubusercontent.com/19474106/119256690-856f2480-bbf4-11eb-870e-a2137dbfc2e3.png)


阶段映射 ( step mappings )
SHA-3 标准中共有 5 个映射函数，可以对状态数组 A 进行不同的排列，下面简要进行介绍。

θ(A)，对 columncolumn 进行重排列。

ρ(A)，对 lanelane 进行重排列。

π(A)，对 sliceslice 进行重排列。

χ(A)，对 rowrow 进行重排列。

ι(A,ir)，对 A[0,0,z] 部分进行重排列。

对于 nr 轮转换，每一轮使用函数 Rnd 进行转换：

![image](https://user-images.githubusercontent.com/19474106/119256694-8dc75f80-bbf4-11eb-8fc1-f943f80da618.png)


置换过程
置换过程总结如下：

![image](https://user-images.githubusercontent.com/19474106/119256699-94ee6d80-bbf4-11eb-8cd2-825c2518629d.png)


定义 SHA-3

SHA-3 中的哈希函数基于 Keccak 海绵结构实现，并将一些参数设置为常量：

设置 KECCAK-p 置换输入长度为 1600 bit，也是状态的长度。

设置 KECCAK-p 置换进行 24 轮。

参数 r = 1600 - c，且其值取决于需要输出的哈希结果的长度。因此，SHA-3 中使用的海绵函数定义为：

![image](https://user-images.githubusercontent.com/19474106/119256708-9e77d580-bbf4-11eb-864f-9d4d53be89c6.png)


参数 c 取决于输出长度。基于上述定义，SHA-3 哈希函数定义如下：

![image](https://user-images.githubusercontent.com/19474106/119256714-a46db680-bbf4-11eb-8b16-2e156ab84375.png)

其中，c 被设为输出长度的 2 倍，输入串还需要添加后缀 01 作为海绵函数的输入。SHA-3 系列函数最终分别得到给定长度的哈希结果。


## 四. Blake 和 Blake2

我们都知道，哈希算法 (Hash Algorithm) 是将任意长度的数据映射为固定长度数据的算法，也称为消息摘要。一般情况下，哈希算法有两个特点, 一是原始数据的细微变化（比如一个位翻转）会导致结果产生巨大差距；二是运算过程不可逆，理论上无法从结果还原输入数据。因此，哈希算法主要用于数据完整性校验和加密/签名。

哈希算法的安全性就在于碰撞难易度，即已知结果，构建出具有相同结果的输入数据的难易度。

常见的哈希算法有 MD5, SHA-1, SHA-2, SHA-3。其中 MD5 已经可以在 2^21 复杂度（在主流智能手机上只需30秒）内完成碰撞，谷歌也于17年早些时候在 2^64 复杂度（约 110 GPU年的计算量）内完成了第一次 SHA-1 碰撞。至此，MD5 和 SHA-1 已经在安全领域被废弃。当前除了 SHA-2，SHA-3 之外，还有另外一个哈希算法系列可供选择，那就是 BLAKE，BLAKE2 系列比常见的 MD5，SHA-1，SHA-2，SHA-3 更快，同时提供不低于 SHA-3 的安全性。BLAKE2 系列从著名的 ChaCha 算法衍生而来，有两个主要版本 BLAKE2b（BLAKE2）和 BLAKE2s。

BLAKE2b 为 64 位 CPU（包括 ARM Neon）优化，可以生成最长64字节的摘要；BLAKE2s 为 8-32 位 CPU 设计，可以生成最长 32 字节的摘要。

二者的衍生版 BLAKE2bp 和 BLAKE2sp 可以进行多核并行计算，在保持相同安全性的前提下，进一步提升计算速度。此外，BLAKE2 系列有一个特殊的变种，BLAKE2x，可以生成最多 4GiB 的“摘要”，可以用于 KDF（密钥派生）和 DRBG（固定随机数序列）。

BLAKE2 算法基于 BLAKE 算法，2012年被提出，也就是说在 Blake2 之前 Blake 系列算法已经产生。BLAKE 算法于2008年提出，它包含两个版本，一种基于32位word用于产生最长256位的哈希结果，一种基于64位word用于产生最长512位的哈希结果，BLAKE算法核心操作是不断地将8个散列中间结果和16个输入word进行组合，从而产生下一轮组合的8个中间结果。按照最终截断的哈希长度，BLAKE-256和BLAKE-224使用32位字分别产生256位和224位的哈希结果（也称消息摘要），而BLAKE-512和BLAKE-384使用64位字并产生512位和384位哈希结果。

blake源码可以参考：https://github.com/veorq/BLAKE

blake2 的源码可以参考：https://github.com/BLAKE2/BLAKE2








