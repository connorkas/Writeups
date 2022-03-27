# PW Crack 2
## Description
> Can you crack the password to get the flag?
> Download the password checker [here](https://artifacts.picoctf.net/c/17/level2.py) and you'll need the encrypted [flag](https://artifacts.picoctf.net/c/17/level2.flag.txt.enc) in the same directory too.

## Approach
I started by running the file to see how the script behaves, upon running `python3 level2.py`, we recieve the following output: <br>`Please enter correct password for flag:`<br>
<br>Entering a random string of characters gives us the output `That password is incorrect`, so now I'll use `cat` to view the script.<br> 
Just like the previous PW Crack, the function we want to look for is <b>level_2_pw_check()</b><br>
The function contains the following code:
```python
def level_2_pw_check():
    user_pw = input("Please enter correct password for flag: ")
    if( user_pw == chr(0x34) + chr(0x65) + chr(0x63) + chr(0x39) ):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
    print("That password is incorrect")
```
The main thing we're looking for when solving these CTF challenges is what checking mechanism does the script use to verify the password. Looking at this script, it checks if the variable <b>user_pw</b> is equal to a collection of chr() functions.<br>
From [w3schools](https://www.w3schools.com/python/ref_func_chr.asp), the chr() function is described as:
```
The chr() function returns the character that represents the specified unicode.
```
Knowing this, we can make our life easier by using [CyberChef](https://gchq.github.io/CyberChef/#recipe=From_Charcode('Space',16)&input=MHgzNCAweDY1IDB4NjMgMHgzOQ) to covert the unicode into readable ASCII text.<br>
Losing the chr() function we're left with `0x34 0x65 0x63 0x39`, and when coverted we recieve the output `4ec9`<br>
After inputting the ASCII output into the password field, we're given the flag.

## Flag
> picoCTF{tr45h_51ng1ng_9701e681}
