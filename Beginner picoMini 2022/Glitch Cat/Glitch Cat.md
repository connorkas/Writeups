# Glitch Cat
## Description
> Our flag printing service has started glitching!
> $ nc saturn.picoctf.net 52026

## Approach
Since our original description doesn't give us much to work with except for a netcat command, we'll start there!
After inputting `nc saturn.picoctf.net 52026` into our terminal, we are given only a string of text:
```
'picoCTF{gl17ch_m3_n07_' + chr(0x62) + chr(0x65) + chr(0x63) + chr(0x66) + chr(0x33) + chr(0x38) + chr(0x36) + chr(0x31) + '}'
```
If you're unfamiliar with the chr() python function, it simply returns an ascii character represented within Unicode.
We can create a python script to do the work for us rather than individually looking up Unicode characters.<br><br>

We can create a python file using the touch command, so I typed `touch decrypt.py` into my terminal, then used a command called `chmod` to modify the permissions of this file, without this our file couldn't be executed by us.
I used `chmod +x decrypt.py` to signify execute permissions for the file, then copied the original string of text we received after connecting to the picoCTF server via netcat.<br>
Using Vim, I wrote the following single line code:
```python
print('picoCTF{gl17ch_m3_n07_' + chr(0x62) + chr(0x65) + chr(0x63) + chr(0x66) + chr(0x33) + chr(0x38) + chr(0x36) + chr(0x31) + '}')
```
With the print() function, python will interpret our chr() function and convert these unicode markers into parsable ASCII.<br>
Running `python3 decrypt.py` will then give us our flag.

## Flag
> picoCTF{gl17ch_m3_n07_becf3861}
