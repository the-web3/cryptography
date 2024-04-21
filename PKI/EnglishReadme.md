[![Chinese](https://img.shields.io/badge/Chinese-README-red)](README.md)

# Chapter X: PKI Public Key Infrastructure

Public Key Infrastructure (PKI) is a typical cryptographic application technology. In the PKI system, the Certificate Authority (CA) issues a digital certificate and binds the PKI user's identity information and public key. The PKI relying party (Relying Party) pre-stores the root CA self-signed certificate that it trusts, which is used to verify the certificate chain of the PKI user communicating with it, thereby credibly obtaining the user's public key for various purposes. Security services.

### A brief history of the development of PKI

In 1978, L. Kohnfelder first proposed the concept of certificates; in 1988, the first version of the X.509 standard was launched and developed into the version 3 standard in 2005; in 1995, the IETF established the PKIX working group to use the Internet, 2013, the IETF PKIX working group concluded its work. After years of technical research, PKI technology has made great progress and is widely used, playing an important security supporting role in global information systems.

### Identity authentication technology

Identity authentication technology is the first barrier to protect information security. Its core technology is the information security assurance system, which is also the most basic link. Its basic idea is to determine whether the user's identity is authentic by verifying the attributes possessed by the user. According to different standard identity authentication technologies, it is divided into four types.

According to the different properties of the authentication message, it is divided into the following three types: First, physical media authentication is based on the physical media held by the verified party for identity authentication, including credit cards and token cards; second, secret knowledge authentication is The two communicating parties use secret information they share to authenticate their identities, such as passwords, personal identification codes, etc.; the third is entity feature verification. On the one hand, it is the physical characteristics of the entity, such as the serial number of the hard disk, etc., and on the other hand, it is the biology of the individual. Features such as fingerprints and voices.

There are two types of authentication, one-way and two-way, based on the correlation between the entity to be authenticated and the entity. In a one-way system, the verified party must trust the verifier, and the verified party provides authentication information to the verifier. In a two-way system, the two parties must provide each other with their own identity verification information to verify each other.

According to the authentication object, it is divided into entity identity authentication and information identity authentication. The former is mainly used to identify the true identity of entities, and the latter is mainly used to ensure non-repudiation, integrity and freshness in the message delivery process.

According to the trust relationship between the two parties, it is divided into two categories: non-arbitration authentication and arbitration authentication. In the non-arbitration authentication system, the two parties transmitting messages work together to resist the enemy's attack, and both trust the other party. In an arbitration authentication system, any party may cheat during the communication process. Neither party trusts the other party. If a dispute occurs, it will be arbitrated by a trusted third party. Currently widely used are: password-based verification methods, biometric-based verification, PKI technology-based verification, etc. In the actual design and application process of identity authentication systems, designers often use multiple authentication mechanisms at the same time to configure two or more authentication methods with each other to achieve the goal of making the authentication process more secure and reliable.

#### Commonly used identity authentication methods

##### **Password-based identity authentication technology**

There are two types of passwords: static passwords and dynamic passwords. The former is a commonly used method in the past, and its principle is that the system has an authentication server. The server saves a set of information for each user in advance, that is, user name ID and password PW. When the user requests to access the system, the user enters the user name and password on the client or terminal. The system matches the user name and password entered by the user with the user name and password information of the legal user stored in the authentication server. If the match is successful, the user is proved to be a legal user and the user is allowed to access system resources. Otherwise, the user's identity has not been verified. The system denies user login and access. The advantages of static passwords are that they are easy to use, extremely simple to operate, low in cost, and fast to run. However, they also have many security risks, such as being easily stolen, impersonated, and snooped.

Dynamic passwords are created to deal with security risks that may arise with static passwords. Dynamic passwords are also called one-time passwords. They use a one-time password method. Each time a user uses a dynamic password token to generate a dynamic password, because only legitimate users can use the dynamic token, the authentication server can authenticate the user by verifying the password, ensuring Security of user identity. Dynamic passwords are divided into synchronous and asynchronous authentication technologies. Synchronous authentication technology has two methods: time-based and event-based; asynchronous authentication technology is based on "challenge-response" authentication technology. For example, when using authentication technology based on time synchronization, if the time on the client side and the server side are not consistent, the user may not be able to log in to the system.

##### **Biometric-based identity authentication technology**

Identity authentication based on biometrics refers to the use of user-specific biometrics, such as iris, fingerprint, and voiceprint authentication technology. Identity authentication based on biometrics is basically considered the most trustworthy authentication method. It is almost impossible to find two people with the same biological characteristics. User information is unique and irreplaceable, and users cannot be counterfeited.

Among them, the fingerprint identity authentication system analyzes, extracts and retains all and part of the characteristics of the fingerprint, and compares the user's fingerprint with the previously stored fingerprints to verify the authenticity of the user's identity. Voice tattoo identity authentication saves the speaker's speech waveform in advance, and compares the speech signal to be recognized with the speech parameters that reflect the speaker's vocal tract and pronunciation characteristics in the speech waveform to identify the speaker's identity. However, biometric recognition technology is not yet fully mature, and its stability and accuracy are not high enough. For example, during fingerprint recognition, if the user's fingers are stained or injured and the fingerprint changes, the system cannot recognize the user's fingerprint information as usual. The user is denied access by the system. In addition, because the research and development cost of the biometric authentication system is high and the market applications are relatively small, it cannot be widely promoted at this stage.

##### **PKI-based identity authentication technology**

PKI is public key infrastructure, which is an infrastructure that follows public key cryptography theory and technology to provide a universal security service platform for e-commerce and other services. The basic principle is: a third-party authority, the identity authentication center CA, combines the public key held by the user with his or her identity information (such as name, phone number, etc.). Before the two are combined, the identity authentication center CA confirms the authenticity of the user's identity, and then the identity authentication center CA signs the certificate bundled with the user and his public key, and the signed certificate is valid.

Each user has a pair of public and private keys. The public key is public in the network and is used to encrypt information when sending files; the private key is confidential and belongs only to the user and is used to encrypt file information. Decrypt and sign. When preparing to send a message, the sender uses the receiver's public key to encrypt the data to be transmitted. After the receiver obtains the data, it uses the private key it holds to decrypt the aura. In this way, users can communicate securely on the PKI service platform.

PKI-based identity authentication technology uses public key technology, digital signatures are non-replicable, and data is protected completely and confidentially. PKI adopts the digital certificate method. The digital certificate is issued by a third-party trusted authority CA and stored in independent devices such as USB Key and IC smart card. It is not transmitted on the network and can prove the user's identity without online query of the digital certificate. It can be expanded Users expand the scope of services and can serve large user groups. PKI technology provides a recovery and revocation mechanism for digital certificates. If the user's digital certificate is lost or the user's information changes, the digital certificate can be restored or revoked to prevent the digital certificate from being stolen or maliciously misappropriated. PKI-based identity authentication technology is flexible and scalable.

### PKI related technologies

#### Symmetric key encryption technology

Symmetric encryption technology, that is, dedicated key encryption technology or single-key encryption technology, the encryption key and the decryption key are the same, and the sender and receiver use the same set of public and private keys to encrypt or decrypt information. A key requirement for data encryption is having the same key to decrypt it. Because both communicating parties share a key, if the key is lost or leaked, the person who obtains the key can encrypt or decrypt the data. Therefore, the security of the key must be ensured to ensure the confidentiality of the message.

Currently commonly used symmetric encryption algorithms include DES, AES, etc. This algorithm is relatively simple and has a relatively small amount of calculation. It is open to the network and can be encrypted efficiently. At the same time, there are shortcomings. First, the communicating parties negotiate a common key in a non-face-to-face manner, so the security of the negotiation process cannot be guaranteed. Second, both communicating parties use a unique key every time they transmit data. This makes symmetric encryption technology need to use and generate a large number of keys in an open network, and the management of keys becomes a great burden for users. Third, the symmetric encryption algorithm can only encrypt and decrypt data to ensure the confidentiality of the data, but it cannot verify the true identity of the communicating parties and cannot determine the integrity of the data.

#### Asymmetric key encryption technology

Asymmetric key encryption technology consists of a public key and a private key to form a key pair. The public key is disclosed to the public and the private key is kept solely by the key holder. When communicating parties use asymmetric keys to encrypt and decrypt data, they must use matching public and private keys. Such algorithms include RSA, PKCS, etc.

It has two methods: one is that the sender uses the receiver's public key to encrypt the information, and the receiver uses its private key to decrypt the information. In this way, the receiver can receive encrypted data from multiple senders, and this encrypted data Only one user on the receiving end can interpret it; the other is that the sender uses its own private key to encrypt the information, and the receiver uses the other party's public key to decrypt the information. Such a message may be decrypted by multiple receivers.
   
The advantage of asymmetric key encryption technology is that it simplifies the process of key issuance and management, and supports security authentication technologies such as digital signatures. The disadvantage is that the calculation process of encryption and decryption is particularly complex, and the speed of running data encryption and decryption is relatively slow.
 
In practical applications, two encryption technologies are often used simultaneously to solve various problems in the data encryption and decryption process.

#### Message summary

The core features of this algorithm are: first, no key is used for encryption; second, if you need to obtain the same encrypted ciphertext data, you must meet two conditions: use the same message digest algorithm and provide the same original text data; Third, the encrypted data cannot be reversely decrypted. The message digest algorithm has a wide range of applications, including distributed networks, etc.

If original text data of different lengths are input and calculated by the same message digest algorithm, the length of the message digest obtained will be the same, that is, the length of the message digest will not change due to more or less input original text data. However, different algorithms have their own fixed lengths, such as MD5 algorithm is 128 bits, SHA-1 is 192 and 256 bits. It is generally believed that the security level of a message digest algorithm is directly proportional to the length of the calculated message digest, that is, the longer the digest, the more secure the algorithm is.

The content of the message summary may appear to be random, but it is not actually random. This can be demonstrated by inputting different original data multiple times to check whether the results calculated by the message digest algorithm are the same. Usually the message digest obtained by inputting different original data is different. If it is truly random, then the input will be the same every time. For the original text data, the message digest obtained should be different. The message digest obtained each time is irreproducible. However, this is not the case. The same message digest is obtained from the same original text data calculated by the same message digest. That is to say Message digests are not truly random. At the same time, the contents of the two original data are basically similar, but the resulting message summaries are very different.

The message summary uses a one-way function, which can only calculate the message summary from the original text data. However, the original text data cannot be obtained reversely based on the message summary, or even any relevant information of the original text data cannot be found. If you try a brute force attack and calculate the message digest backwards to determine whether it is the same as the existing message digest, the relevant information obtained is one of tens of thousands of possible messages, so the brute force attack method is not advisable.

The message digest algorithm plays an important role in constructing a digital signature scheme. The message digest calculated through it is closely related to the original data. Changing the original data will cause the message digest to change, and it is always a fixed length, which is much shorter than the original data. There is a one-way one-to-one relationship between the message digest and the original data. Signing the message digest of the data greatly improves the signature efficiency.

#### Digital Certificate

The receiver uses the sender's public key to decrypt the other party's digital signature to verify whether the information was provided by the sender, but it cannot prove that the sender is consistent with the owner of the data it claims. At the same time, although the public key is public, it does not rule out security loopholes and the digital signature may be forged. Currently, digital certificates are mainly used to solve the above problems.
      
A digital certificate is actually a piece of data issued by a certification center that contains the certificate holder's real identity information, public key information and other information. Moreover, its function is similar to that of the daily resident ID card. The digital signature issued by the identity authentication agency can ensure the authenticity of the digital certificate information. The digital certificate holder has a private key that belongs only to him/her, and uses it to sign the information to be transmitted or decrypt the received information; at the same time, he/she discloses a public key and shares it with a group of people who need to communicate. User, used to encrypt information and verify signatures.

Usually, the digital certificate issuance process is that before the user applies to the identity certification center, he must generate his own pair of keys, and then send the application containing his identity information and public key to the certification center. The certification center first verifies the relevant information provided by the user. In this process, it must perform key steps to confirm that the application was sent by the user himself. Then the certification center issues a digital certificate to the applying user. The certificate stores the user name, public key and other relevant information. Information, digital signature information. Users holding digital certificates can perform data transmission, online banking and other related activities. The agency that issues digital certificates is a trusted third-party independent agency. Due to the different areas authorized by the issuing agency, the types and uses of the certificates are also different, and various types of

Certificates also vary greatly in their level of trustworthiness. Digital certificates have the following three characteristics:

It is a component of the PKI system. All security services provided by the PKI system are based on digital certificates. Every step in the system operation process is inseparable from digital certificates. It can be said that digital certificates are the core component of PKI.

Digital certificates are authoritative. It is authenticated by an authoritative, trustworthy and impartial third-party identityThe certification center CA issued by the central CA provides identity authentication services for specific application networks and users. It is responsible for verifying the legitimacy of the public key and proving that the user is the legal holder of the certificate. At the same time, it issues, distributes, stores, updates and deletes certificates.

Digital certificates not only carry the user's public key but also prove the user's identity. At present, the format of digital certificates generally follows the X.509V3 international standard. The certificate includes the version number, serial number, algorithm, and naming rules of the certificate. Usually the X.500 format, validity date, name, public key information, and digital certificate issuer identifier are used. X.509V3 digital certificates include extended identifiers, criticality indicators, and extended field values. Digital certificate extensions include key information, policy information, etc.

#### digital signature 

A digital signature means that the sender of the data encrypts a piece of data using a cryptographic algorithm, and processes it to generate a piece of plus data and sends it to the receiver together with the original data.
    
Digital signatures are used to prove the authenticity of the sender's data. Because the public key is public to a certain range of users, multiple people can use the public key to encrypt data, and the recipient can use the digital signature to confirm the identity of the sender. When the cryptographic system is secure, the receiver can authenticate the sender's true identity through this method.
    
Digital signatures ensure the integrity of transmitted data, prevent the identity of the data sender from being forged, and prevent data from being intercepted, modified, and forwarded by third parties through illegal means during the transmission process. Although there is no guarantee that the data will never be modified by a third party, This approach makes it very difficult for third parties to read the data.
 
Digital signatures ensure the non-repudiation of transactions. After using a digital signature, the sender cannot deny that the data has been transmitted, and the recipient of the data can use the digital signature to prove the sender of the data.

#### Hash value digital signature

The hash function is one-way, strongly collision-free, and it is infeasible to find the second preimage. When data of any length is encrypted and compressed by the Hash algorithm, a hash value of a specified length will be generated. The process of hash value digital signature is: first, use the Hash algorithm to encrypt the original data to generate a fixed-length hash value; second, use the sender's own private key to encrypt the hash value to generate a digital signature and transmit it to the receiver; third, the receiver Use the sender's public key to decrypt the digital signature generated in the second step, perform reverse calculation to obtain the hash value generated in the first step, use the same Hash algorithm to calculate the data, and obtain another hash value. Compare the two values. If they are the same, It means that the data is signed by the sender and sent to the receiver. Otherwise, it is not the data sent by the sender and cannot be trusted.

#### Private key signature
Private key signature uses the private key of the asymmetric encryption algorithm to encrypt the original data. It is a signature of the entire message and is suitable for small file information.
 
  First, the sender encrypts the data with its own private key, generates a digital signature, and then bundles the original data with the generated digital signature and transmits it to the receiver, because the receiver has the matching public key that the sender has disclosed to the outside world. , use this public key to decrypt the received information, and then compare the decrypted data with the original data in the bundle, thereby proving that the data received by the receiver is indeed provided by the sender it claims to be.


#### Digital envelope

  The sender encrypts the data using a symmetric key, and then encrypts the symmetric key using the recipient's public key, producing a digital envelope that is sent to the recipient. Because the matching public-private key pair corresponds to a fixed user's digital envelope, only the designated recipient can open the digital envelope and use the obtained key pair to decrypt the digital envelope and obtain the original data.

Digital envelopes offer very high security. The first is the packaging of digital envelopes, using the recipient's public key to encrypt the information to be transmitted, and the information can only be restored with the recipient's private key; the second is the disassembly of digital envelopes, that is, using the private key to encrypt the encrypted data Decrypt.

Digital envelopes ensure the authenticity and integrity of transmitted data. Because the function of a digital envelope is close to that of an ordinary envelope used in life, it uses password encryption technology to protect data, stipulating that the designated recipient can decrypt the data and obtain the original data.

The digital envelope combines the efficiency and security of symmetric key encryption technology to overcome the complexity of the key issuance process, and combines the flexibility of asymmetric key encryption technology to avoid the long time required to encrypt data. , to ensure the integrity, authenticity and efficiency of data transmission.

### PKI-based digital certificate identity authentication system

#### Composition of PKI system

PKI uses public key technology and digital certificates to establish a security domain. Within this environment, PKI is mainly responsible for managing encryption keys, including key update and recovery, and for issuing digital certificates, including certificate generation, update, and revocation. If the PKI system needs to establish an interconnected trust relationship with other security domains, the connection can be established through cross-certification and other forms.
 
PKI combines hardware systems, software systems and security policies to form a complete security mechanism. No matter where the sender is or what his identity is, the certificate is the most fundamental basis of trust. On this basis, the two parties conduct various communication activities.

The PKI system consists of certification authority CA, registration authority RA, digital certificate library, key backup and recovery system, certificate revocation system, key update mechanism, etc.

![enter image description here](https://images.gitbook.cn/18f163f0-4b84-11e9-96f1-356961e976e6)

Certification authority CA: It is the issuing authority of digital certificates and the core of the PKI system. It is an authoritative and impartial third-party organization. The certification authority CA first confirms the identity of the applicant who applies for the certificate, and then bundles the subject of the certificate to be issued with the public key to generate a digital certificate, thereby establishing a corresponding relationship between the applicant and a pair of public and private keys.

Registration Authority RA: It is responsible for collecting user applications and verifying the user's true identity. Users who meet the conditions for issuing certificates can be issued a digital certificate, otherwise they will not be able to obtain a digital certificate.

Digital certificate library: Centrally stores issued certificates and public keys. Users can easily query other certificates and other related information in the certificate library. The digital certificate library is stored in a directory server, relational database, etc. Typically an LDAP directory is used.

Key backup and recovery system: It is the core of the key management system. If the user accidentally loses the decryption key of the data, the once-encrypted data cannot be decrypted. This system can solve such problems. When the digital certificate is generated, the certification authority CA backs up the encryption key and stores it in the digital certificate library. When the user needs to retrieve the key due to loss of the key or other reasons, he or she can apply to the certification authority CA. The CA recovers the key for the user.

Certificate revocation system: Because the user has lost the key, or the user's identity has changed, and the certificate has expired, the certificate must be updated accordingly, a new certificate must be generated, and the old certificate must be revoked. As an indispensable part of the PKI system, the certificate revocation processing system requires the PKI system to provide a complete set of management mechanisms for the certificate revocation system. After the certificate is generated, the PKI system will automatically check whether the certificate exceeds the validity period and automatically renew the certificate every time. Before expiration, the CA will start the update process, generate a new certificate, and then revoke the expired certificate.

Application interface (API): The PKI system provides users with secure services such as communication and usage. It also has very high security requirements for application interfaces. A high-performance application interface system can meet the realization of various functions of the PKI system, such as user query for certificates, some information related to the revocation of certificates, etc. The application interface system can ensure that the PKI system and other functions are safe and reliable. Various applications run well.

The PKI system mainly provides three main security services: authentication, integrity and confidentiality.

  Authentication - Confirmation to one entity that another entity is indeed itself.

Integrity – Assuring an entity that data has not been modified intentionally or unintentionally.

Confidentiality – Assurance to an entity that only the recipient, and no one else, can decrypt critical portions of the data.

The PKI system must provide users with secure and transparent services. Users do not need to consider how certificates in the PKI system are generated, updated, revoked, and restored, or how keys are managed, as long as users can easily obtain digital signatures.

 
### CA Certificate

#### CA Overview

Certification Center CA is an authoritative, trustworthy and impartial third-party organization that is responsible for generating, issuing and managing digital certificates, and providing security services for users participating in online transactions and other activities. The digital certificate issued by the certification center CA includes the user's name and other identity-related information, and this information corresponds one-to-one with the public key in the digital certificate library. When the user applies to the registration center RA, his identity and other related information After the review, the CA issues a certificate to the user, thereby establishing a legal connection between the user who owns the digital certificate and the user's public and private keys, information about the user's identity, and the digital certificate center. The authenticity of the user and the digital certificate are consistent.

CA is a key component of the PKI system, issuing and managing digital certificates for various applications to users. The main functions of the certification center CA include certificate application, approval, issuance, query, update and revocation, and management of revoked certificate lists.

The components of CA and the main functions of each part:

![enter image description here](https://images.gitbook.cn/85244b80-4b86-11e9-8269-8dda0475a431)

**Certificate Issuing System**

The system's private key and encryption algorithm are used to bundle the personal information provided by the user when applying and the user's public key into the digital certificate to be issued.
     
**Key Management System**
 
It is responsible for the generation, storage, revocation, recovery, update and query of keys.
    
**Registration Audit System**
 
When a user makes a request to the certification center for issuance or restoration of a digital certificate, the registration audit system is responsible for registering and reviewing the user's relevant identity information, reviewing and submitting the user's request, and providing certificate management statistical functions.

**Certificate CRL Publishing System**
  
The certificate CRL publishing system is responsible for publishing the information of the certification center CA, and the external publishing time is at a fixed interval.

#### CA Trust Model

It is a model that establishes trust relationships between users in different PKI domains, implements mutual authentication, and establishes trust paths between each user. The PKI trust model is the primary issue in establishing a PKI system. The PKI trust model can effectively solve the problem of where the user's trust starts and how this trust is transferred in the PKI system.

The trust model of the same PKI system will have different construction plans due to different CA architectures.

There are five types of trust models in PKI.

Strict hierarchical trust model. All nodes in the model trust the unique root CA. Each node must save the public key of the root CA center. There is only one trust path from the root CA to the certification node. When users need to communicate, the public key certificates of both parties must first be verified through the root CA. Such a trust model is suitable for independent, hierarchical enterprise applications and is difficult to use between enterprises in different organizations. The advantage is that the certificate path is one-way, short, and easy to expand. The disadvantage is that if the root CA fails, the entire trust model will be destroyed, and there is currently no good technology to solve this problem.

![enter image description here](https://images.gitbook.cn/9cce2ba0-4b8d-11e9-8269-8dda0475a431)

Mesh trust model. There are many CAs in the trust model. Any CA has the right to certify other CAs, and any two CAs can certify each other. The mesh trust model is suitable for communication organizations without hierarchical relationships or dynamic changes. However, it may not be suitable for a specific CA to certify a certain CA, and there may be many trust paths between two CAs, so building trust Paths are more complex than hierarchical models, and optimization measures need to be applied when building trust paths. The CAs in the mesh trust model are all independent and have no levels. There is no root CA. When the demand for trust transfer increases, multiple CAs can be added at any time to increase the number of trust paths through cross-certification relationships. . The advantage is that each root CA is independent, the security of a certain root CA is destroyed will not affect the mutual trust of other root CAs, and the mutual authentication path is flexible and changeable. The disadvantage is that the certification path from the user end to the root CA is uncertain, and there are many alternative paths, so addressing is relatively difficult. After choosing a correct path, abandon other alternative paths, and sometimes you may fall into an endless circular addressing path.

![enter image description here](https://images.gitbook.cn/a6432140-4b8d-11e9-8269-8dda0475a431)
The hybrid trust model combines hierarchical and network trust models. In this trust model, each hierarchy has a root CA. Cross-certification must be established between any two root CAs, and there is a corresponding cross-certificate for mutual authentication between the two hierarchies.

![enter image description here](https://images.gitbook.cn/7a1bc3f0-4b8e-11e9-9703-f9a332732a5a)

If the cross-certification relationship between non-hierarchical root CAs is not complex, a simple certification path can be constructed between the two. However, in the hybrid trust model, every time a new domain is added, the number of cross-certifications established between domains increases by the order of square. When application entities need to expand domains on a large scale, the number of cross-certification certificates established between root CAs will increase. Cross-certifications will continue to grow in size and complexity.

Trust list model, this model provides the public key of a trusted root CA to the client system, and the authentication certificate is directly or indirectly connected to the trusted root CA. Examples of the application of this model are the various certificates used to download applications in the browser we use. this modelThe advantage is that the interoperation steps are simple and convenient, but there are many security issues that cannot be ignored. To give a common example, the browser we use will install some public keys of trusted root CAs in advance, and users will default to these public keys. All are trusted, but if one of the root CAs is this secure, the entire browser's security will be compromised. When the security of a root CA's public key has been compromised, or the private key corresponding to the root CA's public key has been leaked, we cannot prevent tens of thousands of browsers from revoking the compromised root CA. of the key.

![enter image description here](https://images.gitbook.cn/4b92f700-4b8f-11e9-9703-f9a332732a5a)

#### Functions of CA

Verify the applicant's identity. When a certificate applicant submits a registration application containing relevant information such as its true identity, the purpose and use of the certificate, etc. to the certification center CA, the CA is responsible for reviewing the applicant's registration information and confirming the authenticity and reliability of his or her identity.

Ensure the security of issued private keys. The private key issued by the certification center CA must be generated by hardware, not simply by software. At the same time, in order to improve the security of the private key, the length of the private key should be as long as possible to reduce the risk of being deciphered, and the private key is not prohibited. Transmission over the network or storage in computer memory must be stored on independent media.

Manage certificates. It is guaranteed that the name, serial number, and CA ID of the issued certificate correspond to each certificate and are unique, and there will be no duplication of CA IDs and certificate serial numbers. Check the validity period of certificates at fixed intervals, update expired certificates in a timely manner, and revoke invalidated certificates.

Publish a list of revoked certificates. Maintain a list of invalidated certificates, provide users with online query services, and prevent security issues in transactions. Monitor the issued certificates throughout the process and record the log of each certificate as a basis for arbitration in case of transaction disputes.
 
The key is generated in the secure and trustworthy hardware device of the certification center CA and stored in an independent key store. The user's private key is also stored in a specific independent storage device. The key will not appear on the network. , but appears in the certificate as ciphertext.

#### User identity authentication process

The user submits personal information including the user's name, ID number, contact number and other personal information to the registration agency RA. RA will review the authenticity of the user information and determine whether the reason for the user's application for registration meets the review conditions. After passing the review, RA will submit the personal information. To the certification center CA, the certification center CA determines that the identity of the applying user complies with its security policy. The CA applies to the key management device to generate the user's public key and private key. The generated public key and private key are stored in the key database for After the user loses the certificate, the key is restored. The CA issues a certificate to the user, and the user's private key is encapsulated in a digital certificate carrier, such as a USB Key device.

After the user obtains the digital certificate, it can be used in systems trusted by the identity authentication center CA. First, the CA issues certificates for its trusted application systems, and then installs the CA's client on the user end. When the user makes an access request to the application system, the client transmits the user certificate information to the CA's authentication module, and the system determines the user's Whether the digital certificate and the system's certificate are issued by the same certification center CA? If they are issued by the same CA, the authentication module generates a random number M as a "challenge" and transmits M to the client; the client uses The user's private key digitally signs the random number M. The result of the digital signature is A. The user submits A to the authentication module; the authentication module queries the user's digital certificate in the LDAP directory and obtains the public key in the digital certificate. , use the public key to decrypt the digital signature M sent from the user end, and the result is m, which is the random number M generated by the authentication module for the user. If M is equal to m, it proves that the user's identity authentication is successful and the user can access e-government affairs. system; otherwise, the user is an illegal user and is denied access to the system.

### Summary

With the rapid development of electronic information technology, information security issues have attracted people's attention. PKI technology can provide a variety of security services based on the needs of multiple computer users, thereby ensuring the authenticity, integrity, and confidentiality of computers in specific application processes. Advantages in many aspects such as sex can be guaranteed, promote the development of computer technology, and enable it to better serve people. Most of the currently popular blockchain projects use PKI technology to authenticate users, such as Hyperledger Fabric, SimpleChain, ImcoreChain, etc. The following is a design diagram of a very common blockchain project architecture.

![enter image description here](https://images.gitbook.cn/88eb2970-4b84-11e9-9703-f9a332732a5a)

We all know that CA is the core of PKI. The CA in the picture above is actually an authoritative certificate service center service built using the PKI system.
