# The Constraints of Block Cipers
The AES Primitive


# The Three Pillars of Symmetric Encryption
- Block cipher (AES): *confusion*
- Mode of operation: *diffusion + scalability*
- Randomness (IVs, nonces, counters:): *semantic security*

If **any pillar fails**, confidentiality fails-even if AES is perfect. 

# ECB Mode Properties
**Definition**
- Each block is encrypted independently: $C_i = E_k(P_i)$ 
**Advantages**
- Parallelizable: High Performance
**Critical Flaw**
- Deterministic: Identical inputs yield identical outputs
- Structural patterns in plaintext remain visible in cipher-text
**Things to Think About**
- ECB provides no semantic security under chosen-plaintext attack
- ECB leaks equality patterns: $P_i

# Visualizing ECB failure: The Penguin
The most famous Image in Cryptography 
**The Flaw**
- Repeating blocks (white background = 0xFF) encrypt to identical cipher-text.
- This demonstrates a total lack of diffusion. 
(Don't re-use the key!!! Gotta change it somehow every iteration)

# Cipher Block Chaining (CBC)
**Definition**
- Input is XOR of current plaintext and previous cipher-text
- $C_i = E_k(P_i \XOR C_{i-1})$ 
**The Initialization Vector (IV)**
- Used for the first block

### CBC IV Rules
- IV must be unpredictable
- IV must be unpredictable and unique per encryption
- Reusing an IV enables prefix attacks

If the same IV is reused, the first cipher-text block leaks whether two messages start with the same plaintext

randomness $\neq$ decoration - it's structural

### CBC Error Propagation
Decryption Formula
- $P_i = D_k(C_i) \XOR C_{i-1}$ 
Scenario: Single bit error $C_1$
- Block 1 ($P_1$): Completely garbled (Avalanche Effect)
- Block 2 ($P_2$): Specific bit error (XOR bit flip)
- Block 3+

### Error Propagation

### Counter Mode

## CTR Mode Is Secure Only *If* the Nonce Is Never Reused
$C_1 \XOR C_2 = P_1 \XOR P_2$ 

Reusing a nonce turns CTR into a two-time pad -one of the oldest cryptographic disasters. 
Nonce + counter pair must never repreat under the same key

# Entropy Sources: RNG Taxonomy
**TRNG (True Random Number Generator)**
- Source: Physical (thermal noise, radioactive decay)
- Use: Key generation, seeds
**PRNG (Pseudorandom Number Generator)**
- Source: Mathematical (LCG, Mersenne Twister)
- Use: Simulation, games (NOT cryptography)
**CSPRNG (Cryptographically Secure PRNG)**
- Source: OS entropy pool (/dev/urandom)
- Use: Nonce, IV, Salt
**Critical Warning**
- Never use standard library random for cryptography - always use secrets or os.urandom
- If an API does not say '**cryptographically secure**', assume it is not. 

```
# Bad
random()
Math.random()

# Good
secrets.os.urandom.getrandom()
```

# What Breaks When RNG Fails?
- Weak IV -> CBC prefix leakage
- Reused nonce -> CTR paintext recovery
- Predictable RNG -> key recovery
- Broken randomness -> broken semantic security 

## Why We Don't Stop Here: Authenticated Encryption
- Modes like CBC and CTR provide confidentiality-but not integrity. 