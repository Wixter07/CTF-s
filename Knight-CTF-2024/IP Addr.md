# IP Addr

So we need to find the IP Address of the machine from the memory dump. I had to look online if there we any ways to find the IP Address of the machine from the memory dump file and came across this online discussion from 2011 about [How to get IP address in WinDbg](https://community.osr.com/discussion/214844/how-to-get-ip-address-in-windbg). 

![Screenshot (17)](https://github.com/Wixter07/KnightCTF-2024/assets/150792650/cfea8757-9550-4e3b-b1b1-6eb9c7cf594a)

Opened the dump file on WinDbg and gave the commands as suggested by the user **Bruce_Dang** from the discussion forum. Didn't get the IP Address at first but after pressing enter a few times, I got the IP Address.

![Screenshot (9)](https://github.com/Wixter07/KnightCTF-2024/assets/150792650/32087316-fcb8-4d80-9b0b-6d6efd8080f8)

I didn't understand how pressing enter a few times gave out the IP Address, but as per my understanding, pressing enter moved across the addresses and read out what's stored in that address. I'll update this writeup after I learn about what's really going on.

The flag - **`KCTF{10.0.2.15}`**
