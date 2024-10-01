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

Our input is checked multiple times using the function ``main_b``.

Function ``main_a`` contains the code that actually does
```go
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

**Th3_M4tH_Do_b3_mAth1ng@flare-on.com**
