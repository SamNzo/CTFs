# Cryptanalyse

## Bébé nageur

### Intro

```py
import random as rd

charset = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789{}_-!"

def gcd_extended(a, b):
    if a == 0:
        return (b, 0, 1)
    else:
        gcd, x, y = gcd_extended(b % a, a)
        return (gcd, y - (b // a) * x, x)

def mod_inverse(a, m):
    gcd, x, _ = gcd_extended(a, m)
    if gcd != 1:
        raise Exception("Modular inverse does not exist")
    else:
        return x % m

def f_inverse(a, b, n, x):
    inverse_a = mod_inverse(a, n)
    return (inverse_a * (x - b)) % n

def encrypt(message, a, b, n):
    encrypted = ""
    for char in message:
        x = charset.index(char)
        x = f(a, b, n, x)
        encrypted += charset[x]
    return encrypted

def decrypt(ciphertext, a, b, n):
    decrypted = ""
    for char in ciphertext:
        x = charset.index(char)
        x = f_inverse(a, b, n, x)
        decrypted += charset[x]
    return decrypted

def brute_force_decrypt(ciphertext):
    n = len(charset)
    for a in range(2, n - 1):
        for b in range(1, n - 1):
            try:
                decrypted_message = decrypt(ciphertext, a, b, n)
                print("Possible decryption with a =", a, "and b =", b, ": ", decrypted_message)
            except Exception:
                continue

# Example usage:
ciphertext = "-4-c57T5fUq9UdO0lOqiMqS4Hy0lqM4ekq-0vqwiNoqzUq5O9tyYoUq2_"  # Replace this with the ciphertext you want to decrypt
brute_force_decrypt(ciphertext)
```

```shell
python3 exploit.py | grep 404
Possible decryption with a = 19 and b = 6 :  404CTF{Th3_r3vEnGE_1S_c0minG_S0oN_4nD_w1Ll_b3_TErRiBl3_!}
```

**404CTF{Th3_r3vEnGE_1S_c0minG_S0oN_4nD_w1Ll_b3_TErRiBl3_!}**
