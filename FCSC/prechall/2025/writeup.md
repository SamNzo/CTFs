# FCSC 2025
## Pré-chall

Dans le code source de la page principale du site (https://fcsc.fr) on trouve ce joli dessin.
```
    /--------------------------\      
   |       Hello Friend,        |
   |   Welcome to FCSC 2025 \o/ |
   |   Let's start the prechall |
   |         at /teasing        |
    \--------------------------/      
            \                      
             \                      
              \_ .~q`,
                 {__,  \
                     \' \
                      \  \
                       \  \
                        \  `._            __.__
                         \    ~-._  _.==~~     ~~--.._
                          \        '                  ~-.
                           \      _-   -_                `.
                            \    /       }        .-    .  \
                             `. |      /  }      (       ;  \
                               `|     /  /       (       :   '\
                                \    |  /        |      /       \    =
                                 |     /`-.______.\     |^-.      \
                                 |   |/           (     |   `.      \_
                                 |   ||            ~\   \      '._    `-.._____..----.._=__
                                 |   |/             _\   \      =~-.__________.-~~~~~~~~~'''
                               .o'___/            .o______}  
```

A l'adresse indiquée https://fcsc.fr/teasing on a 3 épreuves à réussir pour avoir le flag avec cette commande:
```
echo -n "FCSC{flag1/3}" "FCSC{flag2/3}" "FCSC{flag3/3}" | sha256sum | sed 's/ .*$/}/; s/^/FCSC{/'
```

### Partie 1
volatility

### Partie 2

On peut ouvrir le binaire avec Ghidra.

La fonction ``verif`` vérifie le flag.

```
byte verif(int param_1)

{
  byte bVar1;
  int iVar2;
  uint uVar3;
  int iVar4;
  uint uVar5;
  byte bVar6;
  uint uVar7;
  uint uVar8;
  byte local_50 [80];
  
  iVar2 = strlen(param_1);
  if (iVar2 == 0x18) {
    for (iVar2 = 0; iVar2 < 0x18; iVar2 = iVar2 + 1) {
      local_50[iVar2] = 0;
    }
    iVar2 = 0;
    uVar8 = 0x7f;
    while (iVar2 < 0xc0) {
      for (uVar7 = 0; (int)uVar7 < 8; uVar7 = uVar7 + 1) {
        uVar5 = uVar8 & 0x71;
        for (uVar3 = 1; (int)uVar3 < 8; uVar3 = uVar3 + 1) {
          uVar5 = (uVar5 ^ (int)(uVar8 & 0x71) >> (uVar3 & 0x1f)) & 0xff;
        }
        iVar4 = iVar2 + 7;
        if (-1 < iVar2) {
          iVar4 = iVar2;
        }
        local_50[iVar4 >> 3] =
             local_50[iVar4 >> 3] ^ (byte)((uVar8 & 1) << 0x20 - (0x20 - (uVar7 & 0x1f)));
        uVar8 = uVar8 >> 1 | (uVar5 & 1) << 7;
        iVar2 = iVar2 + 1;
      }
    }
    memcpy(local_50 + 0x18,&DAT_3f403840,0x18);
    breakpoint(0x1000,0x400d88a2,1,1);
    bVar6 = 0;
    for (iVar2 = 0; iVar2 < 0x18; iVar2 = iVar2 + 1) {
      bVar1 = local_50[iVar2] ^ local_50[iVar2 + 0x18];
      local_50[iVar2 + 0x18] = bVar1;
      bVar6 = bVar6 | bVar1 ^ *(byte *)(param_1 + iVar2);
    }
    bVar6 = bVar6 | local_50[0x18] != 'F' | local_50[0x19] != 'C' | local_50[0x1a] != 'S' |
            local_50[0x1b] != 'C';
  }
  else {
    bVar6 = 1;
  }
  return bVar6;
}
```

Code pour reverse la fonction et récupérer le bon input.
```py
buffer = [0 for i in range(80)]
flag = [0 for i in range(24)]

hex_value_1 = 0x7f
i = 0
while i < 0xc0:
    for j in range(8):
        hex_value_2 = hex_value_1 & 0x71
        for k in range(1, 8):
            hex_value_2 = (hex_value_2 ^ (hex_value_1 & 0x71) >> (k & 0x1f)) & 0xff
        buffer[i >> 3] = buffer[i >> 3] ^ ((hex_value_1 & 1) << 0x20 - (0x20 - (j & 0x1f)))
        hex_value_1 = hex_value_1 >> 1 | (hex_value_2 & 1) << 7
        i = i + 1

data = [0x39, 0x03, 0xb2, 0xef, 0xf8, 0x0e, 0x71, 0xb4, 0xdb, 0x93, 0xf6, 0x51, 
        0x3a, 0x62, 0xa6, 0xe8, 0x64, 0x9b, 0x81, 0x04, 0x01, 0x42, 0x74, 0xb5]

index = 24
for byte in data:
    buffer[index] = byte
    index += 1

ret_value = 0
for i in range(24):
    xor_result = buffer[i] ^ data[i]
    buffer[i + 24] = xor_result
    flag[i] = xor_result

flag[24] = 70
flag[25] = 67
flag[26] = 83
flag[27] = 67

print(''.join(chr(x) for x in flag))
```

### Partie 3
faire un solveur et lister toutes les possibilités puis prendre celle qui optimise le pgcd de chaque ligne
