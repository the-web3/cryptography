[![Chinese](https://img.shields.io/badge/Chinese-README-red)](README.md)

## MPC Brief Description

Multi-party secure computing was first proposed by Professor Yao Qizhi of my country in 1982. Its main research problem is how to design a function without a trusted third party that allows multiple parties to safely obtain output without revealing any information. The composition of multi-party secure computation makes use of a lot of cryptographic knowledge, such as zero-knowledge proofs, digital signatures, etc., as well as distributed computing principles, such as broadcast problems and Byzantine problems. However, there are big differences between multi-party secure computing and traditional cryptography and distributed computing. Traditional cryptography achieves data protection through encryption in a non-secure environment. The encryption mechanism is to transform the original information according to certain rules. Even if the data is tampered with or leaked during the transmission process, it can be discovered in time and can be remedied in time without worrying about the data being exploited. Cryptography protects the privacy of the data of the participants under attack by the attacker. The problem of multi-party secure computing research is how to protect and ensure the accuracy of the data of each data participant. Different from distributed computing, multi-party secure computing controls the computing process through protocols. There is no third party to control the computing process. All participants have equal status and there is no third party intervention.

In order to design secure multi-party computation (MPC) protocols, many studies have been conducted, such as inadvertent transmission, obfuscated circuits, homomorphic encryption and linear secret sharing schemes. Secure MPC provides enhanced privacy, correctness and input independence, and guaranteed output delivery. Blockchain is well suited for secure MPC protocols as they both deal with security and trust issues in a distributed environment. There are many practical scenarios that benefit from blockchain-based secure MPC, such as MPC cross-chain bridge and MPC distributed wallet.

Multi-party secure computing was early used in scenarios such as electronic elections, threshold signatures, and electronic auctions. With the deepening of research, it has been expanded to collaborative computing for distributed scenarios, including private information query, computational prediction, federated machine learning, etc., and has broad application prospects in government affairs, medical care, finance and other fields. For example, in August 2019, Google (google) open sourced a multi-party secure computing tool - Private Join and Compute, to help organizations and institutions collaboratively process confidential data sets; in October 2019, Facebook (facebook, meta) will use secure machine learning to The framework cryptoTen is open source. Relevant institutions and organizations in my country actively promote the research and development of multi-party secure computing core technologies, the formulation of standards and specifications, and the implementation of commercial applications. For example, Ant Financial launched the Ant Chain Moss multi-party secure computing platform; Huakong Qingjiao implemented a high-performance and general secure computing framework PrivPy platform based on multi-party secure computing technology; Matrix Element launched the privacy machine learning open source framework Rosetta.


### 1. A brief history of the development of secure multi-party computation

1981: Michael O. Rabin proposed the concept of inadvertent transmission

1982: Yao Qizhi proposed a two-party data comparison millionaire problem and published the text of the secure computing protocol, but it only stopped at two parties.

1987: O.Goldreich, S.Mical and A.wigderson proposed a cryptographically secure secure multi-party computation protocol that can calculate any function by analyzing any kind of psychological game.

1998: O.Goldreich systematically summarized the research on secure multi-party computation and published a monograph on secure multi-party computation.

2008: Ivam Damgard and others proposed the first secure multi-party computing protocol at the US Secret Conference

2015: Tal Moran theoretically addresses the problem of topological privacy in secure multiparty computation. This theory was described by Hinkelmann and Jakoby

2019: Google and Facebook both open sourced the secure multi-party computing framework. In the same year, Binance in our currency circle also open sourced the threshold signature library tss-lib to help the development of the MPC industry in the currency circle.

### 2. The concept of multi-party secure computing

Mathematical definition of multi-party secure computing: Assume there are n participants P1, P2...Pn, each participant has a private input data Xi, and all participants jointly calculate a certain function f(x1, x2...xn) , and it is required that at the end of the calculation, each participant Pi can only obtain the output of the private input data Xi, but cannot obtain the input information and output result information of other participants.

The multi-party secure computing theory mainly solves the problem of information protection and calculation correctness of each data participant. It can ensure the correctness of calculation without a third party and protect the data from leakage. Therefore, the multi-party secure computing theory Features include:

#### 1. Enter privacy

When performing computing tasks, multi-party secure computing queries the data locally based on the calculations of the MPC nodes, and then performs data calculations based on the computing tasks. During the entire process, the data is saved in the local database, and there is no data leakage problem, thus ensuring that the input data is privacy.

#### 2. Calculation correctness

Multi-party secure computing data participants perform task calculations according to the agreement, and perform calculation data query and collaborative calculation through the multi-party secure computing protocol, so the correctness of the calculation can be guaranteed.

#### 3. Decentralization

There are no privileged participants or trusted third parties in multi-party secure computing. Instead, a protocol is used to replace the third party. The protocol ensures that all data participants have equal status and power, and any data owner can start computing tasks.

### 3. Secure multi-party computation model

The composition model of multi-party security computing mainly consists of four parts: protocol participants, protocol attackers, network conditions and communication channels.

#### 1. Agreement participants

According to the behavior of the protocol participants during the execution of the protocol, the protocol participants can be divided into

- Honest protocol participants: This type of participant is the most ideal protocol participant. They execute each step according to the protocol according to the agreed process when computing the task.
- Semi-honest protocol participants: This type of participant does not follow every step of the protocol like honest participants. It privately collects the required data based on the actual situation and deduce the input data and input values ​​of other participants, but does not Actively attack or unite with other data participants to destroy the protocol. Such participants are generally difficult to detect because they do not actively attack or unite with other participants. This has a great impact on the security of the protocol. Once semi-honest participants are bribed or If it is breached, the data collected will be leaked.
- Malicious participants. Such participants can easily be bribed by attackers, or they can be disguised as participants by attackers to illegally obtain useful data.

In real situations, there are mainly semi-honest protocol participants and malicious participants, so a semi-honest model and a malicious adversary model are designed.

Semi-honest model: When the protocol is executed, participants follow the process specified in the protocol, but malicious attackers may monitor and obtain the input and output of the participants during the execution of the protocol and the information obtained during the running of the protocol.
Malicious adversary model: During the execution of the protocol, the attacker can analyze the private information of honest participants by making illegal inputs through participants under his control, or maliciously tampering with inputs. Termination of the agreement can also be caused by early termination and refusal to participate.

#### 2. Protocol attacker

Protocol attackers and protocol malicious participants have the same purpose in participating in collaborative computing, which is to obtain data through illegal means. Different from the behavior of malicious participants, it can control participants and tamper with the steps of protocol participants, allowing participants to continue executing the protocol to obtain information as they wish.

The attacker's control over dishonest participants can be divided into the following two situations:
- Passive attack/eavesdropper: Only eavesdrops on the channel or obtains the information obtained by dishonest participants during the collaborative calculation process. The dishonest participants still execute the protocol steps according to the agreement.
- Active attacker: The attacker will change the behavior of dishonest participants, not only eavesdrop or obtain the information obtained by dishonest participants during the protocol, but also make them participate in the protocol according to their own wishes to achieve the purpose of stealing information.

#### 3. Network conditions

Data owners of multi-party secure computing need to be connected through network media when performing collaborative computing tasks. In a synchronous network media, all data participants will share the same global clock, and all information will be stored in the same Delivered within the time period, and each data participant can receive their own data information within the next time period.

However, in an asynchronous network medium, all data participants cannot have the same global clock. Information is sent from the local database of a data participant, and it takes several periods of time before the recipient of the data participant can receive it. to your own data information, and since the data information received comes from different participants, the order of the data information received may not be the actual order of sending.

#### 4. Communication channel

The network medium between participants in secure multi-party computation requires channel connection to complete data exchange with other participants. Since protocol attackers will have a certain degree of control over dishonest protocol participants, the communication channel is divided into 3 levels

- Secure channel, non-secure channel, and unauthenticated channel. The attacker has no control over the secure channel; on the non-secure channel, he can eavesdrop on the communication information of the participants, but cannot tamper with the content; on the unauthenticated channel, he can have complete control and even disguise himself as Honest participants participate in the protocol.

### 4. Cryptographic protocols involved in the secure multi-party computation group

Message digests, symmetric and asymmetric encryption, secret sharing, certificates, oblivious transmission and obfuscated circuits, etc.

### 5. Application scenarios of secure multi-party computation

#### 1. Government affairs application
The public sharing and data trading of government data can promote the common development of government departments and commercial institutions. However, the process of public exchange of data will lead to the leakage of government data and query information of commercial institutions. The use of multi-party secure computing technology can make the data always exist. In the local database of the government system, government data can be shared without leaking data. Multi-party secure computing provides a unified data standard for commercial organizations, which can realize information retrieval, query, data tracking and other functions in collaborative computing. It ensures the security and privacy of data and solves the problem of "data island".

#### 2. Financial applications

Marketing, risk control, anti-fraud, etc. in the financial field require institutions to form complete portraits of users to judge their creditworthiness. Therefore, cross-institutional collaboration is required to jointly create user portraits. Obtaining data across organizations requires obtaining data from multiple data structures, and then conducting data mining and analysis. However, the data acquisition process may lead to the leakage of data information, data being copied and pasted, and the ownership of the data owner being copied. Multi-party secure computing technology can realize calculations without data collection and sharing, protecting the privacy of target data owners and the security of data assets.

#### 3. Medical applications

For patients, medical data has certain sensitivity and privacy, which also results in medical data not being used to the maximum extent, making it difficult to exchange and share data among hospitals, pharmaceutical companies, and equipment suppliers. Utilize multi-party security technology to establish a unified, safe and trustworthy data exchange network among relatively closed medical data participants. All participants can obtain the data they need without leaking medical data. This enables effective use of medical data.

#### 4. Innovative applications

Multi-party secure computing technology can create more new applications when integrated with new technologies such as edge computing, blockchain, federated learning, and 5G. For example, joint credit reporting based on multi-party secure computing and blockchain technology can carry out credit inquiry business without a trusted central node to protect the business secrets and private data of each participant, which is helpful for solving the problems of multi-party lending and excessive credit granting. It is of great significance; such as the research on the "federated learning + blockchain" multi-party secure computing engine system, which can realize multi-party private data sharing, build a data ecosystem, break data islands, and mine the joint value of data, thereby realizing multi-party secure computing.

#### 5. Applications in the blockchain industry

MPC cross-chain bridge, multi-party secure custody wallet, asset protection

### 6. Summary

The research on multi-party secure computing technology is to solve the contradiction between data owners and data users. Data owners do not want to leak data resources, while data owners need correct calculation results. Under normal circumstances, the owner of data is also the user of other data, which requires data participants to coordinate calculations and get what they need. Multi-party secure computing adopts protocol standard solutions without third parties, allowing multiple participants to cooperate and complete calculations collaboratively. The data required for calculations are always saved in the local database throughout the calculation process, which ensures The privacy of the input data is ensured. All participants perform collaborative calculations and return their respective calculation results after the task is completed, ensuring the correctness of the calculation. Multi-party computing security is applicable to many fields such as government affairs, finance, and medical care, and can realize multiple functions such as data sharing and exchange, data query, data joint analysis, and data secure storage.