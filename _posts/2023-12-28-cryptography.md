---
title: "Cryptography"
layout: post
---
Summary:
  1. Use encrypting/decrypting techniques
  2. Generate hashes and file checksum

To begin this exercise, I logged into the administrator account of a Windows OS virtual machine.

Next, I launched the application Cryptool, and opened a new file.

In the new file I entered the phrase, "This is an example of how data hashing works!!" and clicked Hash Demonstration to demonstrate how MD2 (128 bits) hexadecimal hash looks when converting the phrase.

Next, I entered another phrase, this time, "This example shows the differences between the old file and the new one. This time I chose SHA-256 (256 bits) as the hash algorithm and I was shown that the hash values are now completely different.

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/2841d1c4-eea2-44b9-9987-b17cb62645c0)

In the next portion of the exercise, I practice encrypting and decrypting text.

To begin, I navigated to the Encrypt/Decrypt tab of the application and chose Symmetric (modern) and AES (CBC) with the key length of 128 bits.

Next, in the text box I entered, "AA AA AA BB BB BB CC CC CC", and clicked encrypt and viewed the output. I then clicked decrypt and I have successfully encrypted and decrypted using a symmetric algorithm.

<img width="374" alt="image" src="https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/7adea322-06d2-4759-b5bb-3fea9be356a9">

Next, I went to the RSA Demonstration tab and configured the demonstration to use a private key by choosing two prime numbers and setting the modulus and encryption equation in the RSA parameters field.

I then chose to use the Miller-Rabin Test, and the upper and lower limits for the prime numbers.

<img width="844" alt="image" src="https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/4f329806-10dd-4f8b-b3ab-c74b1b12d7a9">

Next, I uploaded a file given to me during the exercise to the application to encrypt it. 

While uploading the file, I Generated a session key and selected a asymmetric key, encrypted document symmetrically, encrypted session key asymmetrically, encrypted the document, and encrypted the session key.

At this point, I was provided with the file in encrypted data in hexadecimal and plain text. The next step is to decrypt the file.

To do this, I navigated to the RSA-AES Decryption tab and was shown a certificate, the private RSA key, and the session key.

I was then shown the encrypted and decrypted file.

<img width="968" alt="image" src="https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/98c6378e-b2ba-4788-b81e-d58a089bf75d">






