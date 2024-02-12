# winter

So basically we have an implementation of the Winternitz singature scheme which when executed, we need to submit a message in hex and it gives the signature for that message. Next we need to give another message in hex but this time we need to also give the signature for that message in hex. And if the signature for the second message that we gave is correct, we get the flag.

## Winternitz signature scheme

It is a quantum resistant digital signaturing method which uses mathematical technique to validate the authenticity and integrity of a message. 

### Key-Generation

The first part of the scheme is the key generation. We need to first create a private key which further yields us the public key.
To create the private key, a random number generator is used to generate 32 256-bit random numbers. It is know to the sender and receiver.
To create the public key, each of the 32 numbers is hashed 256 times to obtain another set of 32 256-bit numbers. The public key is shared with everyone.

![image](https://github.com/Wixter07/CTF-s/assets/150792650/194fe71c-523d-442e-be5b-bfb89d0a2f38)

### Signature-Generation

Now for signing the message, we need to hash the message we're sending using SHA256 which produces a 256 bit digest. This digest is split up into 32 8 bit values.

![image](https://github.com/Wixter07/CTF-s/assets/150792650/adfdca55-8807-441d-b7d8-133ac6fabfbc)

Then we take each of the private key and SHA256 hash it **256-N** times, where N is the value of 8 bit value. So if the value of the first 8 bit value N1 is 32, we hash the first value of the private key **256-32** times. We do the same for all the 32 bytes in the private key.

![image](https://github.com/Wixter07/CTF-s/assets/150792650/5f5e024d-4087-435a-badd-58bb4929a955)

### Signature-Verification

For verification, since the receiver knows the private key, we first SHA 256 hash the message to get the 256 bit digest which is split into 32 8 bit values. Now we know what the 8 bit values are, we hash the private key with the 32 8 bit values and after hashing if we get the public key, the message is verified.


![image](https://github.com/Wixter07/CTF-s/assets/150792650/11915e3f-4e74-4a49-a9c6-16f76dbed230)

## The challenge

So the variables in the code are sk and vk. sk is the private key and vk is the public key.
The key generation is as shown below

    def keygen(cls):

		sk = [os.urandom(32) for _ in range(32)]
  
		vk = [cls.hash(x, 256) for x in sk]
  
		return cls(sk, vk)

sk takes in a random 32 byte strings and vk is obtained by SHA256 hashing sk 256 times.

The Signature-Generation is as shown below

    def sign(self, msg):

    m = self.hash(msg, 1)
   
    sig = b''.join([self.hash(x, 256 - n) for x, n in zip(self.sk, m)])

		return sig

Refer to the Signature Generation in WOTS above to understand.

The Signature-Verification is as shown below


    def verify(self, msg, sig):

		chunks = [sig[i:i+32] for i in range(0, len(sig), 32)]
  
		m = self.hash(msg, 1)
  
		vk = [self.hash(x, n) for x, n in zip(chunks, m)]
  
		return self.vk == vk
  


So here, if the vk we obtained after hashing the digest by N number of times is same as the vk initially being generated, we get the flag.

I wasn't able to get what was going on in this challenge while the CTF was still up, but now I understood something but I may be wrong

The the vk and sk generated stays the same for the second message also. So assuming that it doesn't change and that we already have the signature for the first messgae, we can actually calculate what the N values are and get the signature for the second value.

That way, we may get the flag.


