# Uzh

So we have a jar file. Going through the manifest after unzipping it, we learn that it is designed for mobile devices that support MIDP 2.0.

Going through the classes, it seems like a game.
We need to run it on a Java MicroEdition emulator.
I used **KEmulator** to run the game and gave the six digit secret code give in the challenge description to enter the game. So basically it's a snake game
Playing it and failing to win will give us the first flag.

![Screenshot (28)](https://github.com/Wixter07/ugra-CTF-2024/assets/150792650/b228bd13-5a08-4735-9a48-b30c3c63af01)

The flag - `ugra_send_via_infrared_0f5ed0`
