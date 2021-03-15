---
title: "RK3308 memory map"
layout: note
updated: "2021-02-25"
---

As appears in the [Rockchip RK3308 Technical Reference Manual Part I]({{ '/pdf/ref/soc/rk3308/RK3308-TRM-1.pdf' | relative_url }}){:target="_blank"}

| Base Address  | Size     | Description                  |
|--------------:|:---------|:-----------------------------|
| `00000000`    | 4080 MiB | External memory (DRAM)       |
| `ff000000`    | 64 KiB   | GRF                          |
| `ff010000`    | 64 KiB   | DDR_UPCTL                    |
| `ff020000`    | 64 KiB   | DFI_MONITOR                  |
| `ff030000`    | 64 KiB   | DDR_STANDBY                  |
| `ff040000`    | 64 KiB   | I2C0                         |
| `ff050000`    | 64 KiB   | I2C1                         |
| `ff060000`    | 64 KiB   | I2C2                         |
| `ff070000`    | 64 KiB   | I2C3                         |
| `ff080000`    | 64 KiB   | WDT                          |
| `ff090000`    | 64 KiB   | **~~Reserved~~**             |
| `ff0a0000`    | 64 KiB   | UART0                        |
| `ff0b0000`    | 64 KiB   | UART1                        |
| `ff0c0000`    | 64 KiB   | UART2                        |
| `ff0d0000`    | 64 KiB   | UART3                        |
| `ff0e0000`    | 64 KiB   | UART4                        |
| `ff0f0000`    | 192 KiB  | **~~Reserved~~**             |
| `ff120000`    | 64 KiB   | SPI0                         |
| `ff130000`    | 64 KiB   | SPI1                         |
| `ff140000`    | 64 KiB   | SPI2                         |
| `ff150000`    | 192 KiB  | **~~Reserved~~**             |
| `ff180000`    | 64 KiB   | PWM_4CH                      |
| `ff190000`    | 64 KiB   | **~~Reserved~~**             |
| `ff1a0000`    | 64 KiB   | TIMER_6CH_0                  |
| `ff1b0000`    | 64 KiB   | TIMER_6CH_1                  |
| `ff1c0000`    | 128 KiB  | **~~Reserved~~**             |
| `ff1e0000`    | 64 KiB   | SARADC_CTL                   |
| `ff1f0000`    | 64 KiB   | TSADC_CTL                    |
| `ff200000`    | 64 KiB   | **~~Reserved~~**             |
| `ff210000`    | 64 KiB   | Non-secure OTPC              |
| `ff220000`    | 64 KiB   | GPIO0                        |
| `ff230000`    | 64 KiB   | GPIO1                        |
| `ff240000`    | 64 KiB   | GPIO2                        |
| `ff250000`    | 64 KiB   | GPIO3                        |
| `ff260000`    | 64 KiB   | GPIO4                        |
| `ff270000`    | 64 KiB   | **~~Reserved~~**             |
| `ff280000`    | 64 KiB   | Secure DMAC0                 |
| `ff290000`    | 64 KiB   | Secure DMAC1                 |
| `ff2a0000`    | 32 KiB   | KEY reader                   |
| `ff2a8000`    | 32 KiB   | Secure OTPC                  |
| `ff2b0000`    | 64 KiB   | SGRF                         |
| `ff2c0000`    | 64 KiB   | DMAC0                        |
| `ff2d0000`    | 64 KiB   | DMAC1                        |
| `ff2e0000`    | 64 KiB   | VOP                          |
| `ff2f0000`    | 64 KiB   | CRYPTO                       |
| `ff300000`    | 64 KiB   | I2S_8CH_0                    |
| `ff310000`    | 64 KiB   | I2S_8CH_1                    |
| `ff320000`    | 64 KiB   | I2S_8CH_2                    |
| `ff330000`    | 64 KiB   | I2S_8CH_3                    |
| `ff340000`    | 64 KiB   | **~~Reserved~~**             |
| `ff350000`    | 64 KiB   | I2S_2CH_0                    |
| `ff360000`    | 64 KiB   | I2S_2CH_1                    |
| `ff370000`    | 64 KiB   | **~~Reserved~~**             |
| `ff380000`    | 64 KiB   | PDM_8CH                      |
| `ff390000`    | 64 KiB   | **~~Reserved~~**             |
| `ff3a0000`    | 64 KiB   | SPDIF_8CH_TX                 |
| `ff3b0000`    | 64 KiB   | SPDIF_8CH_RX                 |
| `ff3c0000`    | 64 KiB   | VAD                          |
| `ff3d0000`    | 192 KiB  | **~~Reserved~~**             |
| `ff400000`    | 256 KiB  | USB 2.0 OTG                  |
| `ff440000`    | 64 KiB   | USB 2.0 HOST EHCI            |
| `ff450000`    | 64 KiB   | USB 2.0 HOST OHCI            |
| `ff460000`    | 128 KiB  | **~~Reserved~~**             |
| `ff480000`    | 64 KiB   | SDMMC                        |
| `ff490000`    | 64 KiB   | EMMC                         |
| `ff4a0000`    | 64 KiB   | SDIO                         |
| `ff4b0000`    | 64 KiB   | NANDC                        |
| `ff4c0000`    | 64 KiB   | SFC                          |
| `ff4d0000`    | 64 KiB   | **~~Reserved~~**             |
| `ff4e0000`    | 64 KiB   | MAC                          |
| `ff4f0000`    | 64 KiB   | **~~Reserved~~**             |
| `ff500000`    | 64 KiB   | CRU                          |
| `ff510000`    | 64 KiB   | **~~Reserved~~**             |
| `ff520000`    | 64 KiB   | PMU                          |
| `ff530000`    | 64 KiB   | DDR_PHY                      |
| `ff540000`    | 64 KiB   | OTP_MASKER                   |
| `ff550000`    | 64 KiB   | CPU_BOOST                    |
| `ff560000`    | 64 KiB   | Audio codec PHY              |
| `ff570000`    | 64 KiB   | **~~Reserved~~**             |
| `ff580000`    | 64 KiB   | GIC                          |
| `ff590000`    | 192 KiB  | **~~Reserved~~**             |
| `ff5c0000`    | 192 KiB  | Interconnect service         |
| `ff5f0000`    | 64 KiB   | DDR Firewall                 |
| `ff600000`    | 2 MiB    | **~~Reserved~~**             |
| `ff800000`    | 256 KiB  | A32_DEBUG                    |
| `ff840000`    | 7424 KiB | **~~Reserved~~**             |
| `fff80000`    | 256 KiB  | SRAM                         |
| `fffc0000`    | 192 KiB  | **~~Reserved~~**             |
| `ffff0000`    | 64 KiB   | BootROM (32 KiB) or SRAM     |
