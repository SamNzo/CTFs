# Strike
## Reverse
### Intro

```python
def to_hex(char):
    if char == "0":
        return 0
    elif char == "1":
        return 1
    elif char == "2":
        return 2
    elif char == "3":
        return 3
    elif char == "4":
        return 4
    elif char == "5":
        return 5
    elif char == "6":
        return 6
    elif char == "7":
        return 7
    elif char == "8":
        return 8
    elif char == "9":
        return 9
    elif char == "a":
        return 10
    elif char == "b":
        return 11
    elif char == "c":
        return 12
    elif char == "d":
        return 13
    elif char == "e":
        return 14
    elif char == "f":
        return 15



def find_flag():
    possible_chars = "0123456789abcdef"

    to_check = "# congratulations! this is a strike :-) you should now see the flag printed ... #"
    charset = "abcdefghijklmnopqrstuvwxyz!# $:-()."

    flag = ""

    round_ok = False

    for i in range(0, 162, 2):
        for char1 in possible_chars:
            for char2 in possible_chars:
                val = ( 16*to_hex(char1) ) | to_hex(char2)
                if (0 | val) <= 0x23:
                    res = ( i + val ) % 0x23
                    if charset[res] == to_check[i//2]:
                        flag = flag + char1 + char2
                        round_ok = True
                        break
            if round_ok:
                round_ok = False
                break

    print(flag)

if __name__ == "__main__":
    find_flag()
```

```shell
┌──(kali㉿kali)-[~/…/fcsc/2024/reverse/strike]
└─$ ./strike 1b1a2108051f051503021a0d1e111512151b1b10020109111e030b10071e1d190e0e061c1c1b1b140e02060c00161b1f140a21100f15190d201e11061b160913170a0e221313080b0f211e121614120a07
[+] Nice! The flag is: FCSC{1b1a2108051f051503021a0d1e111512151b1b10020109111e030b10071e1d190e0e061c1c1b1b140e02060c00161b1f140a21100f15190d201e11061b160913170a0e221313080b0f211e121614120a07}
```

**FCSC{1b1a2108051f051503021a0d1e111512151b1b10020109111e030b10071e1d190e0e061c1c1b1b140e02060c00161b1f140a21100f15190d201e11061b160913170a0e221313080b0f211e121614120a07}**
