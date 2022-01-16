# PW Crack 4
## Description
> Can you crack the password to get the flag?
> Download the password checker [here](https://artifacts.picoctf.net/c/62/level4.py) and you'll need the encrypted [flag](https://artifacts.picoctf.net/c/62/level4.flag.txt.enc) and the [hash](https://artifacts.picoctf.net/c/62/level4.hash.bin) in the same directory too.
> There are 100 potential passwords with only 1 being correct. You can find these by examining the password checker script.

## Approach
I began by inspecting the `level4.py` file that was given and looked for the <b>level_4_pw_check()</b> function as the format of these challenges have all been similar. This challenge is incredibly similar to the previous PW Crack 3, but the only difference is the amount of password possibilities.
```
# The strings below are 100 possibilities for the correct password.
#   (Only 1 is correct)
pos_pw_list = ["6b3e", "989c", "4b17", "d06f", "f495", "6ea1", "44e4", "1d45", "3e1a", "b0b4", "8c65", "3276", "c496", "9d3d", "2476", "6ef4", "6b7f", "c184", "c2a8", "9708", "7bea", "9a2d", "4a22", "93ae", "826b", "9a50", "8b39", "5410", "a86c", "3760", "6426", "ec8e", "c294", "a909", "cbc6", "2e75", "f137", "9cb3", "79e7", "469f", "a9f9", "3e37", "b33e", "3f31", "4b27", "2f06", "cc2f", "d9e4", "2de7", "7328", "b4d4", "8e74", "a677", "b139", "9c74", "8ea4", "36f6", "613b", "7a7a", "5710", "838c", "44d5", "7190", "99d9", "c0a6", "b218", "3223", "477e", "38e5", "19b4", "3267", "2287", "b947", "a8d0", "fd9c", "e99c", "d8b7", "4c82", "b289", "332b", "bba5", "716d", "653e", "eb5d", "ad77", "ad3a", "3922", "7565", "947d", "928c", "2937", "823f", "f362", "79cf", "4582", "c0d0", "ed20", "d89a", "129c", "4e81"]
```
I knew that the previous approach of manually bruteforcing the amount of combinations wasn't going to work here, so I decided to modify my original approach.<br><br>
I started by cloning the original file using the command `mv level4.py decrypt.py` just to keep everything clean, and created a for loop to automatically check each possible password. One of the most important things to remember with this challenge is that our correct flag stored in `level4.flag.txt.enc` is encrypted and is decrypted through the .decode() funtion within our <b>level_4_pw_check()</b> function.
So in our created for loop we have to encrypt each line to verify we've found the correct string within the array. <br>

I've modified the original function to comment lines that no longer had use, such as the `user_pw` & `user_pw_hash` variables because we won't need these assigned before our for loop.
I then moved the array string above this function so the script can recognize it and actually read from the list.<br>

After cleaning up and formatting, I began to work on our actual for loop. <br>
For each iteration of the loop, I compared it to the `correct_pw_hash` variable, and if it didn't match no result was produced and the function ran again. I then modified the decryption variable (`decryption = str_xor(flag_enc.decode(), x)`) to subsitite our current iteration of the loop to ensure the correct string was being used.<br>
<br>After making all of these changes, my modified code looked like this:
```python
pos_pw_list = ["6b3e", "989c", "4b17", "d06f", "f495", "6ea1", "44e4", "1d45", "3e1a", "b0b4", "8c65", "3276", "c496", "9d3d", "2476", "6ef4", "6b7f", "c184", "c2a8", "9708", "7bea", "9a2d", "4a22", "93ae", "826b", "9a50", "8b39", "5410", "a86c", "3760", "6426", "ec8e", "c294", "a909", "cbc6", "2e75", "f137", "9cb3", "79e7", "469f", "a9f9", "3e37", "b33e", "3f31", "4b27", "2f06", "cc2f", "d9e4", "2de7", "7328", "b4d4", "8e74", "a677", "b139", "9c74", "8ea4", "36f6", "613b", "7a7a", "5710", "838c", "44d5", "7190", "99d9", "c0a6", "b218", "3223", "477e", "38e5", "19b4", "3267", "2287", "b947", "a8d0", "fd9c", "e99c", "d8b7", "4c82", "b289", "332b", "bba5", "716d", "653e", "eb5d", "ad77", "ad3a", "3922", "7565", "947d", "928c", "2937", "823f", "f362", "79cf", "4582", "c0d0", "ed20", "d89a", "129c", "4e81"]

def level_4_pw_check():
    #user_pw = input("Please enter correct password for flag: ")
    #user_pw_hash = hash_pw(user_pw)

    for x in pos_pw_list:
        if( hash_pw(x) == correct_pw_hash ):
            print("Welcome back... your flag, user:")
            decryption = str_xor(flag_enc.decode(), x)
            print(decryption)
            return
   # print("That password is incorrect")
```
Since we commented out the `input()` function, the script will automatically determine when `x` is a correct match for `correct_pw_hash`.<br>Afterwards, it will display our flag as if we typed in the correct string.

## Flag
> picoCTF{fl45h_5pr1ng1ng_89490f2d}
