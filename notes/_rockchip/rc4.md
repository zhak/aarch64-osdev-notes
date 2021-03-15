---
title: "RC4 algorithm"
layout: note
updated: "2021-03-15"
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
<br>
<div class="language-fasmarm"><div class="highlight"><pre class="highlight"><code>
macro rc4 start, count {
    local K, S, i, j, Si, Sj, Ki, x, y

    virtual at 0
        K:: db 0x7c,0x4e,0x03,0x04,0x55,0x05,0x09,0x07,\
               0x2d,0x2c,0x7b,0x38,0x17,0x0d,0x17,0x11
    end virtual

    virtual at 0
        S:: rb 256
        repeat 256
            store byte %-1 at S:%-1
        end repeat
    end virtual

    j = 0
    repeat 256
        load Si byte from S:%-1
        load Ki byte from K:(%-1) mod 16
        j = (j + Si + Ki) mod 256
        load Sj byte from S:j
        store byte Si at S:j
        store byte Sj at S:%-1
    end repeat

    i = 0
    j = 0
    repeat count
        i = (i + 1) mod 256
        load Si byte from S:i
        j = (j + Si) mod 256
        load Sj byte from S:j
        store byte Si at S:j
        store byte Sj at S:i
        load y byte from S:(Si + Sj) mod 256
        load x byte from start + %-1
        store byte (x xor y) at start + %-1
    end repeat
}
</code></pre></div></div>
