---
title: "Introduction to Cryptography: Encrypting My First Message"
date: 2026-04-27
categories: [cybersecurity]
---

This article details the basics of cryptography, specifically a simple example of how to use a Caesar cipher as well as an introduction to RSA, HMAC and AES. 

<h2>Introduction</h2>

Cryptography is a term that appears all throughout pop culture, appearing in many popular movies and tv shows. It is also used in many types of applications from messaging and email to cryptocurrency or data storage. It is very likely that you have interacted with some form of cryptography dozens of times, possibly without even realizing it. In fact, if you are reading this article right now, you are doing exactly that! The part of the url that says "https" is actually one tiny part of what cryptography is used for. The "s" in "https" stands for secure, which means the connection between your computer and this page is encrypted, protecting the contents of the communication from being intercepted as they travel between the two. So, what exactly is cryptography? In short, cryptography is a broad field that focuses on protecting and hiding information through the use of algorithms, complex mathematical principles and codes to ensure that data is safe and protected from unauthorized users. While cryptography has been around for thousands of years, even appearing in early cultures such as Ancient Egypt, it has evolved over time to accommodate for advances in computing, science, and code-breaking humans! Today, many cryptographic principles rely on advanced mathematics that are still difficult for even the fastest computers to solve. Since it is such a vital and widely used concept, it is also an important tool for cybersecurity professionals to learn and utilize. 

In this article, I am going to provide an overview of how to use a Caesar cipher with a simple example. Then, I will provide an overview of three essential, modern cryptographic tools known as RSA, HMAC, and AES. It should be noted that using a Caesar cipher is purely for educational reasons as this cipher is not secure in the modern age and should not be used to protect important data. However, because it relatively simple and easy to learn, a Caesar cipher is a good place to start for beginners to gain the general idea behind cryptographic techniques. 

<h2>Process</h2>

<h3>Caesar Cipher</h3>

The Caesar cipher is a "monoalphabetic cipher \[meaning\] - one letter replaces another" \[1\]. It is one of the most widely known ciphers that exists and is an excellent tool for beginners as its process uses simple letter substitutions. Since the English alphabet only has 26 letters, there are only 25 possible substitutions that can be made for a single letter. Especially with the use of modern computers, this means that a Caesar cipher can easly be broken using brute-force or frequency analysis techniques. Frequency analysis is the process of breaking a code by "counting up the letters \[and identifying the\] most common letters" \[1\]. The way a Caesar cipher works is by shifting each letter by a specified amount and writing the enciphered message using the new letter assignments.

<h3>Caesar Cipher Example</h3>

Let's do an example where we encrypt the phrase "hello". We will do this by using a shift key (a shift amount) of 5 as follows:

- a = f
- b = g
- c = h
- etc.

In our phrase, we have:

- h shifts to m
- e shifts to j
- l shifts to q
- l shifts to q
- o shifts to t 

So, our enciphered text (shifted forwards by 5) now looks like: mjqqt

To decode the message, you simply have to shift each letter backwards by 5 to get the original plaintext that says "hello". 

<h3>RSA Encryption</h3>

RSA encryption is a commonly used algorithm for securing data that utilizes complex mathematical techniques, named for its creators, Rivest-Shamir-Adleman. It is an asymmetric encryption algorithm that is typically "used to generate symmetric keys because it is computationally expensive" \[2\]. An asymmetric encryption algorithm is one in which two keys are generated: a public key and a private key. The public key is available to everyone, meaning anyone can use it to encrypt a message. The private key is available only to one person, meaning only that person can decrypt the messages. One of the most well-known facts about RSA encryption is that it uses very large prime numbers in conjunction with a one-way mathematical function, which makes it extremely difficult to break, even for the fastest computers. A one-way function is an operation that is "easy to do, but hard to undo" \[2\]. Essentially, computers can multiply very large numbers quickly but they cannot easily "undo" that multiplication to figure out what the original numbers were. This is why RSA is utilized so often, since the difficulty in factoring extremely large numbers helps ensure data stays protected. 

The RSA process is completed as follows:

Step 1: Key Generation

- Choose two very large prime numbers, represented by p and q, respectively.

- Calculate the modulus, represented by n, as \\(n=p*q\\).

- Calculate the totient, represented by \\(\phi (n) \\), as \\(\phi (n) = (p-1)*(q-1)\\). 

