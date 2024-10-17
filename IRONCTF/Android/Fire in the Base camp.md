# Fire in the Base Camp

Ye so solved this after the CTF. The challenge name hints it pretty well, a firebase db. Used android studio to decompile, was hard to interpret and then jadx'ed it.

We need to get the firebase db url, which can be found in `/res/values/strings.xml`

So this `https://app3-7d107-default-rtdb.firebaseio.com/`

That literally had the flag

![image](https://github.com/user-attachments/assets/b8a2974b-dd13-4078-8eb2-2d580cd47617)

The flag - `ironCTF{y0u_pu7_0u7_th3_f1r3_1n_th3_b4s3_c4mp_1f84a5c66f5}`
