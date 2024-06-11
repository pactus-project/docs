---
title: Data Serialization
weight: 9
---

Data serialization is the process of converting data into a format that can be easily stored or transmitted over a network.
It typically involves encoding data into a sequence of bytes, which can later be decoded to
reconstruct the original data structure.
Pactus has two methods for data serialization: Deterministic serialization and CBOR serialization:

## Deterministic Serialization

Pactus uses a deterministic serialization for the deterministic data like blocks and transactions.
The serialization format for different types of data is listed in the table below:

| **Data Type**           | **Size (bytes)** | **Description**                                  |
| ----------------------- | ---------------- | ------------------------------------------------ |
| uint8                   | 1                | An 8 bits unsigned integer                       |
| int8                    | 1                | An 8 bits signed integer                         |
| uint16                  | 2                | A 16 bits unsigned integer                       |
| int16                   | 2                | A 16 bits signed integer                         |
| uint32                  | 4                | A 32 bits unsigned integer                       |
| int32                   | 4                | A 32 bits signed signed integer                  |
| uint64                  | 8                | A 64 bits unsigned integer                       |
| int64                   | 8                | A 64 bits signed signed integer                  |
| [VarInt](#varint)       | Variable         | A compact representation of an unsigned integer. |
| [VarByte](#varbyte)     | Variable         | A variable length bytes                          |
| [VarString](#varstring) | Variable         | A variable length string                         |
| Address                 | 21               | 21 bytes of address data                         |
| Hash32                  | 32               | 32 bytes of hash data                            |

### VarInt

Variable length integer (VarInt) is encoded by 7-bit chunks. The MSB indicates whether there are
more octets (1) or it is the last one (0). It means `0x00` to `0x7f` encoded in 1 byte, `0x80` to
`0x3fff` encoded in 2 bytes, ...

Example:

```text
0x0f -> 0f
0x1000 -> 8020
0xffff -> ffff03
0xffffff -> ffffff07
```

### VarByte

Variable length byte (VarByte) is encoded as a variable length integer (VarInt) containing the
length of the array followed by the bytes themselves: `VarInt(len(bytes)) || bytes`

### VarString

Variable length string (VarString) is encoded as a variable length integer (VarInt) containing the
length of the string followed by the bytes that represent the string
itself:`VarInt(len(str)) || str`

### Byte Order

All the internal number representation are in little-endian byte order.

### Example

Here is an example of a block header data that encoded using deterministic serialization:

```shell
000000   01 1A 87 3D 62 B6 9E 39  B4 E0 65 67 B6 AD 3A 58  ...=b¶.9´àeg¶­:X
000010   F6 1D F4 C3 C0 59 20 A2  90 43 27 7A F0 12 64 C9  ö.ôÃÀY ¢.C'zð.dÉ
000020   E1 E7 69 30 68 BB F7 B5  E0 10 CA 98 DA 56 29 65  áçi0h»÷µà.Ê.ÚV)e
000030   A1 A3 41 1A 48 FE E7 0B  D0 DB BE 11 D9 86 7F A9  ¡£A.Hþç.ÐÛ¾.Ù..©
000040   E1 3B 3E 00 5E 99 BB D5  49 99 C7 CD 6B B1 76 B1  á;>.^.»ÕI.ÇÍk±v±
000050   60 96 20 80 EE 13 0C 45  5C 88 50 7B D5 1A 87 8A  `. .î..E\.P{Õ...
000060   0B 85 C6 56 CF C1 A5 42  CB BE 01 05 70 83 89 CA  ..ÆVÏÁ¥BË¾..p..Ê
000070   68 26 9B DA 29 01 19 CB  A9 96 0C 6A D2 8A AA A1  h&.Ú)..Ë©..jÒ.ª¡
000080   40 37 7F 65 2B DE A0 55  1E 3B                    @7.e+Þ U.;
```

## CBOR Serialization

For non-deterministic data, such as networking messages, Pactus uses
“Concise Binary Object Representation” or [CBOR](https://tools.ietf.org/html/rfc7049).
CBOR is a binary data serialization format that is widely used in various application,
including IoT, web services, security, and automotive, due to its compact representation and efficient parsing.

### CBOR Me!

[cbor.me](https://cbor.me)
is an online tool for encoding and decoding CBOR data, offering developers an easy way to test and
validate their CBOR data without having to set up a local environment.

### Example

Here is an example of a vote message that encoded using [CBOR](https://cbor.me/?bytes=a60101021864030004582019ba0a47813c13b2459f4ce3851ca42da8299c4f17b226e8bad1a9859172ab960555015da8f5e196d6e961609ae41528c4ec7368975937065830b047d5c2c072299284355f5b5014b5bf77f1702bc08b36061ddba08e41bebf51ab0416d265973190d26cbb79144681e7).

```shell
000000   A6 01 01 02 18 64 03 00  04 58 20 19 BA 0A 47 81  ¦....d...X .º.G.
000010   3C 13 B2 45 9F 4C E3 85  1C A4 2D A8 29 9C 4F 17  <.²E.Lã..¤-¨).O.
000020   B2 26 E8 BA D1 A9 85 91  72 AB 96 05 55 01 5D A8  ²&èºÑ©..r«..U.]¨
000030   F5 E1 96 D6 E9 61 60 9A  E4 15 28 C4 EC 73 68 97  õá.Öéa`.ä.(Äìsh.
000040   59 37 06 58 30 B0 47 D5  C2 C0 72 29 92 84 35 5F  Y7.X0°GÕÂÀr)..5_
000050   5B 50 14 B5 BF 77 F1 70  2B C0 8B 36 06 1D DB A0  [P.µ¿wñp+À.6..Û
000060   8E 41 BE BF 51 AB 04 16  D2 65 97 31 90 D2 6C BB  .A¾¿Q«..Òe.1.Òl»
000070   79 14 46 81 E7                                    y.F.ç
```
