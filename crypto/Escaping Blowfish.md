# Escaping Blowfish

## Description

I found a strange part while analyzing the enemy's communication! Can you tell me what it is?

Author : Sy2n0
Points 150

## Solution

This is Blowfish cipher, obviously. The link given gives:
b'\x0b\xfc\x8d\xcb\x0eE\x9cdh\x8br8\x14\xb0HV\xd6M\xb2\xda\x88L\xe3"\xeb\xb6\xafS\xd4[\xb1S\x93\xda\xcdF;\x19\xb9\xc5x\xe2D\xad\x88g\xb5\x82\xa4\xe3X\xeb\x02\x15\xdf\xee'

We are given key = b"N0bOdy_cAn_FiNd_Th1s!"

Simply use script:
```py
from Crypto.Cipher import Blowfish
from Crypto.Util.Padding import pad

key = b"N0bOdy_cAn_FiNd_Th1s!"  

ciphertext = b'\x0b\xfc\x8d\xcb\x0eE\x9cdh\x8br8\x14\xb0HV\xd6M\xb2\xda\x88L\xe3"\xeb\xb6\xafS\xd4[\xb1S\x93\xda\xcdF;\x19\xb9\xc5x\xe2D\xad\x88g\xb5\x82\xa4\xe3X\xeb\x02\x15\xdf\xee'

cipher = Blowfish.new(key, Blowfish.MODE_ECB)
plaintext = cipher.decrypt(ciphertext)
print(plaintext)
```

Output: b'ESCAPE{I_l0v3_CrYpt0grAph7_th3_mOst_1n_th3_w0r1d_!!!}'
Flag - ESCAPE{I_l0v3_CrYpt0grAph7_th3_mOst_1n_th3_w0r1d_!!!}