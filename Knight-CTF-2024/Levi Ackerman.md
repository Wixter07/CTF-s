# Levi Ackerman

So the challenge is similar to **"where are the robots"** from picoCTF. We look for the **robots.txt** text file which tells the engine crawlers about which URL's the crawlers can access on the site. 
So we can just do **`http://66.228.53.87:5000/robots.txt`** .

![Screenshot (10)](https://github.com/Wixter07/KnightCTF-2024/assets/150792650/ea63d72f-1acb-405c-aa7a-bf81968fd308)

We can see that it disallows going to **/l3v1_4ck3rm4n.html** . So we can go there by **`http://66.228.53.87:5000/l3v1_4ck3rm4n.html`** , and it displays the flag.

![Screenshot (11)](https://github.com/Wixter07/KnightCTF-2024/assets/150792650/0ea8d05b-453d-4917-a5a0-953c5b1880e5)

flag - **`KCTF{1m_d01n6_17_b3c4u53_1_h4v3_70}`**
