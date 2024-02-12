# baby-asm 

So we get a URL which takes us to a page and the input console read **"Input the password"**. On a random input, the output read "Incorrect". Inspecting the page sources, we have a html and Web Assembly file. Going through the html file, we can see that the input for password is supposed to be our flag as **TetCTF{}** and the password length is of 27 characters. **TetCTF{}** itself makes up 7 characters, so we need 20 characters that come inside the braces.



On analyzing the Web Assembly file, there are 20 global variables and they all go through some calculations in 5 different functions. The variables were initialized with some values and it's probable that at some point these values maybe converted to ascii. 

![Screenshot (18)](https://github.com/Wixter07/TetCTF-2024/assets/150792650/aaa3022c-caf6-4535-b555-60181efe6a08)

Then in the first function, the values in the global variables were XOR'ed with some other values and the output was placed in an array.

The array now is **[115, 82, 52, 149, 136, 67, 76, 97, 71, 90, 71, 74, 124, 104, 84, 67, 114, 127, 52, 31]**

Then in the array fill function, what I believe to be happening is that **19** is being added to each values in the variable and 64 is being deducted from each value. Or it could also be possible that 64 is being added since the code say its **-64** and is being subtracted, so basically 64 is being added.

![Screenshot (19)](https://github.com/Wixter07/TetCTF-2024/assets/150792650/89e6b5b3-4a7b-40ac-a39f-4c15980d52db)

Then again in function 3, these values are being loaded to an array


I couldn't proceed further since it was my first time going through web assembly. But by a look at it, we can make out that these values are being further made to go through some other mathematical operations. I also couldn't understand how the check function is working, can't figure out where these values are being converted from decimal to ASCII or something else.
