# Security

* CIA

  * Confidentiality
  * Integrity
  * Availability

* Criptography

  * Not

    * Encoding
    * Steganography: Hiding that there are messages. Invisible ink, Secret tattoos
    * One-way function

  * Kerchoffs' principle

    * Assume that the enemy knows all about your system.

      Security must rest solely on secrecy of the keys.

  * Historical ciphers

    * Caesars cipher

      * System:
        * ciphertext = message + key (mod 26)
        * message = ciphertext - key (mod 26)
      * Only 26 possible keys
        * Brute force attack
        * A good cipher need **a large number of possible keys**

    * Monoalphabetic ciphers

      * Caesar-rotating: 26 possiblities

        Random shuffle: 26! possiblities

      * Frequency

      * A good cipher also needs to hide **pattern** in the message

    * Vigenere cipher

      * Pick a secret work

        use **alphabet square**

        ciphertext = message + key

      * Polyalphabetic: uses a different key for differet letters

      * Frequency analysis

        * Divided into rows every n letters
        * frequency analysis each column

      * **Kasiski analysis**

        * ```
          ALPNALPCZIYIALTHALCDBKSH
          | 4 |   8   | 4 |
          ```

        * GCD of 4 and 8 is 4

  * Bits of security

    * A safe with an n-digit code:

      * You (the owner) need to remember D = n digits
      * A burglar has to try B = $10^n$ cominations

    * A cryptographic system with **n bits of security**

      * you need some "efficient" function of n steps/time to operate it (e.g. $n^2$)
      * **to break the system takes $2^n$ steps/time**

    * **$log_2(26!) = 88.38 = 89$**

      Nowadays 128 bits is the minimum requirement

    * Key length is not the same thing as security level

    * Security recommendations

      * 56: pitiful
      * 80: weak
      * 128: minimal
      * 192: recommended
      * 256: secure

* Symmetric

  * Lessons from Vigenere cipher

    * if the key is as long as the message, no need to repeat
    * choose a key with no patterns

  * One-time pad

    * Truely random
    * at least as long as the plaintext
    * never reused
    * kept completely secret
    * **Impossible** to decrypt
    * **Information-theoretically secure**
      * cannot be broken even with unlimited computing power
      * the ciphertext deos not contain enough information for any cryptanalysis to succedd

  * Block ciphers e.g. AES (advanced encryption standard)

    * **approaches**

      * Feistel networks

        * used in DES, etc

      * Substitution-permutation network

        * Substitution: replace with something else

        * Permutation: shuffle the content around

          * the Rail-Fence permutation cipher

          * ```
            killtheemperor
            k  l  e  p  o
             i  t  e  e  r
              l  h  m  r
              
            KLEPOITEERLHMR
            ```

        * AES
      
      * Lai-Massey

    * Modes of Operation
    
      * ECB (electronic code book)
        * $C_i=E_k(P_i)$
        * Never do this
        * pattern exists
      * NEED initialisation vector
      * CBC (cipher block chaining)
        * $C_i=E_k(P_i+C_{i-1})$
      * CTR (counter) - stream cipher
        * $S_i=E_k(IV,i)$$C_i=P_i+S_i$

* Authentication

  * MAC (Message Authentication Code)

    * MAC

      * Passive attack: observe

        Active attack: insert, delete, change

      * Integrity: can detect if the message modified

      * A MAC is a single, deterministic function M(k,m). Without k, it should be hard to find M(k,m) for any m.

      * NOT MAC

        * Checksums
        * hash
        * no integrity, attacker can compute checksum/hash for new msg
        * MAC needs a key

      * CBC MAC

        * tag = last block of CBC with IV = 0

      * Hash-MAC: prepend (twiddled) key and hash, then repeat

        * tag = Hash(key++Hash(key++msg))

    * Encryption: confidentiality

      MAC: integrity

    * Dont send mac without encrypt it (encrypt-and-MAC)

      * Cryptographic protocols do exactly what they were designed for, and no more
      * MAC does not need to keep anything confidential

    * Encrypt-then-MAC or MAC-then-Encrypt

    * Authenticated Encryption

      * Provides both confidentiality and integrity: without k, it should be hard to
        * learning anything about m from c = E(k,m)
        * compute E(k,m) for any m

  * Authentication = identification + authorisation

    * offline: credential

      Online: database

  * Passwords
    * Good:
      * easy for human to remember
      * hard for computer to guess
    * haveibeenpwned.com

