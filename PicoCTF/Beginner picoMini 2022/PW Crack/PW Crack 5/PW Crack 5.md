# PW Crack 5
## Description
> Can you crack the password to get the flag?
> Download the password checker [here](https://artifacts.picoctf.net/c/83/level5.py) and you'll need the encrypted [flag](https://artifacts.picoctf.net/c/83/level5.flag.txt.enc) and the [hash](https://artifacts.picoctf.net/c/83/level5.hash.bin) in the same directory too. Here's a [dictionary](https://artifacts.picoctf.net/c/83/dictionary.txt) with all possible passwords based on the password conventions we've seen so far.

## Approach
If you've already completed the previous 4 PW Crack challenges, you'll know the general structure of how these challenges work. Thankfully, we did most of the hard work in the previous challenge ([PW Crack 4](https://github.com/connorkas/picoCTF-Writeups/blob/main/Beginner%20picoMini%202022/PW%20Crack/PW%20Crack%204/PW%20Crack%204.md))
<br>The main difference between the previous challenge and this one, is that our possible combinations are stored within a file called `dictionary.txt`. We'll have to open this file, run through the possible iterations with a for loop and determine the correct 4 character string.
<br><br>
I began this challenge by duplicating the original python file using `cp level5.py decrypt5.py` and begun working on the seperate file to keep things clean.<br>
I created a variable titled `lines` under `flag_enc` & `correct_pw_hash` then loaded the `dictionary.txt` file into it.
```python
flag_enc = open('level5.flag.txt.enc', 'rb').read()
correct_pw_hash = open('level5.hash.bin', 'rb').read()
lines = open('dictionary.txt', 'r').read().split('\n')
```
Because we're not working with a predetermined array like before, we need to let python know how we'll choose to split lines. Using `\n` as a delimiter allows us to register each line as an item in our for loop.
<br> There's one more thing we need to do before we can run this script. We can re-use the same for loop as PW Crack 4 but with a few modifications. Initially, we need to change where the for loop is pulling this information, it'll look something like this:
```python
for x in lines:
```
But before we create our for loop again, we have to make one addition. We have to add `x = x.strip()` in order to remove any possible trailing whitespaces within our strings. If we didn't, the decryption algorithm would register the whitespaces and it wouldn't be able to match our `correct_pw_hash` variable.<br>
After all of these additions, our for loop should look something like this.
```python
def level_5_pw_check():
    #user_pw = input("Please enter correct password for flag: ")
    #user_pw_hash = hash_pw(user_pw)

    for x in lines:
        x = x.strip()
        if( hash_pw(x) == correct_pw_hash ):
            print("Welcome back... your flag, user:")
            decryption = str_xor(flag_enc.decode(), x)
            print(decryption)
            return
    #print("That password is incorrect")
```
Like before, since we commented out `user_pw` & `user_pw_hash`, the script will automatically run as if we typed in the correct string. After running our decrypt script, we will recieve the correct flag.
## Flag
> picoCTF{h45h_sl1ng1ng_2f021ce9}
