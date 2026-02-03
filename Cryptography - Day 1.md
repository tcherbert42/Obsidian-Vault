________
01-21-2026 | 01:38
Status: #school 
Tags: #Cryptography

# The **[[Cryptosystem Tuple]]**
Cryptography is a mathematical function mapping one set to another. The tuple **(P, C, K, E, D)**
- **P**: Set of **Plaintexts** (messages)
- **C**: Set of **Ciphertexts** 
- **K**: Set of **Keys**
- **E**: **[[Encryption Function]]** where E(P, K) -> C
- **D**: **[[Decryption Function]]** where D(C, K) -> B

##### Kerckhoff's Principle (1883)
-  **"The security of a cryptosystem must lie only in the secrecy of the Key, not the Algorithm"** 
- 'Security through obscurity' will **NOT** work. Hiding the source code is a proven failure mode. 

# Key Length $\neq$ Entropy
- A 256-bit key is *useless* if derived from a weak source. 
- Weakest link: Systems do not gracefully degrade; if entropy is low, security collapses. 
- Example: A 256-bit AES key derived from a 6-character password has only ~ 20 bits of actual entropy. 