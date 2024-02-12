# winter

So basically we have an implementation of the Winternitz singature scheme which when executed, we need to submit a message in hex and it gives the signature for that message. Next we need to give another message in hex but this time we need to also give the signature for that message in hex. And if the signature for the second message that we gave is correct, we get the flag.

## Winternitz signature scheme

It is a quantum resistant digital signaturing method which uses mathematical technique to validate the authenticity and integrity of a message. 

### Key-Generation

The first part of the scheme is the key generation. We need to first create a private key which further yields us the public key.
To create the private key, a random number generator is used to generate 32 256-bit random numbers. It is know to the sender and receiver.
To create the public key, each of the 32 numbers is hashed 256 times to obtain another set of 32 256-bit numbers. The public key is shared with everyone.

![image](https://github.com/Wixter07/DiceCTF-2024/assets/150792650/4ee62f73-b6b9-47a3-a953-48d29547dc56)

### Signature-Generation

Now for signing the message, we need to hash the message we're sending using SHA256 which produces a 256 bit digest. This digest is split up into 32 8 bit values.

<img width="363" alt="wots" src="https://github.com/Wixter07/DiceCTF-2024/assets/150792650/7b0fe368-d311-4b2a-a5e4-cef202541e64">

Then we take each of the private key and SHA256 hash it **256-N** times, where N is the value of 8 bit value. So if the value of the first 8 bit value N1 is 32, we hash the first value of the private key **256-32** times. We do the same for all the 32 bytes in the private key.

![image](https://github.com/Wixter07/DiceCTF-2024/assets/150792650/79f15ed6-617a-4a81-a533-e88da4397c80)

### Signature-Verification

For verification, since the receiver knows the private key, we first SHA 256 hash the message to get the 256 bit digest which is split into 32 8 bit values. Now we know what the 8 bit values are, we hash the private key with the 32 8 bit values and after hashing if we get the public key, the message is verified.


![image](https://github.com/Wixter07/DiceCTF-2024/assets/150792650/9f8a778c-b05e-4332-99a0-9452659441f4)

