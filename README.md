# jura-smartconnect-wifi
JURA SmartConnect WiFi reverse engineering.

## UDP Broadcast Packets

UDP broadcast: Data 117 bytes

### Known Fields

* Bytes   4- 19, length 16 bytes: SmartConnect WiFi Firmware version. E.g. "TT237W V05.26" 00 00 00
* Bytes  20- 51, length 32 bytes: JoE machine name.
* Bytes  52- 67, length 16 bytes: ??? + version. E.g. "EF538M V01.07" 00 00 00
* Bytes 104-109, length  6 bytes: MAC address, e.g. f4  cf a2 a7 58 28 = MAC F4:CF:A2:A7:58:28

### Assumed Fields

* Bytes   0-  3, length  4 bytes: Packet identifier? 00 75 a5 f3

### Raw Packet Data and Analysis

```
Data: 0075a5f3545432333757205630352e32360000004b616c656e204a757261204538000000…

Bytes   0-  3, length  4 bytes: Packet identifier? 00 75 a5 f3
Bytes   4- 19, length 16 bytes: SmartConnect WiFi Firmware version. E.g. "TT237W V05.26" 00 00 00
Bytes  20- 51, length 32 bytes: JoE machine name.
Bytes  52- 67, length 16 bytes: ??? + version. E.g. "EF538M V01.07" 00 00 00
Bytes  68-103 = ???.
Bytes 104-109, length  6 bytes: MAC address, e.g. f4  cf a2 a7 58 28 = MAC F4:CF:A2:A7:58:28
Bytes 110-116 = ???.

0040              3b e8 bc 82  00 03 3e 51 3d 65 00 ff       ;··· ··>Q=e··
0050  00 00 00 00 00 00 00 00  00 00 01 c0 41 b6 28 00   ········ ····A·(·
0060  00 00 00 00 00 00 00 f4  cf a2 a7 58 28 81 00 04   ········ ···X(···
0070  00 00 0c 00 08                                     ·····

0         1         2         3         4         5         6         7
0123456789012345678901234567890123456789012345678901234567890123456789012345678
 u··TT237W V05.26   NNNNN Jura E8                   EF538M V01.07   ;··· ·>Q=e 
                     1         1 
78         9         0         1
90123456789012345678901234567890123456
 ·          ··A·(        ····X(· ·   ·
```
