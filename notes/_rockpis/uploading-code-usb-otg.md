---
title: "Uploading code for testing over USB OTG"
layout: note
updated: "2021-02-25"
---

Booting from SD card just to test code during active development phase is pretty inconvenient and wears memory card out. Hopefully, there's a much better option. With the help of `rkdeveloptool` it is possible to upload code for testing over USB OTG directly into device memory.

`rkdeveloptool` is open source and can be obtained from [GitHub](https://github.com/rockchip-linux/rkdeveloptool){:target="_blank"}.

However, `rkdeveloptool` only accepts firmware images which comply with Rockchip RKBOOT format.

The following Python script packs `ddr.bin` and target application for use with `rkdeveloptool`:

```python
# rkpack.py ddrbin appbin outbin
#
# Params:
# ddrbin - path to ddr.bin
# appbin - path to target app.bin
# outbin - output file name (should be .bin to please rkdeveloptool)

import datetime
import struct
import sys


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


hdr_fmt = '<LHHLHHBBBBBL BLB BLB'
hdr_size = struct.calcsize(hdr_fmt)

fte_fmt = '<BL40sLLL'
fte_size = struct.calcsize(fte_fmt)

with open(sys.argv[1], 'rb') as f:
    ddrbin = f.read()

with open(sys.argv[2], 'rb') as f:
    appbin = f.read()

now = datetime.datetime.now()
hdr = struct.pack(
    hdr_fmt + fte_fmt[1:] + fte_fmt[1:],

    # rkboot header
    0x544f4f42,     # signature ('BOOT')
    hdr_size,       # size of header
    0x0100,         # version (1.0)
    0,              # reserved
    0x0103,         # magic
    now.year,       # year
    now.month,      # month
    now.day,        # day
    now.hour,       # hour
    now.minute,     # minute
    now.second,     # second
    0x33333038,     # SoC model ('3308')

    # file table entry descriptors
    1, hdr_size, fte_size,
    1, hdr_size + fte_size, fte_size,

    # file table entries
    fte_size,                                   # entry size
    1,                                          # file type
    bytearray('ddr.bin'.encode('utf-16-le')),   # file name (UTF-16)
    hdr_size + fte_size * 2,                    # file offset
    len(ddrbin),                                # file size
    0,                                          # ???

    fte_size,                                   # entry size
    1,                                          # file type
    bytearray('app.bin'.encode('utf-16-le')),   # file name (UTF-16)
    hdr_size + fte_size * 2 + len(ddrbin),      # file offset
    len(appbin),                                # file size
    0                                           # ???
)

out = bytearray(hdr)
out.extend(rc4(ddrbin))
out.extend(rc4(appbin))
out.extend(crc32(out).to_bytes(4, 'little'))
with open(sys.argv[3], 'wb') as f:
    f.write(out)
```

### Example

```bash
$ python3 rkpack.py rk3308_ddr_589MHz_uart0_m0_v1.26.bin test-app.bin out.bin
$ rkdeveloptool db out.bin
```

Target application starts executing in SDRAM at address `0x00000000`, having UART conveniently pre-configured for serial communication.
