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
>- Strent