# Talking Phase

Well this was pretty easy but took me time due to brain fog at 4 am. There are two entities A and B who are communicating with each other by exchanging their RSA OAEP public keys. All the communicationgs is in B64 encoded format.

## Approach
You are entity C who can intercept the key and messsage and have the option to tamper with them. I generated my own key and tampered on both sides so that I can decrypt the message they are trying to communicate with each other. Now just tampering the keys won't do because let's say A encryptss a message with B's key (Which is my key as I replaced it), I can decrypt it, but B won't be able to with his private key. I was stuck here at 4am, I then thought let's just sleep, something might pop up on my mind when I wake up and voila. Didn't even take me 2 mins to think on what the solution might be after I woke up. So while launching the instance and tampering with the keys, both A and B's public key were actually displayed. So to tamper the message, I can just encrypt A's messaage to B with B's public key.

So there is they code block

```py
def checkflag(self, message):
		if message == b"giv me the flag you damn donut":
			return True
		else:
			return False
```
I decoded A's message to be and then encrypted `giv me the flag you damn donut` with B's public key and sent it forward. That's it

I also realized later that you can solve this without even tampering the keys

The flag - **`TCP1P{smooth_talker_or_talk_smoother}`**