* Public-key cryptography

  * Security problem ->Key management problem
    
    * n people = $O(n^2)$ keys needed
    
  * public-key encryption
    * The padlock analogy
      * You can send me a locked box without ever seeing my key
    * Public keys
    * secret keys
    * A public-key encryption scheme contains three algorithms
      * Key generation algorithm **K**
      * Encryption algorithm **E**
      * Decryption algorithm **D**
      * If **(pk, sk)** comes from **K** then **D(sk, E(pk, m)) = m**
    
  * RSA
    1. Choose any two distinct prime numbers, p & q
    2. Compute n = pq
    3. Select a prime number e between 1 and lcm(p-1, q-1)
    4. The public key is <n, e>
    5. Compute the number d such that $(d * e)\space mod\space lcm(p-1, q-1)=1$
    6. The private key is <n, d>
    7. To encrypt a message m $c=m^emod\space n$
    8. To decrypt a ciphertext c  $m = c^dmod\space n$
    * Secyrity relies on the diffculty of factoring n into p and q (for large values)
    
  * PGP
  
    * GnuPG (Gnu Privacy Guard)
  
  * Key exchange
  
    * HTTPS
  
    * Hybrid encryption
  
      * Public key encryption is much slower than symmetric encryption
      * Use asymmetric exchange symmetric key
  
    * Diffie-Hellman key exchange
  
      * magic functions
        * one-way
        * linear: $f(a+b)=f(a)+f(b),\space f(c*a)=c*f(a)$
  
      * A: secret a
  
        $b=f(a)$
  
        B: secret c
  
        $d=f(c)$
  
      * $k=a*d=c*b$
  
        $a*d=a*f(c)=f(a*c)=c*f(a)=c*b$
  
      * actually $k = H(a*d) = H(c*b)$
  
      * suitable vector spaces with linear one-way functions
  
        * $V=Z_p^*,f(x)=g^x(mod\space p)$ (g is a fixed, public base value)
        * $V=elliptic\space curve, f(x)=x*P$ (P is a fixed, public point on the curve)
          * EC give better keylength size
  
* Digital signature

  * Digital signature scheme contains three algorithms
    * Key generation algorithm **K**
    * Signing algorithm **S** takes a secret key and a message and returns a signature
    * Verification algorithm **V** takes a public key, a message and a signature and returns yes or no
    * if (pk, sk) comes from K then **V(pk, m, S(sk, m)) = "yes"**
  * Notes 
    * The sig has a fixed size - however long the message(Usually one signs a hash of the message)
    * Unlike a handwritten one, does not change the original document - its an extra piece of data
    * If you sign two diff documents, the two digi sig will not be the same
  * PGP / GPG
  * Non-repudiation
    * If you sign a message, anyone with the signature can prove to a third party with an authenticated copy of your public key that you signed the message (or your key has been compromised)
  * Terminology
    * ultimate trust = this is my own key
    * full trust = i trust this person to sign others' keys
    * marginal trust = I trust this person's key, but i don't completely trust them to sign others keys
    * GPG: one full or ultimately trusted or at least three marginally trusted
    * chains of trust can be at most 5 steps long

* Protocols
  * inside the car: challenge-response protocol
    * please encrypt "N" with our shared key k
  * Man-in-the-middle
  * Reflection attack
    * $\{A,N\}_k$ doesn't work for B to verify with A
  * Announcing yourself
  * Key exchange
    * Needham-Schroeder protocol
* Social engineering





* EAX, EBX, ECX, EDX, ESI, EDI
* ESP, EBP
* EIP: extended instruction pointer

* HTTP-TCP
* DNS-UDP

`