- Find a value, represented by e, such that e is between 1 and \\(\phi (n)\\) and that the greatest common factor (GCF) between all three values is 1. 

- Find a value, represented by d, such that \\(d*e \equiv 1 mod(\phi (n))\\). 

- The public key is: (n,e)

- The private key is: (n,d)

Step 2: Encryption

- Convert the plaintext message, represented by M, into an integer representation (format) of the message, represented by m.

- The encryption formula is: \\(C = m^{e} mod (n)\\), where C represents the ciphertext message, m represents the original plaintext message converted to integer format, and (n,e) is the public key used to encrypt the message. 

Step 3: Decryption

- Convert the enciphered message, represented by C, into the integer representation (format) of the message, represented by m. 

- The decryption formula is: \\(m = C^{d} mod (n)\\), where m represents the integer format of the original message, C represents the ciphertext message, and (n,d) is the private key used to decrypt the message.

- After obtaining the integer format, m, convert m back into the original plaintext message, M. 

<h3>RSA Example</h3>

Let's do an example where Alice wants to send a message to Bob that says "hi" using RSA encryption. To keep it simple, we will assign the integer representations of each letter as they appear in alphabetical order. In other words, since "a" is the first letter of the alphabet we will say that a=1, b=2, c=3, etc. In practice, the integer values are typically assigned to each letter using ASCII character encoding. Also for the sake of simplicity, we will use small, simple prime numbers to demonstrate the concept rather than two large prime numbers. 

So, M = hi, where M is our original plaintext message. Now, we must convert each letter in the message into an integer format that we can use in our encryption. In our case, we have:

- h = 8 (since h is the 8th letter of the alphabet)
- i = 9 (since i is the 9th letter of the alphabet)

Step 1: Key Generation

- Bob generates a shared public key that anyone can see and a private key that only he knows, in order for Alice to send an encrypted message to him.

- Choose two prime numbers. Let p = 2 and q = 11.

- Calculate the modulus: \\(n=p\*q=2\*11=22\\), so n=22. 

- Calculate the totient: \\(\phi (n) = (p-1)\*(q-1)=(2-1)\*(11-1)=(1)\*(10)=10\\), so \\(\phi (n) = 10\\).

- Find a value, e, such that e is between 1 and \\(\phi (n)\\) and that the GCF of all three is 1. In this case, we must find e such that e is between 1 and 10 and the GCF of 1, e, and 10 is 1. Let e = 7.

- Find a value, d, such that \\(d\*e \equiv 1 mod (\phi)\\). In this case, we must find d such that \\(d\*7 \equiv 1 mod (10)\\). If we choose d = 3, then 3\*7 = 21 and 21 = 2\*10 + 1, i.e. 21 mod (10) = 1, so this value works! Note: there may be many possible values for d that satisfy this condition, which is part of the reason why RSA is so hard to break.

- Our public key is: (22,7)

- Our private key is: (22, 3)

Step 2: Encryption

- To encrypt the message, Alice must encrypt each letter individually, using the shared public key. 

- First, encrypt the letter h. In this case, we have that m = 8:

    - \\(C = 8^{7} mod (22) = 2097152 mod (22) = 2\\), so \\(C = 2\\).

- Next, encrypt the letter i. In this case we have that m = 9:

    - \\(C = 9^{7} mod (22) = 4782969 mod (22) = 15\\), so \\(C = 15\\).

- The enciphered message is: C = 2 15

Step 3: Decryption

- To decrypt the message, Bob must decrypt each value individually, using his private key.

- First, decrypt the value 2.

    - \\(m = 2^{3} mod (22) = 8 mod (22) = 8\\), so \\(m = 8\\).

- Next, decrypt the value 15.

    - \\(m = 15^{3} mod (22) = 3375 mod (22) = 9\\), so \\(m = 9\\).

- The deciphered message is: m = 8 9

- Now, Bob must convert m back into the original plaintext message, M. Remember that the rule used to make this conversion was assigning each letter a value based on alphabetical order:

    - 8 = h
    - 9 = i

- So, the original plaintext message is: M = hi

<h3>HMAC</h3>

