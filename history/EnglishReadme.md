[![Chinese](https://img.shields.io/badge/Chinese-README-red)](README.md)


# Chapter 2: A brief history of the development of cryptography

Cryptography has been around since more than 400 BC. The history of human beings using cryptography is almost as long as the use of words. The development of cryptography can be roughly divided into three stages: the classical cryptography stage before 1949; Cryptography became a branch of science in 1975; after 1976, symmetric key cryptography algorithms were further developed, giving rise to a new direction in cryptography—public key cryptography. In 1976, W.Diffie and M.Hellman first publicly proposed the concept of public-key cryptography in their article "New Directions in Cryptography". The proposal of public key cryptography realizes the independence between the encryption key and the decryption key, and solves the problem that both communicating parties must share the key in the symmetric cryptography system. It has epoch-making significance in the cryptography community.

### 1. Classical cryptography

The history of classical cryptography can be traced back to 400 AD. The Spartans invented the "Serta cipher", which is to spirally wrap a long strip of paper diagonally around a polygonal rod, and write words along the horizontal direction of the rod. Write from left to right, write a word and rotate it. After writing one line, start another line and write from left to right until you finish. After being decoded, the text message on the note is messy and unintelligible. This is the cipher text, but after wrapping it around another rod of the same size, the original message can be seen. This is the earliest cryptographic technology.

In ancient my country, there have been records of hiding the true meaning or "secret words" in specific positions in poems or paintings in the form of acrostic poems, acrostic poems, omit poems and paintings. Most people only pay attention to the meaning of poems or paintings. Surface artistic conception, without paying attention to or finding it difficult to discover the "subtext" hidden in it. For example, in "Water Margin", Liangshan wanted to recruit Lu Junyi to join the gang, and Wu Yong and Song Jiang, who were both "intelligent," came up with a story about "Wu Yongzhi earns jade unicorns". Taking advantage of Lu Junyi's fear of avoiding the "bloody disaster", he wrote four lines of hexagrams:

     A small boat among the reed flowers,
     Junjie traveled from here. ​
     If a righteous person can understand this principle,
     There is no need to worry if you can't escape. ​

The four words "Lu Jun rebelled" are hidden. As a result, it became evidence for the government to punish him, and finally "forced" Lu Junyi to Liangshan.

More widely known is "I Love Qiuxiang" written by Tang Bohu:

     I paint the blue river and the long flowing water,
     I love the sadness of maple leaves in the evening pavilion.
     The autumn moon shines brightly on the Buddhist temple,
     Cigarettes curled around the sutra building.

Ancient treasure maps, after layers of encryption, are actually a manifestation of my country's classical cryptography.

Cryptography during this period was more like an art, and its core methods were substitution and replacement. Substitution means that each character in the text is replaced with another character in the ciphertext, and the receiver can restore the plaintext by reversely replacing the ciphertext; substitution means that the letters in the ciphertext and plaintext remain the same, but the order is disrupted. Famous examples of substitution ciphers include the Roman Caesar cipher (1st century BC) and the French Vigenère cipher (16th century BC). The Caesar cipher replaces each letter in the alphabet with the k-th letter after it. For example, "comeatnine" is encrypted into "htrjfysnsj" (k=5). However, this encryption method cannot conceal the frequency characteristics of each letter and is easily cracked. The Vigenère cipher improves security in comparison. Its key is usually a word, such as "hear". For the above plaintext "comeatnine", the first letter is shifted back by 8 bits during encryption (the key The first letter h of "hear" is in the 8th position of the alphabet), the second letter is shifted back 5 bits (the second letter e of the key is in the 5th position of the alphabet),..., so the encrypted result It's "jsmvhxnzui".

We all should have seen the Anti-Japanese War movies, in which messages were sent in cipher text, and this cipher text would correspond to a codebook, such as the book "Romance of the Three Kingdoms". Its encryption method will tell you that the encrypted text belongs to the word in the book. When you complete the decryption, you can get the plaintext message. This is a common classical encryption method.

#### 1. Several classical cryptography

##### 1.1. Rolling bucket password

In order to ensure the encryption of communication information, the ancient Greeks encrypted the information by using a stick called scytale. The sender first spirally rolls a parchment strip around a stick, then writes the message to be written on it in a certain order, then opens the parchment strip and delivers the letter to the recipient through other channels. It is not easy to decrypt the contents without knowing the thickness of the stick, but the recipient can use the same scytale stick to decrypt the letter according to a prior agreement with the writer.

Below is an example:

Cipher text:

After everyone's thoughts, the name of the playhouse was buried in the coolness of some short Qi Guan characters, and the wind was rushing to teach him to blow him into a ditch that came from the front hall to welcome the family. Here, there are teachings in Lingtong ritual and the soul of the courtyard. The one served in Shiguotang is the after-dinner meal. Because of this, the industry is surrounded by wind. According to ancient and Chinese works, the tree is right. The sand in this city is similar to the one in Zhongtian that looks like the sand passing by. It is said that it is a group market. The death wells did not ring for a long time. After the stone bottom in Xingong City, the people under the long board were allowed to go and bury themselves comfortably. They cared about the country in life and death. Also use Kai Zhiduo. The emperor asked the Boshi people to play with the most human race, the laughing Boshi people, who felt super close to the ground. The leader of the engraving office in Deyue City led the way with the words of the Emperor and our people wishing for peace in the summer.

Plain text after decryption by roller

.：
     ![.：
](/img/1.png)

##### 1.2. Mask password

The mask cipher invented by Cardano, a physicist and mathematician in Milan in the 16th century, can design the openings of the grid in advance to combine the information to be transmitted with some other irrelevant symbols into invalid information, making it difficult for the interceptor to analyze the valid information. information.

##### 1.3.Chessboard password

We can create a table so that each character corresponds to a number , which is the row label where the character is located, and is the column label. This turns the plaintext into a string of digital ciphertext.

##### 1.4. Caesar Cipher

During the Roman Empire, Julius Caesar designed a simple shift cipher for wartime communications. This encryption method is to put the letters of the plain text in alphabetical order, and then recurse the same letters in order to get the encrypted cipher text. The decryption process is exactly the opposite of the encryption process.

Principle: Replace one letter with another letter at a fixed position behind it (single representation of password replacement).

A B C D E F G……X Y Z

D E F G H I J…A B C

Plain text:Caesar cipher is a shift substitution

Cipher text: FDHVDU FLSKHU LV D VKLIW VXEVWLWXWLRQ

##### 1.5. Furnham Cipher

In 1918, Gilbert Vernam designed a one-time pad cipher (multi-representation substitution cipher) for AT&T.

Principle: Use an arbitrarily long sequence of non-repeating numbers and combine it with plaintext.

Plain text: V E R N A M C I P H E R

Equivalent numbers: 21 4 17 13 0 12 2 8 15 7 4 17

+Random numbers: 76 48 16 82 44 3 58 11 60 5 48 88

and mod26: 19 0 7 17 18 15 8 19 23 12 0 1

Cipher text: t a h r s p i t x m a b

##### 1.6. Disk cipher

People have further improved the Caesar cipher. As long as the letters are moved in different orders, the difficulty of cracking can be increased and the confidentiality of the information can be increased. For example, the disk cipher invented by Alberti, a Florentine in the 15th century, is a typical encryption method using single table substitution. As shown in the picture on two concentric disks, the inner disk is filled with letters or numbers in a different (messy) order, while the outer disk is filled with letters or numbers in a certain order. By turning the disk, you can find the replacement method of the letters, which is very convenient. Encryption and decryption of information. The essence of the Caesar cipher and the disc cipher are the same. They are both single-table substitutions, that is, the ciphertext letters corresponding to a plaintext letter are determined. The interceptor can analyze the frequency of occurrence of the letters and carry out effective attacks on the cryptographic system. Alberti's disk theory is one of the main representatives of classical cryptography. Carving letters with spaces on the surface of a clay disk became the first human encryption method, and no one has been able to break this method to this day.

##### 1.7. Vigenère Code

In order to improve the difficulty of deciphering passwords, people have invented a multi-table substitution cipher, that is, a plaintext letter can be represented as multiple ciphertext letters. The results of the multi-table cipher encryption algorithm will enable a simple frequency analysis method to be used for single-table substitution. Invalid, the Vigenère cipher is a typical encryption method. The Vigenère cipher uses a phrase (statement) as a key. Each letter in the phrase is used as a shift substitution cipher key to determine a substitution table. The Vigenère cipher uses each substitution table cyclically to complete the plaintext letters to After the transformation of ciphertext letters, the final sequence of ciphertext letters is the encrypted ciphertext. Virginia is an important milestone in the development of classical cryptography theory, and his theory is also called polyalphabetic coding.

m shift substitution tables are determined by key words composed of m letters

Plain text: w e a r d i s c o v e r e d s a v e

Key: d e c e p t i v e d e c e p t i v e

Corresponding numbers: 3 4 2 15 19 8 21

Cipher text: Z I C V T WQNGRZGVTWAVZH


##### 1.8. Transposition password (replacement password)

1. Transposition is to rearrange the positions of letters in plain text. The simplest transposition is the reverse order method:
      
Plain text: computer system

Secret text: metsys retupmoc

2. Column permutation (column permutation): Rearrange the characters in the plaintext by columns.
For example:
Plain text: THIS IS A MESSAGE.

           T  H  I  S  I
          
           S  A  M  E  S
          
           S  A  G  E  X
          
Cipher text:TSSHAAIMGSEEISX

3.Introduce key k

For example, k=COMPUTER, the plain text is: WHAT CAN YOU LEARN FROM THIS BOOK

.：
     ![.：
](/img/2.png)


The cipher text is: WORO NNSX ALMK HUOO TETX YFBX ARIX CAHX

##### 1.9. Encryption of Enigma wheel set

The encryption principle of the Enigma wheel set is exactly multi-table replacement - it continuously changes the letter mapping relationship between plaintext and ciphertext, and performs continuous table-changing encryption operations on plaintext letters.

.：
     ![.：
](/img/3.png)



* The different directions of the three rotors constitute 26*26*26=17576 different possibilities;
* There are 6 possibilities for different relative positions between the three rotors;
* The number of possibilities for exchanging 6 pairs of letters on the connecting board is very huge, 100391791500; so there are 17576*6*100391791500 in total, which is about 10000000000000000, or one hundred billion possibilities.

At that time, the price of an Enigma wheel set was RMB 240,000.

In the 1930s, he led Polish cryptographers to take the lead in systematically studying and deciphering the Enigma cipher used in Germany. In the process of deciphering, Rejevsky applied strict mathematical methods to the field of code deciphering for the first time, which was an important achievement in the history of cryptography. Rejewski and others deciphered a large number of messages from Germany during World War II, and their work became the basis for the Allies to decipher the German Enigma code throughout World War II. Rejewski, together with Polish mathematicians Jerzy Rozoki and Henrik Zogarski, is known as the "Three Polish Masters" in the field of cryptography research.

.：
     ![.：
](/img/4.png)


### 2. Modern cryptography

Cryptography was formed as a new discipline in the 1970s, which was stimulated and promoted by the booming development of computer science. On the one hand, fast electronic computers and modern mathematical methods provide new concepts and tools for encryption technology, and on the other hand, they also provide powerful weapons for decipherers. The arrival of the computer and electronics era has brought unprecedented freedom to cryptographic designers. They can easily get rid of the mistakes that were easily made when designing by hand with pencil and paper, and no longer have to face cryptographic machines implemented by electronic machinery. high fees.

Arthur Scherbius designed the most famous cipher machine in history, the German Enigma machine, in 1919. During World War II, Enigma served as the most advanced cipher machine for the German army, navy and air force. The Enigma machine uses 3 regular wheels and 1 reflective wheel. This prevented the British army from interpreting the signals sent by German submarines from February to December 1942. The use of the wheel cipher machine greatly improved the speed of password encryption, but due to the limited amount of keys, by the middle and late World War II, it triggered a confrontation between encryption and deciphering. First, the Poles used the repetition of the first few letters in German telegrams to crack the early Enigma cipher machine, and then told the French and British the deciphering method. The British father of computer theory——Under the leadership of Turing, he cracked a lot of very important German intelligence by looking for mistakes made by the Germans in key selection, successfully seizing part of the German codebooks, obtaining the keys, and conducting selected plaintext attacks.

This stage really began with a series of papers published by Shannon in the late 1940s, especially the "Communication Theory of Secrecy Systems" in 1949, which pushed the thousands-year-old cryptography onto a scientific track based on information theory. close
An important breakthrough in the development of cryptography is the emergence of the "Data Encryption Standard" (DES). The significance of the DES cipher is that, first of all, its emergence enabled cryptography to move from the government to the private sector. Its design was mainly completed by IBM, with the National Security Agency and other government departments only participating in it. Finally, after an open call and selection by the United States National Bureau of Standards, it was determined to be Federal Information Processing Standards. Secondly, many ideas in DES cipher design (Feistel structure, S box, etc.) were adopted by most subsequent block ciphers. Once again, after the emergence of DES, it was not only used in the U.S. federal departments, but also became popular around the world and was widely used in finance and other commercial fields.


### 3. Modern cryptography

In 1976, American cryptographers proposed the concept of "public key cryptography". Different keys are used for encryption and decryption in this type of password. The one used for encryption is called the public key, and the one used for decryption is called the private key. In 1977, the Massachusetts Institute of Technology in the United States proposed the first public key encryption algorithm, the RSA algorithm. After that, ElGamal, elliptic curve, and bilinear peer-to-peer public key cryptography were successively proposed, and cryptography truly entered a new period of development. Generally speaking, the security of public key cryptography is guaranteed by the difficulty of solving the corresponding mathematical problems on computers. Taking the widely used RSA algorithm as an example, its security is based on the decomposition of large integer prime factors on computers. Difficulty, for example, for the integer 22, we can easily find that it can be decomposed into the multiplication of two prime numbers 2 and 11, but for a 500-digit integer, even if the corresponding algorithm is used, it will take a long time to complete the decomposition. However, with the continuous enhancement of computing power and the continuous improvement of factorization algorithms, especially the development of quantum computers, the security of public key cryptography is gradually threatened. At present, researchers are beginning to pay attention to cryptography that is resistant to quantum algorithms such as quantum cryptography and lattice cryptography. Cutting-edge cryptography technologies such as post-quantum cryptography have gradually become a research hotspot.

### 4. Quantum cryptography

Quantum cryptography is a new and important encryption method that uses the quantum properties of single photons to achieve provable security of data transmission with the help of quantum key distribution protocols. Quantum cryptography has the characteristics of unconditional security (that is, there is no need to possess sufficient time and computer power (eavesdropper attack), and private keys do not need to be exchanged before actual communication occurs. This article reviews the research progress of quantum cryptography, including the physical basis of quantum cryptography, quantum key distribution, Secrecy enhancement, practicality of quantum keys, and pitfalls of current technology limitations.


### 5. Prospects of cryptography

The idea of public key cryptography proposed by Diffie and Hellman in 1976 marked the birth of modern cryptography and was a landmark event in the history of the development of international cryptography. Since then, many public key cryptography systems have been proposed internationally, such as Cryptosystems based on the difficulty of decomposing large integers - RSA cryptography and its variants, public key cryptography based on the discrete logarithm problem - ElGamal cryptography and its variant ECC, etc., have been widely used, and It provides a variety of security services (such as confidentiality, credibility (identification), integrity, non-repudiation, availability and access control, etc.) in today's information age. The security of these public key cryptography systems all depends on the difficulty of mathematical problems (large integer decomposition problems and discrete logarithm solution problems). However, in the case of quantum computing, these problems can be turned into easy-to-solve problems - P problems through Shor's algorithm. Therefore, we can conclude that the day when quantum computers appear will be the day when today's cryptography comes to an end. Therefore, studying cryptographic algorithms for quantum-resistant calculations is a new research direction in future cryptography.