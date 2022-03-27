# Serpentine
## Description
> Find the flag in the Python script!<br>
> [Download Python script](https://artifacts.picoctf.net/c/95/serpentine.py)

## Approach
We're given direct instructions on how approach this problem, so let's run the python script before anything else. Running it gives us the following output:
```

    Y
  .-^-.
 /     \      .- ~ ~ -.
()     ()    /   _ _   `.                     _ _ _
 \_   _/    /  /     \   \                . ~  _ _  ~ .
   | |     /  /       \   \             .' .~       ~-. `.
   | |    /  /         )   )           /  /             `.`.
   \ \_ _/  /         /   /           /  /                `'
    \_ _ _.'         /   /           (  (
                    /   /             \  \
                   /   /               \  \
                  /   /                 )  )
                 (   (                 /  /
                  `.  `.             .'  /
                    `.   ~ - - - - ~   .'
                       ~ . _ _ _ _ . ~

Welcome to the serpentine encourager!


a) Print encouragement
b) Print flag
c) Quit

What would you like to do? (a/b/c)
```
Hitting the obvious option of (b), we're given the following text:
```
Oops! I must have misplaced the print_flag function! Check my source code!
```
Looking at this, we know we have to look into the source code. Using Vim we can access this file and figure out what's going on.<br>
At the bottom of the script, we see where our original choices stem from, and looking at the following line we now know a print() function is in place of the actual print_flag() we're hunting for.
```python
elif choice == 'b':
      print('\nOops! I must have misplaced the print_flag function! Check my source code!\n\n')
```
Scrolling up further in the script, we find the print_flag() function:
```python
def print_flag():
  flag = str_xor(flag_enc, 'enkidu')
  print(flag)
```
It seems pretty straightforward, so if we replace the previous print() function under choice b, our script should hopefully work.
```python
elif choice == 'b':
      print_flag()
```
Running the script again and choosing option b will run the correct function and give us our flag!

## Flag
> picoCTF{7h3_r04d_l355_7r4v3l3d_8e47d128}
