# Golden Ticket

So we've been given this code 

```python
from Crypto.Util.number import *

#Some magic from Willy Wonka
def chocolate_generator(m:int) -> int:
    p = 396430433566694153228963024068183195900644000015629930982017434859080008533624204265038366113052353086248115602503012179807206251960510130759852727353283868788493357310003786807
    return (pow(13, m, p) + pow(37, m, p)) % p

#The golden ticket is hiding inside chocolate
flag = b"idek{REDACTED}"
golden_ticket = bytes_to_long(flag)
flag_chocolate = chocolate_generator(golden_ticket)
chocolate_bag = []

#Willy Wonka is making chocolates
for i in range(golden_ticket):
    chocolate_bag.append(chocolate_generator(i))

#And he put the golden ticket at the end
chocolate_bag.append(flag_chocolate)

#Augustus ate lots of chocolates, but he can't eat all cuz he is full now :D
remain = chocolate_bag[-2:]

#Can you help Charles get the golden ticket?
print(remain)

#[88952575866827947965983024351948428571644045481852955585307229868427303211803239917835211249629755846575548754617810635567272526061976590304647326424871380247801316189016325247, 67077340815509559968966395605991498895734870241569147039932716484176494534953008553337442440573747593113271897771706973941604973691227887232994456813209749283078720189994152242]
```


So in short what it's doing is taking the flag and converting it to long and then it's generating values till `golden_ticket` using the `chocolate_generator` function and appended them to `chocolate_bag`.
We have with us the last two values from the `chocolate_bag` which was generated from the flag and the value before it.


I initially thought of this equation 

```
chocolate_bag[-2] - chocolate_bag[-1] = (((13^(golden_ticket-1) - 13^(golden_ticket)) + (37^(golden_ticket-1) - 37^(golden_ticket))) % p = 21875235051318387997016628745956929675909175240283808545374513384250808676850231364497768809056008253462276856846103661625667552370748703071652869611661630964722595999022173005
```


But there was a better approach 

The challenge boils down to two equations 

```
c1 = 13^flag + 37^flag %p
c2 = 13^(flag-1) + 37^(flag-1)  %p
```

Make it simpler by these substitutions 

```
x = 13^(flag-1)
y = 37^(flag-1)

```

Which gives us two simpler eqns


```

c1 = 13x + 37y  %p
c2 = x + y      %p

```

We can boil it to one equation by substituting x in c1 using x from c2

So that would be 

``` x = c2 - y %p ```

Putting this in c1 and on simplifying we get 

```24y = 13c2 - c1 %p```
This is where I could get till but then dhruthi later came on and said that doing mod inverse 24 on both side would eliminate 24 on the left and you'd have y. That made so much sense

Now after multiplying with mod inverse of 24 on both side, the eqn becomes

```y = (13c2 - c1) * modinv(24,p)  %p```

And now it turns into a discrete log problem which can be solved on [alpertron](https://www.alpertron.com.ar/DILOG.HTM)

```y = 13^(flag-1) % p```


That's how much I was able to get till. I was invested in another challenge and Madhav took care of this one and made the script. Now here's my implementation of the solve script

```python
from Crypto.Util.number import *

remain = [88952575866827947965983024351948428571644045481852955585307229868427303211803239917835211249629755846575548754617810635567272526061976590304647326424871380247801316189016325247, 67077340815509559968966395605991498895734870241569147039932716484176494534953008553337442440573747593113271897771706973941604973691227887232994456813209749283078720189994152242]
c1 = remain[-1]
c2 = remain[-2]
p = 396430433566694153228963024068183195900644000015629930982017434859080008533624204265038366113052353086248115602503012179807206251960510130759852727353283868788493357310003786807
    

a = 24
inv = pow(a, -1, p)
print("The mod inverse of 24 is " + str(inv))
 
dlog = int("57629776445896163024735745086814515288454966100802334039751672315837361336412607584713634047210889596") + 1    
print(long_to_bytes(dlog))  
```

The inverse was `-1` so added one to the result.

The flag - `idek{charles_and_the_chocolate_factory!!!}`

## Learning
 - The inverse of mod 24 made a lot of sense. It should've been common knowledge but it's fine. We learn.




