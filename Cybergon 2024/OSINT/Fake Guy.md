# Fake Guy

Well our team first blooded this one. Was a tough one tbh.

## The Challenge

```
A guy from somewhere is pretending to be a member of our CYBERGON. He created several social media accounts by abusing our username. Some intel said he setup username by doing typo squatting. Please try to investigate and help me to track him down.

CYBERGON_CTF2024{Current City's IATA, Visiting City's IATA, Flight Number, Aircraft Type, Airline Name}

Author - iamkfromburma
```

# Solve

We have info that the guy is pretending to be a member of CYBERGON by creating several accounts by typo squatting. Let's consider it luck that I searched for `CYBERGOM_MM` instead of CYBERGON and got the [X](https://x.com/Cybergom_MM) handle. We will come to the hex in the bio later.

Then I ran sherlock with the username and got these results

```bash
[+] AskFM: https://ask.fm/Cybergom_MM
[+] Discord: https://discord.com
[+] HackenProof (Hackers): https://hackenproof.com/hackers/Cybergom_MM
[+] Instagram: https://instagram.com/Cybergom_MM
[+] Pastebin: https://pastebin.com/u/Cybergom_MM
[+] ProductHunt: https://www.producthunt.com/@Cybergom_MM
[+] SlideShare: https://slideshare.net/Cybergom_MM
[+] Strava: https://www.strava.com/athletes/Cybergom_MM
[+] Twitch: https://www.twitch.tv/Cybergom_MM
[+] Twitter: https://x.com/Cybergom_MM
[+] babyRU: https://www.baby.ru/u/Cybergom_MM/
[+] mastodon.cloud: https://mastodon.cloud/@Cybergom_MM
[+] threads: https://www.threads.net/@Cybergom_MM
```

The handles of interest are the Instagram and Pastebing accounts.

Back to the hex in the bio which was 

```
33 31 32 68 67 36 6f 63 6c 6c 6a 37 78 73 63 6a 73 6b 6f 6d 68 62 63 66 71 66 62 75
```

Which translates to

```
312hg6ocllj7xscjskomhbcfqfbu
```

Now if you analyse the X account a bit, you'd realize John Wick is following all the handles related to the challenge. But why Spotify?

Just raw searching **312hg6ocllj7xscjskomhbcfqfbu** gives us this [Instagram](https://www.instagram.com/312hg6ocllj7xscjskomhbcfqfbu/) account. This had a [Threads](https://www.threads.net/@cybergom_mm) account which inturn led to the Instagram account from the sherlock search.

![image](https://github.com/user-attachments/assets/e5bf6f4a-2a7b-4972-a97d-f11584ca95cb)

The secret code will come in handy soon


Unfortunately, couldn't find any spotify account just by searching for CYBERGOM, so I picked a random user and looked at the URL to realize the user identifier was somewhat of the same length as the hex. To test it out, I changed the user identifier to the the hex data and voila!, got the [Spotify](https://open.spotify.com/user/312hg6ocllj7xscjskomhbcfqfbu) handle.


Now on Spotify *My Favorites* playlist, you'd find more hex data.

![image](https://github.com/user-attachments/assets/f85d053d-687e-4873-8305-34c1d17bda83)


```63 79 62 67 6f 6e 2e 6d 6d 40 70 72 6f 74 6f 6e 2e 6d 65``` which translates to ```cybgon.mm@proton.me``` a mail id.


Only thing left to investigate now is the pastebin account.

![image](https://github.com/user-attachments/assets/2e75c98f-d3df-491e-934b-88f260518767)

So more hex data. Double Up is a hint that the message has been encoded to hex twice. So decoding it would give 

![image](https://github.com/user-attachments/assets/058021d6-ed62-4857-a7c0-2a26d4acce9c)

Now going to the author **iamkfromburma**, he'd give you a discord link to a server called **JW's Home**

There are two channels of interest here. First one is resources 

![image](https://github.com/user-attachments/assets/06fd9ac9-d997-42f8-b2f8-917592dab31b)

We have a .kdbx file with us now. Unfortunately not crackable by keepass2john as it doesn't support KDBX4 format.

Next the info channel

![image](https://github.com/user-attachments/assets/6d217707-7a1b-4d76-b143-af56dfad86f3)


So recall that we got the mail id from the Spotify account and the secret code from the threads account. So we mailed the id with the team details and got ther reply back

![image](https://github.com/user-attachments/assets/bc846881-36c9-48ff-81a7-9cd38fa7cb1e)


I opened the kdbx file with the password, and got a [Google Drive](https://drive.google.com/file/d/1Pf2OprsU3p0hLjvXhnk2i1GBmKUwjRg6/view) file with it. There is a Intel.rar file in it and can be unzipped with this ```7sX1qBFtqQyAe7p466nkpmawEjxfBm7262CKauDetBSM63Kzavfj7HR16xr83cMA``` password from the unlocked kdbx file.

The Intel folder had to files in it. A text file which read out 

```
Congrats !! You are almost closet to track him ;) 

We understand that you already possess some crucial details, such as the city he intends to visit and the earlier flight information.

Additionally, we have obtained an updated MAC address linked to his current city of residence. This visit is planned for Sunday, January 5, 2025.

With this updated intelligence, we are confident in our ability to intercept him this time.

Flag format:
CYBERGON_CTF2024{Current City's IATA, Visiting City's IATA, Flight Number, Aircraft Type, Airline Name}
```

And the image showing the mac address 


![MAC](https://github.com/user-attachments/assets/09d2faf1-8d67-4f52-99a1-37093121f8fe)


Searching for the MAC address on wigle.net would show that the current city of residence in Yangon and the IATA code for it is RGN

![image](https://github.com/user-attachments/assets/47e718d5-11cd-4120-b81f-cccab6560367)

Now a lot of you might be wondering, what was this picture from the X handle trying to communicate

![image](https://github.com/user-attachments/assets/22eed391-972b-4d5a-a3e4-0b23b13850c0)

Well it was indicating the Airlines that he was about to travel in which is Myanmar Airways International.

Next his destination. Recall that he posted a picture on his Instagram account, it had  a location in it. An image with hot air balloons. If you just open who he is following, you'll know of the location of the image 

![image](https://github.com/user-attachments/assets/6626b7c4-0a06-44e8-9e79-d28f4ddbcfc3)


Bagan it is. The closest airport to Bagan is Nyaung U Airport and the IATA code for it is NYU.

Now to bring it all together with the last search. If we search for flight scheduled to NYU from RGN on 05/01/2025 on Myanmar Airways International official portal, you'd get this 

![image](https://github.com/user-attachments/assets/601b1984-79fe-44a0-adb3-0b0d922d0c68)

So we have the flight number and the aircraft type and the airlines that operates it. 


All of this makes up our flag 

```CYBERGON_CTF2024{RGN, NYU, 8M-4214, AT7-600 68Y, AIR KBZ}```



Ngl this was one heck of a challenge. I felt ecstatic after solving this lmao.

