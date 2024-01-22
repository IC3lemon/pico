 ```
  _____                                 __                                      _     _                 
 |_   _|  _ __    __ _   _ __    ___   / _|   ___    _ __   _ __ ___     __ _  | |_  (_)   ___    _ __  
   | |   | '__|  / _` | | '_ \  / __| | |_   / _ \  | '__| | '_ ` _ \   / _` | | __| | |  / _ \  | '_ \ 
   | |   | |    | (_| | | | | | \__ \ |  _| | (_) | | |    | | | | | | | (_| | | |_  | | | (_) | | | | |
   |_|   |_|     \__,_| |_| |_| |___/ |_|    \___/  |_|    |_| |_| |_|  \__,_|  \__| |_|  \___/  |_| |_|

```
****

## > Description
`I wonder what this really is... enc ''.join([chr((ord(flag[i]) << 8) + ord(flag[i + 1])) for i in range(0, len(flag), 2)])`

****

## > Solution

We're given with a file `enc`.\
It had some chinese/bengali cusswords, \
[enc.txt](https://github.com/IC3lemon/pico/files/14009395/enc.txt)

```
灩捯䍔䙻ㄶ形楴獟楮獴㌴摟潦弸彤㔲挶戹㍽
```
I'm guessing I gotta decode that somehow, \
the one liner code they gave in the challenge seems like some form of encoding method.\
it's prolly what was used to ***transform*** our flag into the chinese unicorn poo.

So I'm gonna try and reverse engineer this shit:\
`''.join([chr((ord(flag[i]) << 8) + ord(flag[i + 1])) for i in range(0, len(flag), 2)])`

it was easy enough, I cooked this :\

```python
enc = "灩捯䍔䙻ㄶ形楴獟楮獴㌴摟潦弸彤㔲挶戹㍽"
flag = ""
for i in range(0,len(enc)):
    char1 = chr(ord(enc[i])>>8)
    char2 = chr(enc[i].encode('utf-16be',"ignore")[1])
    flag += char1
    flag += char2

print(flag)
```

and nigga worked

****

### > Flag  - `picoCTF{16_bits_inst34d_of_8_d52c6b93}`


****
