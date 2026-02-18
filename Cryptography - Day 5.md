________
02-18-2026 | 12:06
Status: #school 
Tags: #CS-4575 #Cryptography 
# Cryptographic Hash Functions & Integrity

### Why this Matters (Adversarial Mindset)
- Hashes appear everywhere: signatures, secure boot, certificates, version control, and authentication systems.
- Hashes are frequently misused as "authentication stamps".
- Many failures are construction failures-not "broken hash" failures.

**Learning Objectives**:
- Distinguish integrity vs authenticity under an adversarial threat model.
- State and interpret the three core hash security properties.
- Explain why collision security is ~n/2 bits for an n-bit hash (birthday bound).
- Describe Merkle-Damgard iteration, padding and length extension.
- Explain why HMAC is constructed with inner/outer pads and how to compute it. 

## Integrity in an Adversarial Setting
*Integrity is threat-model dependent*

### Accidental Integrity vs Adversarial Integrity
- Accidental corruption: noise, disk errors, bugs (checksums/CRCs often sufficient.)
- Adversarial modification: attacker can interpret, edit, and resend messages. 
- If a check value is unkeyed, the attacker can recompute it for a forged message. 

### A Hash Alone Does Not Authenticate

## Hashes as Primitives
*Fixed-length fingerprints with formal security goals*

# What is a Cryptographic Hash Function?
- Deterministic, efficiently computable function: $H : {0,1}* -> {0,1}^n$ 
- Arbitrary-length input -> fixed-length digest.
- Avalanche effect: small input change -> large, unpredictable output change.
- Fixed output size implies collisions must exist (pigeonhole principle).

# Three Core Security Properties
> [!important] 
>  Will be on exam!
- Preimage resistance: given $y$, hard to find $x$ with $H(x)=y$
- Second preimage resistance: given $x$, hard to find $x'\neq x$  with $H(x')=H(x)$.
- Collision resistance: hard to find any $x \neq x'$ with the same digest. 

### From Birthdays to Hash Collisions
- $n$-bit hash -> $2^n$ possible digests

#### Concrete Example: SHA-256
- Output size $n=256$ bits
- Generic Collision work ~ $2^{128}$ evaluations. 
- Preimage / second preimage work ~ $2^{256}$ evaluations.
- Takeaway: $256$-bit digest ~ $128$-bit collision security.

## How Hashes are Built

### Merkle-Damgard Construction (SHA-2 family)
- Message is processed in fixed-size blocks
- Iterative chaining: $Hi = f(Hi-1, Mi)$ 
- Final digest is the final chaining value
- Padding is deterministic and includes message length
` { IV } { M1 } { M2 } { M3 } { ... } { Mt } <- last iteration = final output`

# MACs: Integrity against Adversaries
- A MAC is a keyed function: $tag = MAC(K,M)$
- Provides integrity + origin authentication (shared-secret setting)
- Does not provide non-repudiation (accountability) 

## HMAC Structure
- $HMAC(K,M) = H((K0$ XOR opad) || $H((K0$ XOR ipad) || $M))$
- ipad (internal pad) = 0x36 repeated; opad = 0x5c repeated
- Two-layer design prevents length extension forgery
- Key material is mixed in both inner and outer computations

### HMAC Walkthrough Example (Step-by-Step)
1) Preprocess key -> K0 (key padded to the hash block size)
2) Computer inner key: K0 XOR ipad
3) Inner digest: inner = H((K0 XOR ipad) || M)
4) Compute outer key: K0 XOR opad
5) Final tag: tag = H((K0 XOR opad) || inner)
`Mixed the peices, added padding, hashed, and put em back together`

##### Engineering Takeaways (Checklist)
- State the threat model (is an active modifier in scope?).
- Translate digest length into collision strength (birthday bound).
- Do not use raw hashes for authenticity; use HMAC (or signatures).
- Do not invent keyed-hash designs; prefer standardized constructions.


