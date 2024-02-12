# rps-casino

We have with us a rock-paper-scissor game. We get 56 free trials and to get the flag, we need to win 50 consecutive time against the computer generated choice.
The choice is being yielded from LFSR.
I went through this video from [Computerphile](https://www.bing.com/ck/a?!&&p=518b014e9937ee54JmltdHM9MTcwNzY5NjAwMCZpZ3VpZD0zOTZmMjkxOC0zYjgxLTYwNWYtMDU1Yi0zZDE4M2E3NjYxYmUmaW5zaWQ9NTgzMg&ptn=3&ver=2&hsh=3&fclid=396f2918-3b81-605f-055b-3d183a7661be&u=a1L3ZpZGVvcy9yaXZlcnZpZXcvcmVsYXRlZHZpZGVvP3E9d2hhdCtpcytMRlNSJm1pZD02N0U5MjcyMzc1MjY0QURDQjA4NjY3RTkyNzIzNzUyNjRBRENCMDg2JkZPUk09VklSRQ&ntb=1)
to understand how LFSR works. His code implementation is very similar to how the code for the challenge looks.

## LFSR (Linear Feedback Shift Register)

A linear-feedback shift register (LFSR) is a shift register whose input bit is a linear function of its previous state.

The most commonly used linear function of single bits is exclusive-or (XOR). Thus, an LFSR is most often a shift register whose input bit is driven by the XOR of some bits of the overall shift register value.

### The challenge

So the challenge used this implementation of LFSR


    def LFSR():

	state = bytes_to_long(os.urandom(8))
 
	while 1:
 
		yield state & 0xf
  
		for i in range(4):
  
			bit = (state ^ (state >> 1) ^ (state >> 3) ^ (state >> 4)) & 1
   
			state = (state >> 1) | (bit << 63)
   
   
The state variable hold a random 8 byte string generated from **urandom** which is converted into long.
We run four loops where we operate on the state by XORing the values obtained from a series of bitwise operations, this later is &ed with 1 to obtain the last value in from the bits.
The state is then updated again.
The yield statement can be understood as a return statement wherein we & our obtained value with 15.

The LFSR value after each win,loose or tie changes. I printed the LFSR values (printing state) by modifying the code and also tried printing the computer choices before I give my input.
For the computer,

**0 = Rock** 
**1 = Paper** 
**2 = Scissors**

So I used the modified code to win the 56 trial and the later 50 wins. I tried looking for some relation between how the next LFSR value is being generated. If only we can notice some pattern deciding the next LFSR value, we can write a script to win the game.
   
