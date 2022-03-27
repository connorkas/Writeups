# keygenme-py
## Description
> [keygenme-trial.py](https://mercury.picoctf.net/static/a6d9cac3bfa4935ceb50c145d3ff5586/keygenme-trial.py)

## Approach
The way I always like to start my CTF challenges is by running the script (if applicable) given to us, once we run the script we're given the following output:
```
===============================================
Welcome to the Arcane Calculator, PRITCHARD!

This is the trial version of Arcane Calculator.
The full version may be purchased in person near
the galactic center of the Milky Way galaxy.
Available while supplies last!
=====================================================


___Arcane Calculator___

Menu:
(a) Estimate Astral Projection Mana Burn
(b) [LOCKED] Estimate Astral Slingshot Approach Vector
(c) Enter License Key
(d) Exit Arcane Calculator
What would you like to do, PRITCHARD (a/b/c/d)?
```
Assuming that the locked portion is what we're after, selecting this option gives us the prompt: `You must buy the full version of this software to use this feature!`,
Since we don't know the license key off the bat, we're going to start our dive into the source code.<br>
One of the first pieces to take note of is this following code block:
```python
username_trial = "PRITCHARD"
bUsername_trial = b"PRITCHARD"

key_part_static1_trial = "picoCTF{1n_7h3_|<3y_of_"
key_part_dynamic1_trial = "xxxxxxxx"
key_part_static2_trial = "}"
key_full_template_trial = key_part_static1_trial + key_part_dynamic1_trial + key_part_static2_trial
```
We're given the majority of the key in the string `key_full_template_trial`, but we have to decode the `xxxxxxxx` portion (also referred to as `key_part_dynamic1_trial`). 
Scrolling down further into the script, we find the function `check_key()`:
```python
def check_key(key, username_trial):

    global key_full_template_trial

    if len(key) != len(key_full_template_trial):
        return False
    else:
        i = 0
        for c in key_part_static1_trial:
            if key[i] != c:
                return False
            i += 1
        if key[i] != hashlib.sha256(username_trial).hexdigest()[4]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[5]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[3]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[6]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[2]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[7]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[1]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[8]:
            return False

        return True
```
Looking at this function, we can see it takes each letter of the `username_trial` variable (string = "PRITCHARD"), encodes it into [SHA256](https://www.n-able.com/blog/sha-256-encryption),
then selects a single letter from the hash. I wrote a short script to decode the rest of the flag as shown here:
```python
import hashlib
username = "PRITCHARD"
obj = hashlib.sha256(str(username).encode('utf-8'))
print('Decrypt: ', obj.hexdigest()[4]+ obj.hexdigest()[5] + obj.hexdigest()[3] + obj.hexdigest()[6] + obj.hexdigest()[2] + obj.hexdigest()[7] + obj.hexdigest()[1] + obj.hexdigest()[8])
```
Running this script will then give us the output of `54ef6292`, and if we replace our original `xxxxxxxx` string with that, we're given the correct flag for this challenge.

## Flag
> picoCTF{1n_7h3_|<3y_of_54ef6292}
