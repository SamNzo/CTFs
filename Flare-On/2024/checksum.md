# 2 - checksum

## Prompt
> We recently came across a silly executable that appears benign. It just asks us to do some math... From the strings found in the sample, we suspect there are more to the sample than what we are seeing. Please investigate and let us know what you find!

## Solution
The program starts with a joke asking us to check a few sums before the actual challenge starts. If any of the answers is incorrect the program stops.

After this part it asks for a checksum, giving the right one will reveal the flag. 

The program grabs encrypted data from its memory.
```go
[...]
encrypted_flag = main_encryptedFlagData;
[...]
```

Creates a file ``REAL_FLAREON_FLAG.JPG`` and write decrypted data inside.
```go
v122 = runtime_concatstring2(
           0,
           v227.len,
           v217,
           (unsigned int)"\\REAL_FLAREON_FLAG.JPG",
           22,
           v118,
           v119,
           v120,
           v121,
           v153,
           v172,
           *(__int64 *)buffer,
           *(__int64 *)&buffer[8]);
[...]
v127 = os_WriteFile(
           v122,
           v117,
           (int)v227.ptr,
           v215[0],
           v216[0],
           420,
           v124,
           v125,
           v126,
           v154,
           v173,
           *(_slice_uint8 *)buffer,
           0);
```

Our input is checked multiple times using the function ``main_b``. However, the writing to the file only happens if ``main_a`` which is called at the end returns ``1``.

Function ``main_a`` contains the interesting part. Each checksum byte is xored with a value obtained from a string ``FlareOn2024`` (indexes are obtained using arithmetic operations on an hardcoded value).
```go
[...]
for ( i = 0LL; size > i; ++i )
  {
    buffer_cpy = buffer;
    v17 = checksum_ptr_cpy;
    byte = i - 11 * ((__int64)((unsigned __int128)(i * (__int128)0x5D1745D1745D1746LL) >> 64) >> 2);
    checksum_byte = checksum_ptr_cpy[i];
    if ( byte >= 0xB )
      runtime_panicIndex(byte, i, 11LL, v17);
    str = "FlareOn2024";
    xor_byte = (unsigned __int8)aTrueeeppfilepi[byte + 3060];
    *(_BYTE *)(buffer_cpy + i) = xor_byte ^ checksum_byte;
    [...]
}
```

The resulting data is then base64 encoded and if the result is equal to another hardcoded value, the function returns 1.
```
v21 = encoding_base64__ptr_Encoding_EncodeToString(
          runtime_bss,
          buffer,
          size,
          size,
          buffer_cpy,
          (_DWORD)str,
          xor_byte,
          v12,
          v13,
          v23,
          v24,
          v25);
  if ( final_buffer == 88 )
    return runtime_memequal(
             v21,
             (__int64)"cQoFRQErX1YAVw1zVQdFUSxfAQNRBXUNAxBSe15QCVRVJ1pQEwd/WFBUAlElCFBFUnlaB1ULByRdBEFdfVtWVA==");
  else
    return 0LL;
```

We can simply build the correct checksum knowing the base64 encoded value:
- decode b64
- get each byte by xoring the resulting bytes with those from the string ``FlareOn2024``

```python
import base64

# The correct checksum we are looking for
checksum = ""

string = "FlareOn2024"

# Decode b64
encoded_str = "cQoFRQErX1YAVw1zVQdFUSxfAQNRBXUNAxBSe15QCVRVJ1pQEwd/WFBUAlElCFBFUnlaB1ULByRdBEFdfVtWVA=="
byte_data = base64.b64decode(encoded_str)

# Initialize the buffer and prepare to calculate the checksum
buffer = list(byte_data)
original_checksum = []

for i in range(0x40):
    byte = i - 11 * ((i * 0x5D1745D1745D1746 >> 64) >> 2)
    xor_byte = ord(string[byte])
    
    checksum_byte = xor_byte ^ buffer[i]
    
    # Append the resulting byte to the checksum list
    original_checksum.append(checksum_byte)

    checksum += chr(checksum_byte)

print("Checksum: ", checksum)
```

Providing this checksum writes ``Noice!!!`` on the terminal and writes data in ``REAL_FLAREON_FLAG.JPG``.

> The image file is created in the default root directory to use for user-specific cached data [see go documentation](https://pkg.go.dev/os#UserCacheDir)
> ```go
> v227.len = os_UserCacheDir();
> ```
> For me it was ``C:\Users\me\AppData\Local``

<p align="center">
           <img src="https://github.com/SamNzo/CTFs/blob/main/Flare-On/2024/img/REAL_FLAREON_FLAG.JPG?raw=true" width=400>
</p>

**Th3_M4tH_Do_b3_mAth1ng@flare-on.com**
