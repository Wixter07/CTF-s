# Secure Vault 


Man I was frustated with this one. This was easy enough to figure out what exactly you had to do. 

Flutter APK. Initial thoughts were to use reFlutter for ssl unpinning but realized there was no network logs even with pinning. So this was actual Flutter rev. Found out about [blutter](https://github.com/worawit/blutter).

That's it. I had to do 

```bash
wixter07@HARSHITH:~/blutter$ python3 blutter.py ../chall/lib/arm64-v8a out_dir
```

blutter.py will automatically detect the Dart version from the flutter engine and call executable of blutter to get the information from libapp.so.

Unfortunately, that thing crashes for me. Tried it on one of my teammates laptop too and it crashed for him too. So wasn't able to solve it. Basically blutter will give the libapp assemblies with symbols.
All the info would be b64 encoded. It would take some time to look for the actual b64 encoded flag. 

Went through a writeup and found that the encoded flag was in `/asm/adminvault/main.dart`. Ye figure why it was in adminvault.

I have tried the challenge and got blutter to work on Windws rather than Lin

The flag - `ironCTF{0h_my_g0d!!_y0u_br0k3_int0_th3_4pp_4f6e22cba}`
