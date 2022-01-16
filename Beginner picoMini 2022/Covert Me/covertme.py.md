# covertme.py
## Description
> Run the Python script and convert the given number from decimal to binary to get the flag.<br>
> [Download Python script](https://artifacts.picoctf.net/c/36/convertme.py)

## Approach
We're given clear directions and a python script in order to move forward, so let's start this CTF challenge by running the script.
```
python3 covertme.py
```
After running the script, we're given the following prompt:<br>
`If 97 is in decimal base, what is it in binary base?
Answer:`<br>

<b>Just to note for this challenge, the number given (in this case `97`) is variable and changes each time you run this script.</b><br>
Moving forward with that, we can use our friend Google and look for a decimal conversion to binary conversion. Googling "decimal base to binary" brings us to a site called [RapidTables](https://www.rapidtables.com/convert/number/decimal-to-binary.html),
which is very useful site when you decide to move forward in other CTF challenges. After inputting our number `97` into the conversion, we're given the binary number `1100001`.<br>
<br>Returning to our script once more, when we input our binary number we're then given the flag.

## Flag
> picoCTF{4ll_y0ur_b4535_e2a58836}
