[![Chinese](https://img.shields.io/badge/Chinese-README-red)](README.md)


## Confused circuit

### 1. Development status of confusion circuits

1982: Yao Qizhi proposed confusion circuit. At this time, confusion circuit recognized two-party calculation.

2009: Lindell et al. gave safety proof and detailed introduction

2013: Goldwasser gave a simplified form


### 2. Confusion circuit

Early MPC protocols were based on circuit models, the most typical of which was the confused circuit protocol. Obfuscation circuit is a two-party secure calculation method, which was first proposed by Mr. Yao Qizhi. For this reason, he also raised the classic millionaire problem: compare who is richer without revealing any assets between the two parties. The two parties involved are the circuit generator and the circuit executor. First, both parties reach an agreement to convert the joint function to be executed into a Boolean circuit. Typically, the generator uses a symmetric encryption algorithm (AES, etc.) to encrypt each gate. For the possible input (output) values of each line on the circuit, the generator selects an equal number of random numbers to replace them one by one. These random numbers are called confusion keys. The generator then uses these obfuscation keys to encrypt the obfuscation key output of each gate in the circuit to obtain the truth table of the obfuscation circuit.

| X | Y | Z |
|:----|:---|:----|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

Taking a simple AND gate circuit as an example, assuming there are inputs x, y, and the output is z, then there is a truth table:

First of all, x and y cannot be made public (nor can they all be sent to the executor). They can be represented by random numbers. What the executor gets is the relevant information about z. The information of z cannot be fully disclosed. If the result of z is replaced by simple coding, the input information of z can be easily deduced. Therefore, the four results of z in the truth table need to use different representations, or Using random numbers, at the same time, the random number of z can be solved by a certain group of xy, so the corresponding xy can be used to encrypt z. The whole process is the process of generating the obfuscated truth table, and the final obfuscated truth table is:

.：
     ![.：
](https://github.com/guoshijiang/cryptography/blob/master/img/121.png)


The generator scrambles the z-order of the confusing truth table and sends it to the executor along with its own input random number (note: the premise is that the generator and the executor jointly agree on the execution circuit), and the executor starts executing the circuit after receiving the message. Generally, after the generator provides its own x input, the executor can solve z by choosing its own input between If you don’t want the generator to know which one you have chosen, then the OT protocol comes into play. The confusion circuit uses the OT protocol to solve this problem. Finally, the executor uses the x input provided by the generator and its own input to decrypt z in sequence. The successfully decrypted z is the final result (note: there is only one result, and it is only the obfuscated key of z that is obtained by decryption). The executor then sends the result, that is, the obfuscated key, to the generator, and the generator sends the output result of the real z corresponding to the key to the executor according to the truth table. At this point, both parties have completed a confusion circuit calculation.

The premise of confusing the circuit is that both parties need to agree on the execution circuit in advance, and both parties can honestly send the results to the other party. This is a semi-honest model. The original obfuscated circuit protocol can resist semi-honest attacks, and after many subsequent improvements and optimizations, it can also resist completely malicious attacks. In the actual application process, there are also performance issues in the representation of complex operational logic and circuit generation calculations.

### 3.GMW Agreement

The GMW protocol was proposed by Goldreich et al. It is based on Garbled Circuit and supports a multi-party semi-honest secure computing protocol. The difference from the previously mentioned Yao's confusion circuit estimation scheme is that the GMW confusion circuit estimation scheme does not require the use of a confusion truth table, so there is no table lookup and encryption and decryption operations caused by the confusion truth table, saving money. It requires a very large amount of calculation and communication. The obfuscation circuit has been introduced in the last popular science. After converting the objective function of secure multi-party computation into a Boolean circuit, the obfuscation circuit is obtained by performing obfuscation (encryption) operation on the circuit. The obfuscation circuit conceals the circuit input and circuit structure by performing obfuscation (encryption) operations on the circuit, thereby achieving confidentiality of the private information of each participant, and then uses circuit calculation to achieve the calculation of the objective function of secure multi-party computation.

The objective function of the GMW protocol consists of XOR gates, AND gates, and NOT gates. The output value of the NOT gate is the inverse of the input value. If the input is 1, the output is 0. Otherwise, if the input is 0, the output is 1.

The truth table of the AND gate is shown below:

.：
     ![.：
](https://github.com/guoshijiang/cryptography/blob/master/img/new_gmw1.jpg)


The XOR gate and its truth table are shown in the figure below:

.：
     ![.：
](https://github.com/guoshijiang/cryptography/blob/master/img/new_gmw2.png)


The algorithm flow is as follows:



### 4.BGW Agreement

The BGW protocol is also a secure computing protocol that supports multiple parties. The BGW protocol is based on the Shamir(t, n) threshold secret sharing mechanism and takes advantage of the additive homomorphism and multiplication homomorphism properties of the Shamir secret sharing mechanism.

Assume that there are n participants in the BGW protocol. Assume that participant Pi needs to enter a secret. Then participant Pi first uses the Shamir(t,n) threshold secret sharing mechanism to share the secret with all other participants. The threshold t is selected according to the specific Determined by the security requirements of the usage scenario.

When the inputs of all participants are shared through the Shamir(t, n) threshold secret sharing mechanism, each participant masters the sub-secret of the protocol input. Assume that the inputs of a gate are a and b respectively, and the secrets ai and bi have been given by the secret assignment function

.：
     ![.：
](https://github.com/guoshijiang/cryptography/blob/master/img/bgw1.png)

The allocation is completed, fa(0) = a, fb(0) = b, and participant Pi masters the sub-secrets ai and bi of a and b. On a Boolean circuit, the XOR gate and the AND gate can be regarded as addition and multiplication on the finite field F2, respectively. Compute XOR with addition modulo 2 and with multiplication modulo 2.

.：
     ![.：
](https://github.com/guoshijiang/cryptography/blob/master/img/bgw2.jpg)


For XOR gates: Since Shamir has additive homomorphism, then

.：
     ![.：
](https://github.com/guoshijiang/cryptography/blob/master/img/bgw3.jpg)

Suppose ci = ai ai xor bi. When all calculations are completed, each participant Pi publishes its calculated c(i), and c(x) and c(0) can be recovered.

.：
     ![.：
](https://github.com/guoshijiang/cryptography/blob/master/img/bgw4.jpg)


For the AND gate, it is the same as the previously described multi-party multiplication calculation based on the Shamir(t, n) threshold sharing mechanism, except that the BGW is on the finite field F2. Each participant Pi calculates ai * bi, and then each Pi independently selects a random polynomial hi(x) of degree t, and satisfies hi(x) = di,1 ≤ t ≤ n, t < n / 2. Allocate di to each participant, and cij = hi(x). After the allocation of all participants, Pi has mastered the information c1i, c2i...cni, and at the same time uses the public reorganization vector 1,...n,

Pi calculation:

.：
     ![.：
](https://github.com/guoshijiang/cryptography/blob/master/img/bgw5.jpeg)

At this time, the sub-secret ci mastered by Pi is the sub-secret of c. When all calculations are completed, each participant discloses his or her own sub-secret, and then can be obtained according to the Shamir(t, n) threshold secret reconstruction algorithm described previously.

### 5.CCD protocol


### 6. Summary

After development in recent years, the MPC protocol system no longer uses strict circuit representation, but uses a hybrid model. In the hybrid model, functions are compiled into a set of optimized sub-protocol functions for common operations. This set of primitives can include traditional circuit-based protocol models and can be seamlessly described in a single protocol. Mixed model systems typically represent intermediate values as key sharing over a large finite field. They can use a mixture of information theory and cryptographic protocols, and therefore differ in both the number of computational parties and the threat model.

Hybrid models allow for very different performance characteristics compared to strictly circuit-based models. For example, in finite fields, operations such as comparisons, shifts, and equality tests are expensive to represent as arithmetic circuits. However, the dedicated subprotocol that operates key sharing is very efficient at sharing the results of computations.
