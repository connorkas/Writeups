```diff
! The challenges listed below don't have as much depth as the other ones,
! so they'll be combined into this single .md file.

- None of these challenges require file modification, so no files will be uploaded to this repo.

+ If you have any questions, comments, or anything please reach out to me over at: connor@aaathats3as.com
```
# runme.py
## Description
> Run the `runme.py` script to get the flag. Download the script with your browser or with `wget` in the webshell.<br>
> [Download runme.py Python script](https://artifacts.picoctf.net/c/92/runme.py)

## Approach
Since this our first CTF challenge of the competition, this one is pretty easy! All we have to do is download this file to our current directory using `wget https://artifacts.picoctf.net/c/92/runme.py`, and then execute the script using python.
```
python3 runme.py
```
After running this script, we're given the flag! If you're curious about how this script works, you can just use `cat` to view the contents of the file:
```python
#!/usr/bin/python3
################################################################################
# Python script which just prints the flag
################################################################################

flag ='picoCTF{run_s4n1ty_run}'
print(flag)
```

## Flag
> picoCTF{run_s4n1ty_run}
***

# ncme
## Description
> Connect to a remote computer using `nc` and get the flag.<br>
> `$ nc saturn.picoctf.net 57688`

## Approach
In this challenge, we're given clear directions and a command to type into our Linux CLI. If you're unfamilar with netcat, be sure to check out their man page, or [view this web version](https://www.commandlinux.com/man-page/man1/nc.1.html)
<br><br>After running this command, we're immediately given the flag. 

## Flag
> picoCTF{s4n1ty_c4t}
***

# Codebook
## Description
> Run the Python script code.py in the same directory as codebook.txt.<br>
> • [Download code.py](https://artifacts.picoctf.net/c/103/code.py)<br>
> • [Download codebook.txt](https://artifacts.picoctf.net/c/103/codebook.txt)

## Approach
After downloading both of these files using `wget`, all we need to do is run code.py using the following command:
```
python3 code.py
```
If you haven't already guessed, our script `code.py` is reliant on the existance/contents of `codebook.txt`. The contents of the file reads:
```
azbycxdwevfugthsirjqkplomn
```
And when reviewing our script, we see that our script pulls letters from this string in a specific combination and then displays our flag.
```python
def print_flag():
  try:
    codebook = open('codebook.txt', 'r').read()

    password = codebook[4] + codebook[14] + codebook[13] + codebook[14] +\
               codebook[23]+ codebook[25] + codebook[16] + codebook[0]  +\
               codebook[25]

    flag = str_xor(flag_enc, password)
    print(flag)
```
It's worth noting that the flag is fully decrypted using the defined str_xor() function at the beginning of the script, but we don't need to pay attention to this function as it's outside the scope of this challenge.<br>
<br>Anyways, after running this script you'll recieve your flag!

## Flag
> picoCTF{c0d3b00k_455157_8100c7c1}
***

# HashingJobApp
## Description
> If you want to hash with the best, beat this test!<br>
> `nc saturn.picoctf.net 65352`

## Approach
Similar to our previous <b>ncme</b> challenge, we begin by connecting to a address via netcat. After entering this command, we're given the following information:
```
Please md5 hash the text between quotes, excluding the quotes: 'mold'
Answer:
```
Before anything else, it's worth noting **this challenge provides randomized options each time** you run this command.<br><br>
This challenge is asking us to provide the md5 hash equivalent to the provided string (in this case 'mold'), and submit it. Since netcat is taking up some terminal space,
we can use an online tool to help us out. After googling "string to MD5 hash", I was brought to the aptly named site "[MD5 Hash Generator](https://www.md5hashgenerator.com)".
After inputting 'mold' we're given the MD5 hash `0ad9f975892bdc82aa683146c002ffac`, and inputting this into our terminal gives us the simple response of `Correct.`.<br>
<br>
This challenge has you repeat this process for a total of three times, my next two matches are listed below:<br>
`chains` -> `99469f92ab96d54efce3d605a4bb4fbe`<br>
`Helen Keller` -> `c0aac1554fe46e67f218df124c318054`<br><br>
After successfully inputting our three corresponding MD5 hashes, we are given the flag for this challenge.

## Flag
> picoCTF{4ppl1c4710n_r3c31v3d_674c1de2}
