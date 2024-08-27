# Crack Me
So we have an .apk file which on opening on Android Studio shows up to be build using react native. So used this [decompiler](https://www.npmjs.com/package/react-native-decompiler) sent by Akash which gives us some 600 js file. The app was a login page so we can search for the place holders of user name and password. On looking for `sekai.team` we get this as our first reference 
```js
var _ = {
  LOGIN: 'LOGIN',
  EMAIL_PLACEHOLDER: 'user@sekai.team',
  PASSWORD_PLACEHOLDER: 'password',
  BEGIN: 'CRACKME',
  SIGNUP: 'SIGN UP',
  LOGOUT: 'LOGOUT',
  KEY: 'react_native_expo_version_47.0.0',
  IV: '__sekaictf2023__',
};
exports.default = _;
```

So it's AES by looking at the key and iv. I searched for references of AES and we get this part of code where it validates the password
```js
e.validatePassword = function (e) {
      if (17 !== e.length) return false;
      var t = module700.default.enc.Utf8.parse(module456.default.KEY),
        n = module700.default.enc.Utf8.parse(module456.default.IV);
      return (
        '03afaa672ff078c63d5bdb0ea08be12b09ea53ea822cd2acef36da5b279b9524' ===
        module700.default.AES.encrypt(e, t, {
          iv: n,
        }).ciphertext.toString(module700.default.enc.Hex)
      );
    };
```

Ued this decryption script to get the password 
```python
from Crypto.Cipher import AES
from Crypto.Util.Padding import unpad
import binascii

ct_hex = "03afaa672ff078c63d5bdb0ea08be12b09ea53ea822cd2acef36da5b279b9524"

ct = binascii.unhexlify(ct_hex)

iv = "__sekaictf2023__".encode('utf-8')

key = "react_native_expo_version_47.0.0".encode('utf-8')

cipher = AES.new(key, AES.MODE_CBC, iv)

plaintext = unpad(cipher.decrypt(ct), AES.block_size)

plaintext_str = plaintext.decode('utf-8')

print("Le beta:", plaintext_str)
```
This gives us the password as: `s3cr3t_SEKAI_P@ss`

Another reference of `sekai.team` brings us to this 
```js
   e._verifyEmail =
      ((o = module275.default(function* (t) {
        t.setState({
          verifying: true,
        });
        var n = module478.initializeApp(module477.default),
          o = module486.getDatabase(n);
        if ('admin@sekai.team' !== t.state.email || false === e.validatePassword(t.state.password)) console.log('Not an admin account.');
        else console.log('You are an admin...This could be useful.');
        var s = module488.getAuth(n);
```
We see that something interesting happens when we login as `admin@sekai.team`. So logged in as that and as seen it tells us `You are an admin...This could be useful`.
Now there was two ways of solving this challenge. The intended way was to go to the firebase database where all user id's where stored as hashed and write a script that runs all the hashes and finds the correct one. The unintended solution was Akash's idea where we can perform HTTP unpinning and log all the network requests. We tried checking the logs on the first day of the ctf but couldn't get to the flag. Plus there were infra issues.
I gave this chall a shot the next day and ran the apk on Android Studio, plugged HTTP Toolkit to that device and logged in with these credentials
```
Username - admin@sekai.team
Password - s3cr3t_SEKAI_P@ss
```

Then I checked for the logs registered and found the flag 
![image](https://github.com/user-attachments/assets/68da2ee5-0804-4437-b854-a7296a1bffe7)
Flag - `SEKAI{15_React_N@71v3_R3v3rs3_H@RD???}`

## Learnings
- Got to know about a new tool called HTTP Toolkit
- Maybe learnt a bit of how android reverse challenges are though this one's not a good example
