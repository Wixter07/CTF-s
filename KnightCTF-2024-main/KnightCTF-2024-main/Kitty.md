# Kitty

So we have a login page in hand which requires a username and password. 


![Screenshot (12)](https://github.com/Wixter07/KnightCTF-2024/assets/150792650/1cdd870b-256b-4be7-9906-9eb91cdbdcf0)


Upon inspecting the page sources, it wasn't obvious at first but when trying to give username and password input as **Username** and **Password** (as it is in the index file), we login to the page.

![Screenshot (13)](https://github.com/Wixter07/KnightCTF-2024/assets/150792650/2a6eba30-ecc6-4cff-b6ae-8b98670e135e)

On inspecting this page, we can see the command **`cat flag.txt`**.

![Screenshot (14)](https://github.com/Wixter07/KnightCTF-2024/assets/150792650/33fad2cf-5aeb-464e-adf0-fb43489f7d39)

So if we remember in the second image, the input dialogue had an execute button, which suggestes that **cat flag.txt** maybe the right input. So I executed the command and got the flag.

![Screenshot (15)](https://github.com/Wixter07/KnightCTF-2024/assets/150792650/e5f520bd-9f84-42a1-bba5-f6e190040fee)

The flag - **`KCTF{Fram3S_n3vE9_L1e_4_toGEtH3R}`**
