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