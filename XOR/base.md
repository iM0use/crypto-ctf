# XOR



## Data Representation

数据有不同的基数，以基数为底的指数，比如二进制。

| Encoding Type | What is Displayed | How to Distinguish                                         |
| ------------- | ----------------- | ---------------------------------------------------------- |
| ASCII         | HI                | 容易读                                                     |
| Binary        | 01001000 01001001 | Only 0s and 1s                                             |
| Decimal       | 72 73             | 全是数，( 32 - 126 ), 在HTML编码，例如, N is &#78 for HTML |
| Hexadecimal   | 48 49             | 由 0 到 F 表示 ( 10 = A, 11 = B, … 15 = F )                |
| Base 64       | SEK=              | 包含随机字母                                               |



## XOR BASICS

An XOR or *eXclusize OR* is a bitwise operation indicated by `^` and shown by the following truth table:

| A    | B    | A^B  |
| ---- | ---- | ---- |
| 0    | 0    | 0    |
| 0    | 1    | 1    |
| 1    | 0    | 1    |
| 1    | 1    | 0    |

So what XOR'ing bytes in the action `0xA0 ^ 0x2C`

| 1    | 0    | 1    | 0    | 0    | 0    | 0    | 0    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 0    | 0    | 1    | 0    | 1    | 1    | 0    | 0    |
|      |      |      |      |      |      |      |      |
| 1    | 0    | 0    | 0    | 1    | 1    | 0    | 0    |

`0b10001100` is equivalent to `0x8C`, a cool property of XOR is that it is reversible  meaning `0x8C ^ 0x2C = 0xA0` and `0x8C ^ 0xA0 = 0x2C`



## What does this have to da with CTF ???

XOR is a cheap way to encrypt data with a password. Any data can be encrypted using XOR as shown in this Python example:



```python
>>> data = 'CAPTURETHEFLAG'
>>> key = 'A'
>>> encrypted = ''.join([chr(ord(x) ^ ord(key)) for x in data])
>>> encrypted
'\x02\x00\x11\x15\x14\x13\x04\x15\t\x04\x07\r\x00\x06'
>>> decrypted = ''.join([chr(ord(x) ^ ord(key)) for x in encrypted])
>>> decrypted
'CAPTURETHEFLAG'
```



## Exploiting XOR Encryption

### Single Byte XOR Encryption

It is easy to break bruteforce.

### Multibyte XOR Encryption

Multibyte XOR gets exponentially harder the longer the key, but if the encrypted text is long enough, character frequency analysis is a viable method to find the key. Character Frequency Analysis means that we split the cipher text into groups based on the number of characters in the key. These groups then are bruteforced using the idea that some letters appear more frequently in the english alphabet than others.
