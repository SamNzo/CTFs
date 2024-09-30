# 1 - frog

## Prompt
> Welcome to Flare-On 11! Download this 7zip package, unzip it with the password 'flare', and read the README.txt file for launching instructions. It is written in PyGame so it may be runnable under many architectures, but also includes a pyinstaller created EXE file for easy execution on Windows.
>
>Your mission is get the frog to the "11" statue, and the game will display the flag. Enter the flag on this page to advance to the next stage. All flags in this event are formatted as email addresses ending with the @flare-on.com domain.

## Solution

The flag is decrypted if the frog is standing on the winning block next to the statue. 

```python
# are they on the victory tile? if so do victory
if player.x == victory_tile.x and player.y == victory_tile.y:
    victory_mode = True
    flag_text = GenerateFlagText(player.x, player.y)

[...]

def GenerateFlagText(x, y):
    key = x + y*20
    encoded = "\xa5\xb7\xbe\xb1\xbd\xbf\xb7\x8d\xa6\xbd\x8d\xe3\xe3\x92\xb4\xbe\xb3\xa0\xb7\xff\xbd\xbc\xfc\xb1\xbd\xbf"
    return ''.join([chr(ord(c) ^ key) for c in encoded])
```

The coordinates of the winning block are used to create the key. Considering that the x and y coordinates go from 0 to 17 a simple for loop does the job.

```python
encoded = "\xa5\xb7\xbe\xb1\xbd\xbf\xb7\x8d\xa6\xbd\x8d\xe3\xe3\x92\xb4\xbe\xb3\xa0\xb7\xff\xbd\xbc\xfc\xb1\xbd\xbf"
for x in range(17):
    for y in range(17):
        key = x + y*20
        flag = ''.join([chr(ord(c) ^ key) for c in encoded])
        if "@flare-on.com" in flag:
            print(flag)
```

**welcome_to_11@flare-on.com**
