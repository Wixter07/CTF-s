# OS

The challenge was to find the OS version of the memory dump. These memory dumps contain some information about a System Crash and a copy of the System memory at the time of crash. Opened the memory dump file on WinDbg previewer and used **`!analyze -v`** command on the command window which analyzes the memory dump and gives out information about it. This info also contains the OS version.

![Screenshot (9)](https://github.com/Wixter07/KnightCTF-2024/assets/150792650/f6da8e1b-60ee-45e1-937f-4b31be5abd5e)

flag - **`KCTF{7.1.7601.24214}`**
