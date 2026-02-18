________
02-02-2026 | 01:05
Status: #school 
Tags: #CS-4575 #Cryptography
# Module 2 - Symmetric Encryption 
The evolution of [[DES]] and [[AES]]

### Theoretical Foundations - The Shannon Paradigm
**Confusion**: Obscuring the relationship between the encryption key and ciphertext. 
- Implemented via **Non-linear Substitution** (S-boxes). 
**Diffusion**: Spreading the statistical structure of the plaintext across the ciphertext.
- Achieved via **Permutations** or linear transformations. 

## Data Encryption Standard (DES) History 
- Development: IBM developed the "Lucifer" cipher in the early 70's.
- NSA Intervention: The NSA insisted on two major changes before the standardization. 
- Key-Size: Reduced from 128 bits to **56 bits**.
	- They could only build equipment powerful enough to handle 56 bit decryption 
- S-box Design: Modified to strengthen the cipher against differential cryptanalysis.
- Standardization: Adopted as FIPS 46 in 1977.
- Legacy: Formally withdrawn by NIST in 2005.

##### DES Technical Architecture - The Feistel Network
- Structure: A 16-round Feistel Network (a 16 iteration loop)
- Block Size: 64-bit blocks
- Key Size: 56-bit effective key (+8 parity bits)
- Round Function: $f()$
- Expansion (E-box), Key mixing (XOR), Substitution (S-boxes), and Permutation (P-box)

## The Fall of DES and the Rise of 3DES
- Brute Force Reality: 1998: EFF's "Deep Crack" broke a DES key in 56 hours.
- 1999 Distributed efforts cracked a key in under 24 hours
- Triple DES (3DES): An interim solution using DES three times. 
- Mechanism:
	- Security: (112-bit (2-key) or 168-bit (3-key) effective security)
	- Limitation: 64-bit block size is vulnerable to collision attacks (e.g. Sweet32)

### The AES Competition (1997-2000)
- Objective: NIST sought a 128-bit block cipher with 128, 192, and 256-bit keys.
- Open Process: Unlike DES, the competition was global and transparent. 
- The Finalists:
	- Rijndael: Efficient, elegant, and flexible (The Winner).
	- Serpent: Highly secure, but slower.
	- Twofish: Flexible, key-dependent S-boxes.
	- RC6: High Performance on 32-bit CPUs. 
	- MARS: Complex, layered Feistel Structure. 

##### AES Architecture **Substitution-Permutation Network (SPN)**
- **SPN** Design: AES processes the entire 128-bit block (the State) in every round. 
- The State: A byte matrix.
- Round Transformations:
- SubBytes: Non-linear byte substitution using a fixed S-box
- ShiftRows: Cyclic shift of State rows for inter-column diffusion. 
- MixColumns: Matrix multiplication in  for intra-column diffusion.
- AddRoundKey: XORing the State with the subkey. 

## Mathematics of AES - finite fields
- Field: Operations are performed in the Galois Field GF($2^8$).
- Irreducible Polynomial: $m(x) = x^8 + x^4 + x^3 + x  + 1$ 
- Field Addition: Bitwise XOR.
- S-box Construction: 
	1. Multiplicative inverse in GF($2^8$.
	2. Affine transformation to break algebraic structure. 
- Benefit: Mathematical rigor provides..

##### Modes of Operation (Confidentiality)
- ECB (Electronic Codebook): Simple but leaks patterns. Never use for structured data. 
- CBC (Cipher Block Chaining): Chains blocks together; requires an Initialization Vector (IV)

### Applications of Symmetric Encryption
- Data at Rest: Full Disk Encryption (FDE) using AES-XTS (BitLocker, FileVault)
- Data in Transit: TLS 1.3 records, IPsec (VPNs), and SSH. 
- Mobile & IoT: WPA3: Uses AES-CCMP/GCMP for Wi-Fi security. 
- ZigBee: Standardized on AES-128 for low-power mesh networks. 
- Hardware Acceleration: AES-NI (Intel/AMD) and ARMv8 Cryptography Extensions. 

##### The Quantum Threat and FIPS Compliance
- FIPS 140-3: The current standard for cryptographic modules, replacing FIPS 140-2. 
- Grover's Algorithm: A quantum attack that provides a quadratic speedup for brute force.
- Mitigation: Transition to AES-256 to maintain a 128-bit security margin.