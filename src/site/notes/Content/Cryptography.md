---
{"dg-publish":true,"permalink":"/content/cryptography/","tags":["crypto","ctf"],"created":"2024-09-16T18:16:30.320-07:00","updated":"2024-09-17T23:38:30.994-07:00"}
---

> [!IDEA] Decoding tips
> - character frequency analysis
> - consider various data representations
> 	- ASCII, HTML encoded chars, base64, hex, etc
> - rainbow tables 🌈 (precomputed hashes)
> - use automated decoders such as [Cyberchef](https://cyberchef.org/), [QuipQuip](https://www.quipqiup.com/), or [dCode](https://www.dcode.fr)
## Simple Ciphers
- Ceasar: shift left/right by a certain offset
- ROT13: Ceasar with offset of 13
- Vigenère: each letter uses a different Ceasar cipher, which is given by a key (use table to decrypt)
- Substitution: like Ceasar but not a set rotation
- Hashes: not really a cipher, but appears a lot in cybersec
- XOR: exclusive OR (true if only 1 out of 2 bits is set)
- Railcipher: zigzag offsets that vary in # of rails
## Sophisticated Ciphers
- [RSA](https://github.com/madfrogsec/how-to-rsa) hard to factor large prime numbers _p_ and _q_; use this to generate public and private keys
- Block: encrypt messages 1 block at a time
	- modes include ECB, CBC, PCBC, CFB, OFB, CTR, etc
- Stream: XOR with random keystream to generate OTP
	- vulnerable to key reuse and bit flipping to alter message
	- synchronous: stream generated independently of state, requires synchronous state to (en/de)crypt
	- asynchronous/self-synchronizing/CTAK: uses previous _N_ digits to compute keystream for next _N_ chars
## Helpful Links
- [.wav morse decoder](https://morsecode.world/international/decoder/audio-decoder-adaptive.html)
- cipher identification: https://www.dcode.fr/cipher-identifier
- [RSATool](https://github.com/RsaCtfTool/RsaCtfTool) lists many RSA attacks
- https://github.com/Ciphey/Ciphey
- [Cryptopals](https://cryptopals.com/) challenges