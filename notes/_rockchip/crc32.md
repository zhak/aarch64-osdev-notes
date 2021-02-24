---
title: "Rockchip CRC32 algorithm"
layout: note
updated: "2021-02-24"
---

```python
def crc32(data):
    crc = 0
    for b in data:
        crc = crc ^ (b << 24)
        for i in range(8):
            if crc & 0x80000000:
                crc = (crc << 1) ^ 0x04c10db7
            else:
                crc = crc << 1
    return crc & 0xffffffff
```
