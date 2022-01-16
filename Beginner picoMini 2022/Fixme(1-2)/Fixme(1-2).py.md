```diff
! These challenges are quite small, so both CTF writeups are going to be stored within this file.
```
# fixme1.py
## Description
> Fix the syntax error in this Python script to print the flag.<br>
> [Download Python script](https://artifacts.picoctf.net/c/38/fixme1.py)

## Approach
In this challenge, we're given a file with a clear objective: fix the syntax error. Upon running this script, we're given the following output:
```bash
  File "fixme1.py", line 20
    print('That is correct! Here\'s your flag: ' + flag)
    ^
IndentationError: unexpected indent
```
The error `IndentationError` refers to incorrect formatting within the file, so using your favorite text editor (I use Vim), we can access and adjust our script.
The code block we're looking for is located directly at the bottom, and all you need to do is hit backspace to correct the indentation, it should look something like this:
```python
flag = str_xor(flag_enc, 'enkidu')
print('That is correct! Here\'s your flag: ' + flag)
```
After running our script once more, we're given the correct flag!

## Flag
> picoCTF{1nd3nt1ty_cr1515_09ee727a}
***
# fixme2.py
## Description
> Fix the syntax error in the Python script to print the flag.
> [Download Python script](https://artifacts.picoctf.net/c/66/fixme2.py)

## Approach
Similar to the previous challenge, we're given a python file and tasked with fixing a syntax error. Running our fixme2.py file gives us the following error:
```bash
  File "fixme2.py", line 22
    if flag = "":
            ^
SyntaxError: invalid syntax
```
With the `SyntaxError` that we have just been given, it's saying our usage of an 'equal' operator is incorrect, but why is that? In Python, a single `=` sign is used as an assignment operater,
and because we're checking the variable flag against a string instead of assigning it, we need to use an equality operator. In python, it's as simple as adding another `=` sign to our if statement.<br>
Afterwards, our block of code should look something like this:
```python
if flag == "":
  print('String XOR encountered a problem, quitting.')
else:
  print('That is correct! Here\'s your flag: ' + flag)
```
After fixing this code and running our script, we're given our flag.

## Flag
> picoCTF{3qu4l1ty_n0t_4551gnm3nt_4863e11b}
