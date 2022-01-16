# PW Crack 1
## Description
> Can you crack the password to get the flag?
> Download the password checker [here](https://artifacts.picoctf.net/c/51/level1.py) and you'll need the encrypted [flag](https://artifacts.picoctf.net/c/51/level1.flag.txt.enc) in the same directory too.
## Approach
For starters, I run a Windows 10 machine and I use WSL Ubuntu to complete my tasks.<br><br>
My initial approach to all CTF challenges that give you a Python file is to run it. Running `python3 level1.py` gives the output:<br>
`Please enter correct password for flag:`<br><br>
After typing in random characters and recieving the output `That password is incorrect`, I then used `cat` to view the code.<br>
After printing the code, we find that our main focus is on the level_1_pw_check() function. The code block reads:<br>
```python
def level_1_pw_check():
    user_pw = input("Please enter correct password for flag: ")
    if( user_pw == "691d"):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
    print("That password is incorrect")
```
Since this is the first rendition of five other "PW Crack" challenges, it seems this one was pretty easy! This script checks for the string `691d` as shown in the code block:
```python
if ( user_pw == "691d"):
```
If we return to our CLI, run the script, and type `691d` for our input, we get the following output which contains our flag:
```
Welcome back... your flag, user:
picoCTF{545h_r1ng1ng_56891419}
```
## Flag
> picoCTF{545h_r1ng1ng_56891419}
