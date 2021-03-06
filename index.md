# linux-chenxing

## Intro

This is intended to be a repository for info on the MStar/[SigmaStar](http://www.sigmastarsemi.com) SoCs.
The name is a parody of linux-sunxi for Allwinner SoCs. MStar in Chinese is
chenxing and the newer SigmaStar name is xingchen.

This will probably never get as big as linux-sunxi so github pages should be
more than enough.

Before MStar was bought out by MediaTek the company offered a wide range
of SoCs focused at STB and camera applications. Since the company was
bought by MediaTek the camera SoC part of the company has been spun out
into the fully owned subsidiary called Sigmastar. The camera SoCs that are 
now marketed by Sigmastar will be the main focus here.

It's worth noting that the MStar/Sigmastar camera SoCs seem to be derived
from the SoCs made by Alpha Imaging Technology which was merged into MStar
at some point.

# Porting Progress Matrix

## u-boot

|            | load u-boot SPL from vendor IPL | load u-boot from SPI NOR |
|------------|---------------------------------|--------------------------|
| infinity   | yes                             | yes                      |
| infinity2m | wip                             | wip                      |
| infinity3  | yes                             | yes                      |
| infinity6  | wip                             | wip                      |
| mercury5   | yes                             | yes                      |

## linux

|           | boots to shell from initramfs | boots to shell from local storage | full system from local storage with network etc |
|-----------|-------------------------------|-----------------------------------|-------------------------------------------------|
| infinity  | yes                           | yes                               | yes                                             |
| infinity3 | yes                           | yes                               | yes                                             |
| infinity6 | wip                           | wip                               | wip                                             |
| mercury5  | yes                           | wip                               | wip                                             |

# Reverse Engineering Progress

| family     | part     | date codes | sample device acquired | boot rom dumped | firmware dumped | SDK acquired | product brief acquired              | datasheet acquired                       |
|------------|----------|------------|------------------------|-----------------|-----------------|--------------|-------------------------------------|------------------------------------------|
| cedric     |          |            |                        |                 |                 |              |                                     |                                          |
|            | mst786   |            |                        |                 |                 |              |                                     | [yes](cedric/mst786_ds_v01maite_new.pdf) |
| infinity1  |          |            |                        |                 |                 | yes[0]       |                                     |                                          |
|            | msc313   | 1647B      | yes                    | yes             |                 |              |                                     |                                          |
|            | msc313d  | 1638B      |                        |                 |                 |              |                                     |                                          |
| infinity2  |          |            |                        |                 |                 |              |                                     |                                          |
|            | msr620   |            |                        |                 |                 |              |                                     |                                          |
|            | ssr621d  | 1945S      | yes                    | yes             | yes             |              |                                     |                                          |
| infinity3  |          |            |                        |                 |                 | yes[0]       |                                     |                                          |
|            | msc313e  | 1744B      | yes                    | yes             | yes             |              | [yes](infinity3/msc313e_pb_v03.pdf) |                                          |
|            |          | 1916S      |                        |                 |                 |              |                                     |                                          |
|            | msc316dc | 1929S      | yes                    | same as msc313e | yes             |              | [yes](infinity3/msc316dc_pb_v03.pdf)|                                          |
|            | msc316q  |            |                        |                 |                 |              | [yes](infinity3/msc316q_pb_v01.pdf) |                                          |
|            | msc318   |            |                        |                 |                 |              | [yes](infinity3/msc318_pb_v03.pdf)  |                                          |
| infinity6  |          |            |                        |                 |                 |              |                                     |                                          |
|            | ssc323   | 1928S      |                        |                 |                 |              |                                     |                                          |
|            |          | 1936J      |                        |                 |                 |              |                                     |                                          |
|            | ssc325   | 1937S      | yes                    | yes             | yes             |              |                                     |                                          |
| mercury2   |          |            | yes                    |                 |                 |              |                                     |                                          |
|            | msc8328  | 1744       |                        |                 | yes             |              |                                     |                                          |
| mercury5   |          |            |                        |                 |                 |              |                                     |                                          |
|            | ssc8336  | 1915S      | yes                    |                 | yes             |              |                                     |                                          |
|            | ssc8336n | 1918S      | yes                    | yes             | yes             |              |                                     |                                          |
|            | ssc8339d |            |                        |                 |                 |              | yes                                 |                                          |

- [0] SDK seems to actually be for the infinity1 but the infinity3 is very similar

# SoCs

## MIPS based

MStar used to make a lot of MIPS based SoCs for STBs. These aren't that
interesting in themselves but the IP blocks used in the MIPS SoCs were
carried forward to the later ARM chips so any datasheets that can be found
for the MIPS SoCs might help with reverse engineering the current ARM based
ones.

### STB

- MSD7818
- MSD7828

## ARM based

### Cedric Family

- [MST786](cedric#mst786) - Dual core Cortex A9 automotive (head unit) SoC

### Infinity IP camera family

#### [Infinity 1](infinity1)
- [MSC313](infinity1#msc313) - Cortex A7 + 64MB DDR2 in a QFN80
- [MSC313D](infinity1#msc313d) - Probably a Cortex A7 + 128MB DDR3 in a BGA

#### [Infinity 2](infinity2)

- part numbers not known, references to infinity2m in SDK. seems to be a multi-core part.
- SSR621D - Dual Cortex A7 128MB DDR3(TBC) in QFN128 with HDMI, VGA, SATA
- [MSR620?](http://www.sigmastarsemi.com/en/products/info.aspx?itemid=390&lcid=53&pid=)
- [MSR630?](http://www.sigmastarsemi.com/en/products/info.aspx?itemid=391&lcid=53&pid=) [TL-NVR6104C-4PX](https://www.tp-link.com.cn/product_1388.html#tag)

#### [Infinity 3](infinity3)
- [MSC313E](infinity3#msc313e) - Cortex A7 + 64MB DDR2 in a QFN80
- [MSC316DC](infinity3#msc316dc) - Cortex A7 + 128MB DDR3 in a QFN88
- [MSC316Q](infinity3) - Cortex A7 + 128MB DDR3 in a 256 ball BGA
- [MSC318](infinity3) - Cortex A7 + 128MB DDR3 in a 324 ball BGA 

#### [Infinity 5](infinity5)
- [SSC328Q](infinity5#ssc328q) - Cortex A7 + 256MB DDR3 (this might be i6)
- [SSC329Q](infinity5#ssc329q) - Cortex A7 + 256MB DDR3 + NPU (this might be i6)

#### [Infinity 6](infinity6)
- [SSC323](infinity6#ssc323) - probably Cortex A7 + 64MB DDR2 in a QFN88
- [SSC325](infinity6#ssc325) - Cortex A7 + 64MB DDR2 in a QFN88
- [SSC325DE](infinity6#ssc325de) - Cortex A7 + 128MB DDR3 in a QFN88
- [SSC326D](infinity6#ssc326d) - Cortex A7 + 128MB DDR3 + NPU
- [SSC327DE](infinity6#ssc327de) - Cortex A7 + 128MB DDR3

- Infinity 6e seems to be a dual core variation in this family

### Mercury family

#### [Mercury 2](mercury2)

- [AIT8328/MSC8328](mercury2#msc8328) - Probably ARM9
- [AIT8428](mercury2#ait8428) - Probably ARM9

#### [Mercury 5](mercury5)

- [SSC8336](mercury5#ssc8336) - Probably Cortex A7 + 64MB DDR2 in a QFP128
- [SSC8336N](mercury5#ssc8336n) - Cortex A7 + 64MB DDR2 in a 128 pin QFN
- [SSC8339D](mercury5#ssc8339d) - Probably in this family, Cortex A7 + 128MB(?) DDR3(?) in a 268 ball BGA

### Misc

- [MSB2521](misc/msb2521.md) - ARM9 based SatNav on a chip
- MSB2531 - Cortex A7 SatNav on a chip

# IP blocks

See [IP](ip).

# ISP/Debug Tool

See [ISP](isp).

# Blobs, headers, layouts

- [BootROM](blobs/bootrom.md) - Baked in BootROM
- [IPL](blobs/ipl.md) - First/Second stage bootloaders
- [MXPT](blobs/mxpt.md) - Partition table used for SPI NOR

# Vendor uboot, kernels..

- [Old 2015.01 based uboot from Taobao sourced SDK](https://github.com/fifteenhex/uboot_msc313e)
- [Old 3.18.30 based kernel from Taobao sourced SDK](https://github.com/fifteenhex/linux_msc313e)
- [Recent 4.9.84 based kernel](https://github.com/fifteenhex/linux-ssc325)

# Vendor SDKs

- [Mercury5](https://github.com/longyanjun2020/SDK_pulbic)
- [Probably Infinity2 NVR](https://github.com/ZYCX8888/Democode-TAKOYAKI-BETA001-0312)

## Sources of firmwares for reverse engineering

- [Anjvision firmwares](http://www.anjvision.com:8021/firmware/)

To get the device tree out of the kernel you can use binwalk + [extract-dtb](https://github.com/PabloCastellano/extract-dtb.git) and dtc.

```
binwalk -e <firmware.bin>
extract-dtb.py <extracted firmware dir><uncompressed kernel blob>
dtc -I dtb -O dts -o out.dts <extracted dtb that looks right>
```

# Links

- [aiwinn](http://www.aiwinn.com/) - seems to supply a bunch of AI enabled things based on SigmaStar SoCs
