# Module: Crypto Misuse

In service, and the patterns CTF-style services favour. Ordered by frequency.

1. Identify first: what algorithm and mode, where the IV, nonce, and tag live, and whether encryption is deterministic (the same input giving the same cookie or token twice means ECB or a fixed IV; testable in 10 seconds).
2. ECB: repeated 16-byte blocks in ciphertext; cut-and-paste block reordering to forge a profile or token block containing an admin or role field.
3. CBC: differential errors or timing on bad padding means a padding oracle (byte-by-byte decrypt; automate it, it is mechanical). No oracle means bit-flipping in the preceding block to edit a known plaintext field.
4. CTR and GCM nonce reuse: two ciphertexts under the same nonce or IV give the XOR of the plaintexts; crib-drag with known or guessable plaintext (flag format, JSON keys). GCM reuse also breaks authenticity.
5. RSA: collect n, e, c, and relationships, then in order: factor check (FactorDB); small e with the message power below n (direct root); Hastad broadcast (same message, at least e recipients); common modulus; shared prime across keys (gcd of two moduli not equal to 1); Wiener (small d); parity or LSB oracle; Franklin-Reiter related message; Coppersmith and LLL for partial leaks via Sage or RsaCtfTool. Record which test ran clean. RSA nodes die by checklist exhaustion, not by vibes.
6. Hash and MAC misuse: length extension on secret-prefix MD5 and SHA1 constructions; timing comparison leaks; custom or homebrew ciphers mean look for XOR with a repeating key (index of coincidence plus frequency), a time-seeded PRNG (brute the timestamp window), or LCG state recovery from outputs.
7. In-service rule: crypto in a lab box is almost always implementation misuse around a token, cookie, or reset flow. Attack the oracle the service gives you (error, timing, acceptance). Do not attempt mathematics against a correctly parameterised primitive. Go around, not through.

Tools: FactorDB, Sage, RsaCtfTool.
