## RSA (Rivest-Shamir-Adleman)
It is a public-key cryptography system used for encrypting data, securely exchanging keys and creating/verifying digital signature.

RSA uses two keys -
- Private Key (kept secret)
- Public Key (shared with anyone)

It relies on difficulty of factoring product of two very large prime numbers. Now, multiplying large prime number is easy but factoring is extremely difficult for sufficiently large prime numbers.

Now, let's say we take two large prime numbers, p and q, so n = p * q which is part of both private and public key.

Now, we compute euler's totient function which is  $\varphi(n)$ = (p-1) * (q-1).

Now, for the calculation of public key, we take any value where 1 < e < $\varphi(n)$ and gcd(e,  $\varphi(n)$ ) = 1.

Now, we compute private key d, where d ≡ $$e^{-1}$$ mod( $\varphi(n)$ ), where we calculate d using extended euclidean algorithm.

Once, we get the value of d computed using e, we will get final keys as private and public key.
- Public Key: (e, n)
- Private Key: (d, n)

### Encryption
Let's say I am having a message M, let's say a json payload consisting of various parameters, now firstly we stringify it and apply RSA using public key, to encrypt the message and get cipher text, now we will get it in the form of bytes, so we convert it to base64 because bytes are a bit volatile and can even cause noise inside the payload.

Hence, Cipher Text, C = $$M^e$$ mod(n), where n = p * q and M < n

### Decryption
Now, I am having a cipher text and want to decrypt it, so we need to utilise RSA private key to decrypt the message. Once we get the decrypted message, we will get the original message.

Hence, Original Message = $$C^d$$ mod(n), where n = p * q

Now, let's say John Doe is a spy who wants to transfer secret messages from one country to the other country. So, the country sends its RSA public key to John Doe and he encrypts his message using that public key and send that generated cipher text to his country. Now, he sends his RSA public key to the country. Now, country decrypts the sent cipher text message using its RSA private key and then would send another encrypted message back to John for further decryption from his side.








