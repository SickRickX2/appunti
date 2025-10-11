## Symmetric Encryption
The universal technique for providing confidentiality for transmitted or stored data. It s also known as *conventional encryption* or *single key encryption*.
Two requirements for secure use:
- need a **strong** encryption **algorithm**
- sender and receiver must have obtained copies of the secret key in a secure fashion and must keep the key **secure**
### Attacking Symmetric Encryption
>[!note] Cryptanalytic Attacks
>- Rely on:
>	- nature of algorithm
>	- some knowledge of the general charateristichs of the plaintext
>	- some sample plaintext-cyphertext pairs
>Exploits the charateristics of the algorithm to attempt to deduce a specific plaintext or the key being used for that data. If it's succesfull all future and past messages encrypted with that key are compromised.

>[!tip] Brute-force Attacks
>It consists in trying all possible keys on some ciphertext until an intelligible translation into plaintext is obtained.
>- on average half of all possible keys must be tried to achieve success

#### Most known symmetric encryption algorithms
- **AES**: *Advanced Encryption Standard* (also known as Rijndael). It's the most popular and widely used symmetric encryption algorithm in the modern IT industry
- **DES**: *Data Encryption Standard* (now considered insecure)
- **RC4**: (also known as ARC4 or ARCFOUR, now considered insecure)

>[!note] DES
>Before AES it was the most widely used ecnryption scheme
>- Strength concerns:
>	- Concerns about the algorithm itself
>		- DES is the most studied encryption algorithm in existence
>	- Concerns about the use of a 56-bit key
>		- The speed of commercial off-the-shelf processors makes this key length woefully inadequate

>[!tip] Triple DES (3DES)
>Repeats basic DES algorithm three times using either two or three unique keys.
>First standardized for use in financial applications.
>**Attractions:** 
>- 168-bit key length overcomes the vulnerability to brute-force attack of DES 
>- Underlying encryption algorithm is the same as in DES
>
>**Drawbacks:**
>- Algorithm is sluggish in software 
>- Uses a 64-bit block size

>[!note] Advanced Encryption Standard (AES)
>Needed a replacement for 3DES because was not reasonable for a long term use. 
>It has:
>- Better security strength than 3DES
>- Significantly improved efficiency
>- Symmetric block cipher

### Practical Security Issues
Tipically symmetric encryption is applied to a unit of data larger than a single 64 bit or 128bit block.
*Electronic codebook (ECB)* mode is the simplest approach to multiple block encryption:
- each blocm of plaintext is encrypted using the same key
- cryptanalysts may be able to exploit regularities in the plaintext
Modes of operation:
- alternative techinques developed to increase the security of symmetric block encryption for large squences
- overcomes the weakness of ECB
## Block vs Stream Ciphers
**Block Cipeher**
- Processes the input one block of elements per time
- Produces an output block for each input block
- Can reuse keys
- More common
**Stream Cipher**
- Processes the input elements continuously
- Produces output one element at a time
- Primary advantage is that they are almost always faster and use far less code
- Encrypts plaintext one byte at a time
- Pseudorandom stream is one that is unpredictable without knowledge of the input key

## Message authentication

>[!note] Message Authentication
>- Protects against active attacks
>- Verifies received message is authentic 
>- Can use conventional encryption

Message encryption by itself does not provide a secure form of authentication. We can combine authentication and confidentiality in a single algorithm.
- Encryption + authentication tag
Typically message authentication is separate from message encryption.
Some examples for message authentication without confidentiality:
- Applications in which the same message is broadcast to a number of destinations
- An exchange in which one side has a heavy load and cannot afford the time to decrypt all incoming messages
- Authentication of a computer program in plaintext
Authentication and encryption combine for meeting security requirements

>[!note] Message Authentication Code (MAC)
>A number of algorithms could be used to generate the code. However, authentication algorithm need to not be reversible.

### Cryptographic hash function
The purpose of an hash function is to produce a "fingerprint" of a file, message, or other block of data. It generates a set of l bits from a set of L(>=k) bits (in general $\to$ non necessarily non-injective)
The result of applying a hash function is called **hash value** or message digest, or checksum.

>[!note] MAC with one way hash functions
>Unlike the MAC, a hash function does not take secret key as input. However, it is possible to get MACs using hash functions.
>**The public key approach advantages:**
>- it provides a digital signature as well as message authentication
>- it does not require the distribution of keys to communicating parties
>
>![[Pasted image 20251011135038.png|500]]

### Properties for a hash function aimed at authentication
1) Can be applied to a block of data of any size
2) Produces a fixed-length output
3) H(x) is relatively easy to compute for any given x
4) One-way or pre-image resistant
5) Computationally infeasible to find y != x such that H(y)= H(x)
6) Collision resistant or strong collision resistance

### Security of Hash Functions
There are two approaches to attacking a secure hash function:
- exploit logical waknesses in the algorithm
- strength of hash function depends solely on the length of the hash code produced by the algorithm
SHA most widely used hash algorithm.
Additional secure hash function applications:
- hash of password is stored by an operating system
- store H(F) for each file on a system and secure the hash values
### Public-Key Encryption Structure
Publicly proposed by Diffie and Hellman in 1976.
Based on mathematical functions.
- Asymmetric:
	- Uses two separate keys:
		- **public key** made public for others to use
		- **private key**
Some form of protocol is needed for distribution.

In broad terms, we can classify the use of public-key cryptosystems into three categories:
- *digital signature*
- *symmetric key distribution*
- *encryption of secret keys*
### Asymmetric Encryption Algorithms
- *RSA*: Most widely accepted and implemented approach to public-key encryption. Block cipher in which the plaintext and ciphertext are integers between 0 and $n-1$ for some $n$.
- *Diffie-Hellman key exchange algorithm*: Enables two parties to securely reach agreement about a hsared secret for subsequent symmetric encryption of messages. Limited to the exchange of the keys. 
- *DIgital Signature Standard (DSS)*: Provides only a digital signature function with SHA-1. Cannot be used for encryption or key exchange.
- *Elliptic curve cryptography* : security like RSA, but with much smaller keys.
A digital signature is a data-dependent bit pattern, generated by an agesnt as a function of a file, message, or other form of a data block.
**FIPS 186-4** specifies the use of one of three digital signature algorithms:
- *Digital Signature Algorithm (DSA)*
- *RSA Digital Signature Algorithm*
- *Elliptic Curve Digital Signature Algorithm (ECDSA)*
![[Pasted image 20251011174854.png]]
![[Pasted image 20251011174912.png]]
![[Pasted image 20251011174941.png]]

## Random Numbers
Uses include the generation of
- Keys for public-key algorithms
- Stream key for symmetric stream cipher
- Symmetric key for use as temporary session key or in creating a digital envelope
- Handshaking to prevent replay attacaks
- Session key
### Random numbers requirements
- Randomness
- $\to$ Unifrom distribution
	- Frequency of occurrence of each of the numbers should be approximately the same
- $\to$ Indipendnce
	- No one value in the sequence can be inferred from others
- Unpredictability
- $\to$ Each number is statistically indipendent of pther numbers in the sequence
- $\to$ Opponent should not be able to predict future elements of the sequence on the basis of earlier elements
>[!tip] Random vs Pseudorandom
>Cryptographic apllications typically make us of algorithmic techniques for random number generation. Algorithms are **determiin**