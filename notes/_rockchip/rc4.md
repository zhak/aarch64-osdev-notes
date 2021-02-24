---
title: "Rockchip RC4 algorithm"
layout: note
updated: "2021-02-24"
---

```python
def rc4(data):
    K = [0x7C,0x4E,0x03,0x04,0x55,0x05,0x09,0x07,0x2D,0x2C,0x7B,0x38,0x17,0x0D,0x17,0x11]
    C = []

    S = [i for i in range(256)]
    l = len(K)
    j = 0
    for i in range(256):
        j = (j + S[i] + K[i % l]) % 256
        S[i], S[j] = S[j], S[i]

    i = 0
    j = 0
    for b in data:
        i = (i + 1) % 256
        j = (j + S[i]) % 256
        S[i], S[j] = S[j], S[i]
        C.append(b ^ S[(S[i] + S[j]) % 256])
    return bytearray(C)
```