HMAC stands for Hash-based Message Authentication Code and it is used to verify "data integrity and authentication" \[3\]. In simple terms, if Alice wanted to send a message to Bob, she would first "hash" her message with a shared key that only she and Bob have and then send both the original message and the hashed message to Bob. After Bob receives the messages, he also uses the shared key to hash the original message that Alice sent. Bob then compares his hashed message with Alice's hashed message and checks to see if they are identical. If they are, then Bob knows the message was not altered in transportation and it's integrity is intact. If the message is not identical, then Bob knows that the message may have been intercepted and changed during transportation and it is compromised. There are different types of hashes that are used in HMAC such as "MD-5, SHA-1 or SHA-256" \[3\]. Regardless of which type of hash is used, however, the process remains the same:

1. Obtain the block size, represented by b, which is a standard value based on the specific hash type chosen. This value is typically 64 bytes or 128 bytes. Then, convert the original message to a number format, represented by m, typically using hexadecimal values. This can be easily done using an ASCII table. The chosen hash type will be represented by H.

2. Generate the secret key, represented by K. 

    2.1. If K is not the same length as b, it must be padded with extra zeros at the end. In other words, if the block size is 64 bytes, then K must be 64 bytes as well.

3. Perform the XOR (exclusive-OR) operation on K and ipad. ipad is a standard value, represented in hexadecimal as 0x36, and it stands for "inner padding".

    3.1. ipad must be the same byte-length as K. In other words, if K is 64 bytes long, then ipad = 0x363636... with 36 repeated a total of 64 times. 

4. Append the numerical message m with the result obtained from step 3: (K (XOR) ipad) \\(\|\|\\) m

    4.1. In this context the symbol \\(\|\|\\) simply means concatenate. In other words, stick m to the end of the result from step 3 as if you are glueing them together. It is important to remember that in this context, \\(\|\|\\) does NOT mean "OR". 

5. Perform the inner hash, H_inner on the result from step 4. This simply means use your chosen type of hash on the result from step 4 and we will call this outcome H_inner.

6. Perform the XOR (exclusive-OR) operation on K and opad. opad is a standard value, represented in hexadecimal as 0x5c, and it stands for "outer padding".

    6.1. opad must be the same byte-length as K. In other words, if K is 64 bytes long, then opad = 0x5c5c5c... with 5c repreated a total of 64 times.

7. Append H_inner (the inner hash obtained from step 5) to the result obtained from step 6: (K (XOR) opad) \\(\|\|\\) H((K (XOR) ipad) \\(\|\|\\) m)

    7.1. As before, in this context the \\(\|\|\\) simply means concatenate. In other words, stick the result of step 5 to the end of the result of step 6 as if you are glueing them together.

8. Perform the hash, H, on the result of step 7. This is the final hash, resulting in the completed HMAC. 

The general formula for HMAC is: \\(HMAC = H((K (XOR) opad) \|\| H((K (XOR) ipad) \|\| m))\\)

<h3>HMAC Example</h3>

Let's do a simple example where Alice wants to send a message to Bob using HMAC. For simplicity, the block size will only be 4 bytes long and Alice will send a message using only the letter "A". For a more detail explanation, we will also convert numbers to binary for specific operations. In addition, we will adapt this [how to do 8 bit modulo 256 to obtain checksum](https://stackoverflow.com/questions/49825888/how-to-do-8-bit-modulo-256-to-obtain-checksum) idea to create our example hash. The example has we will use, H, will convert each byte to decimal format and then add them all together. It will then take this sum and perform modulo 256 on it. 

- We have that b = 4. The message m = "A" = 0x41 (in hexadecimal) = 65 (in decimal) = 01000001 (in binary). Alice obtained the values for m by using an ASCII table to look up the letter "A". 

- Let the shared key that both Alice and Bob have be K = 0x01020304 (in hexadecimal format) or for easier reading K = 01 02 03 04. In this case, K is already 4 bytes, so no adjustment is needed. However, let us look at two examples of what to do if this was not the case:

    - Case 1: K `<` b. In this case, "we need to add 0s until the key length equals the block size" [\4\]. For example, suppose K = 0x0102. In this case K is only 2 bytes and we need it to be 4 bytes. So, we add zeros to the end of K until it is 4 bytes long: K = 0x01020000. 

    - Case 2: K `>` b. In this case, "we first hash the key, and then add 0s until its length becomes b bytes" \[4\]. For example, suppose K=0x010203040506. In this case, K is 6 bytes and is too long. So, we first hash K using our example hash, H (if you were using SHA256 this is what you would use instead). First, we convert each byte to decimal format and then add them: 1 + 2 + 3 + 4 + 5 + 6 = 21. Then we do 21 mod (256), which equals 21. Convert 21 back to hexadecimal to get K = 0x15. Now, K is only 1 byte, which is too short. So, we add 0s to the end of it until it is 4 bytes long. We get K = 0x15000000. 

