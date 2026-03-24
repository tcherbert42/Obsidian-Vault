________
03-23-2026 | 01:13
Status: #school 
Tags: #Cryptography #CS-4575 

# Module 6: Asymmetric Cryptography & RSA
## RSA Key Generation Architecture
**Step 1**: Select two large, distinct primes $p$ and $q$.
**Step 2**: Compute the modulus $n = p * q$. (Published openly)
**Step 3**: Compute the totient $\Phi(n) = (p-1)(q-1)$. (The secret trapdoor).
**Step 4**: Choose a public exponent $e$ (typically 65,537) that is coprime to $\Phi(n)$.
**Step 5**: Compute the private exponent $d$ using the Extended Euclidian Algorithm such that $e * d$ 


> [!WARN] Warning: 
> Never use Textbook RSA in production.
### The Fatal Flaws of Textbook RSA
**Deterministic Encryption**
- Encrypting the same plaintext with the same public key always yields the same ciphertext. This fatally violates IND-CPA security. 
**Multiplicative Homomorphism** 
- Attackers can manipulate intercepted ciphertext mathematically. 

### Optimal Asymmetric Encryption Padding (OAEP)
The Fix: OAEP transforms RSA into a probabilistic, IND-CCA2 secure scheme.

**Feistel-Inspired Masking**: Uses a structure requiring two hash functions to pad the message prior to exponentiation. 

## Flipping the Script: Digital Signatures (origin integrity)
Encryption in Reverse

**Signing**: The sender encrypts a hash of the message with their private key: $\sigma = h^d$ mod $n$.
+private key
**Verification**: Anyone decrypts the signature with the public key to verify the hash: $h'=\sigma^e$ mod $n$.

