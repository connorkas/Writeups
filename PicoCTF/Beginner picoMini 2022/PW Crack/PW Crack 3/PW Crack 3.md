# PW Crack 3
## Description
> Can you crack the password to get the flag?
> Download the password checker [here](https://artifacts.picoctf.net/c/25/level3.py) and you'll need the encrypted [flag](https://artifacts.picoctf.net/c/25/level3.flag.txt.enc) and the [hash](https://artifacts.picoctf.net/c/25/level3.hash.bin) in the same directory too.
> There are 7 potential passwords with 1 being correct. You can find these by examining the password checker script.

## Approach
After running the script and recieving the output `Please enter correct password:`, we know this challenges has the same format as the previous PW Crack challenges. Unlike the previous challenges, when inspecting the <b>level_3_pw_check()</b> function, the user input is matched against the password hash we have been provided with for this challenge.
Thankfully, the author of this challenge provided us with 7 possibilities for the correct password, as shown in an array.
```python
# The strings below are 7 possibilities for the correct password.
#   (Only 1 is correct)
pos_pw_list = ["8799", "d3ab", "1ea2", "acaf", "2295", "a9de", "6f3d"]
```
We can make things easier by manually bruteforcing each possible password combination. After a few attempts, the correct password is `1ea2`.<br>
Inputting `1ea` will give us the flag for this challenge.

## Flag
> picoCTF{m45h_fl1ng1ng_6f98a49f}