- Perform the XOR (exclusive-OR) operation on K and ipad. 

    - In hexadecimal format, we have K = 01000001. In binary, K = 0001000000100000001100000100. We can separate it by bytes for easier reading: 00000001 00000010 00000011 00000100.

    - Since K is 4 bytes long, ipad must be 4 bytes long. So, we get that ipad = 0x36363636, or in binary format, ipad = 00110110 00110110 00110110 00110110 (separated by byte for easy reading).

    - The XOR rules are as follows:
    
        - 0 XOR 0 = 0
        - 0 XOR 1 = 1
        - 1 XOR 0 = 1
        - 1 XOR 1 = 0

    - Perform XOR operation byte-by-byte:

        - 00000001 XOR 00110110 gives: 00110111 = 37 in hex

        - 00000010 XOR 00110110 gives: 00110100 = 34 in hex

        - 00000011 XOR 00110110 gives: 00110101 = 35 in hex

        - 00000100 XOR 00110110 gives: 00110010 = 32 in hex

    - So, we get K (XOR) ipad = 00110111001101000011010100110010 = 37343532

- Append the numerical message m with the result obtained from step 3: (K (XOR) ipad) \\(\|\|\\) m

    - Remember, m = 0x41 (in hexadecimal) = 01000001 (in binary)

    - In binary: 00110111001101000011010100110010\|\|01000001 = 0011011100110100001101010011001001000001

    - In hexadecimal: 37343532\|\|41 = 3734353241

- Perform the inner hash, H_inner on the result from step 4. 

    - Recall that our example hash H, first converts each byte to decimal and adds all the values together. Then, H takes this sum and performs mod (256) on it. 

    - First convert 3734353241 to decimal format (can use a calculator to do this): 55 52 53 50 65

    - Next add: 55+52+53+50+65 = 275 (in decimal)

    - Then: 275 mod (256) = 19 (in decimal)

    - Convert 19 back to hexadecimal to get: H_inner = 0x13 or in binary, H_inner = 00010011. 

- Perform the XOR (exclusive-OR) operation on K and opad. 

    - In hexadecimal format, we have K = 01000001. In binary, K = 0001000000100000001100000100. We can separate it by bytes for easier reading: 00000001 00000010 00000011 00000100.

    - Since K is 4 bytes long, opad must be 4 bytes long. So, we get that opad = 0x5c5c5c5c, or in binary format, opad = 01011100 01011100 01011100 01011100 (separated by byte for easy reading).

    - Using the same XOR rules, perform XOR operation byte-by-byte:

        - 00000001 XOR 01011100 gives: 01011101 = 5d in hex

        - 00000010 XOR 01011100 gives: 01011110 = 5e in hex

        - 00000011 XOR 01011100 gives: 01011111 = 5f in hex

        - 00000100 XOR 01011100 gives: 01011000 = 58 in hex

    - So, we get K (XOR) opad = 01011101010111100101111101011000 = 5d5e5f58

- Append H_inner (the inner hash obtained from step 5) to the result obtained from step 6: (K (XOR) opad) \\(\|\|\\) H((K (XOR) ipad) \\(\|\|\\) m) 

    - In binary: 01011101010111100101111101011000\|\|00010011 = 0101110101011110010111110101100000010011

    - In hexadecimal: 5d5e5f58\|\|13 = 5d5e5f5813

- Perform the hash, H, on the result of step 7.

    - First, convert 5d5e5f5813 to decimal format: 93 94 95 88 19

    - Next add: 93+94+95+88+19 = 389

    - Then: 389 mod (256) = 133 (in decimal)
    
    - Convert 133 back to hexadecimal to get: H = 0x85

So, we get HMAC = 0x85. In practice, this result would be much longer, typically at least 64 bytes long. 

Now, Alice the original message and the HMAC to Bob. Bob performs his own hash on the original message using the same shared key. If his result is HMAC = 0x85, then Bob knows the message was not changed in any way during transportation.

<h3>AES</h3>

AES stands for Advanced Encryption Standard and it is a symmetric block cipher that "uses various key lengths (128, 192, or 256 bits) to encrypt data in blocks of 128 bits each" [\5\]. Since AES is symmetric, this means that the same key is used for both encryption and decryption. Also, due to the nature of this algorithm, it is impractical to perform even a simple example of AES by hand. However, the general process that AES uses is as follows:

Step 1: Input Data

- Data is processed 128 bits at a time. 

- The number of iterations of the algorithm (commonly referred to as "rounds") varies based on the key length: 128 bit key means 10 rounds, 192 bit key means 12 rounds, 256 bit key means 14 rounds.

Step 2: Round Key Creation

- The original key is used to create many new keys, which will be used at each corresponding round of the algorithm. 

- The amount of round keys created depends on the number of rounds the algorithm will perform.

Step 3: Encryption

- Each block of data is "a 16-byte (4-byte x 4-byte = 128) grid column" [\5\]. 

- Each round of encryption has four steps: SubBytes, ShiftRows, MixColumns, Add Round Key

Step 3.1: SubBytes

- SubBytes means substitution. 

- Each byte is replaced using a lookup table called the S-box.

Step 3.2: ShiftRows

- The rows of each 4x4 byte grid are shifted as follows:

    - Row 0: not shifted

    - Row 1: shift left by 1 (for example: [byte4, byte5, byte6, byte7] = [byte5, byte6, byte7, byte4])

    - Row 2: shift left by 2

    - Row 3: shift left by 3

Step 3.3: MixColumns

- This step performs matrix multiplication.

- Each column is "multiplied by a specific matrix and thus the position of each byte in the column is changed" \[5\].

- This step is not performed in the last round.

- The specific matrices that each column is multiplied with are standards which are used in every implementation and are denoted in \[5\]. 

Step 3.4: Add Round Key

- Perform the XOR operation on the result from 3.3 with the corresponding round key. 

Step 4: Repeat step 3 many times (for however many rounds there are)

- This ensures that the encryption is hard to break.

Step 5: Decryption

- The same process is done as encryption, but in the reverse order using the same key, but with a few small differences:

Step 5.2: Inverse MixColumns

- This step also uses specific matrices for the multiplication operation, but these matrices are not the same as the ones used during encryption, as denoted in \[5\]. 

Step 5.4: Inverse SubBytes

- In this step, Inverse S-box is used as the lookup table. 

<h2>Challenges & Lessons Learned</h2>

- When doing simple examples of RSA encryption, it is important to choose your values carefully as small numbers can potentially result in you obtaining a zero for the ciphertext message, C. If this is the case, it is not possible to decrypt the message because you won't be able to obtain the original value of m. In practice, because RSA uses such large values, this problem does not occur (otherwise RSA would be ineffective). 

- In AES, the specific matrices used to perform the MixColumns steps were chosen as the standard by using a specific mathematical system that ensures the inverse matrices can quickly reverse (undo) the matrix multiplication that was done during the encryption step. This is why the numbers used in the encryption step are not the same as those in the decryption step. The numbers used during encryption were chosen because they are fast and efficient for most computer hardware. The numbers used during decryption were calculated by the mathematical system as the values that quickly undo the multiplication. 

<h2>Citations</h2>

\[1\] C. Trudeau, “A Brief Introduction to Cryptography,” Realpython.com, 2026. https://realpython.com/lessons/brief-intro-cryptography/ (accessed Apr. 24, 2026).

\[2\] C. Trudeau, “Exchanging Asymmetric Keys,” Realpython.com, 2026. https://realpython.com/lessons/asymmetric-keys/ (accessed Apr. 24, 2026).

\[3\] GeeksforGeeks, “What is HMAC(Hash based Message Authentication Code)?,” GeeksforGeeks, Jul. 12, 2025. https://www.geeksforgeeks.org/computer-networks/what-is-hmachash-based-message-authentication-code/

\[4\] O. Volkov, “How HMAC works, step-by-step explanation with examples,” Medium, Dec. 17, 2023. https://medium.com/@short_sparrow/how-hmac-works-step-by-step-explanation-with-examples-f4aff5efb40e

\[5\] GeeksforGeeks, “Advanced Encryption Standard (AES),” GeeksforGeeks, Aug. 08, 2025. https://www.geeksforgeeks.org/computer-networks/advanced-encryption-standard-aes/

<h2>Next Steps</h2>

- Implement RSA, HMAC, and AES using Python.