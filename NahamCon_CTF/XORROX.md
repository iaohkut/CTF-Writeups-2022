### Challenge crypto: XORROX

> We are exclusive -- you can't date anyone, not even the past! And don't even think about looking in the mirror! \
Author: @JohnHammond#6971\
Point: 50pts

* xorrox.py
```python
#!/usr/bin/env python3

import random

with open("flag.txt", "rb") as filp:
    flag = filp.read().strip()

key = [random.randint(1, 256) for _ in range(len(flag))]

xorrox = []
enc = []
for i, v in enumerate(key):
    k = 1
    for j in range(i, 0, -1):
        k ^= key[j]
    xorrox.append(k)
    enc.append(flag[i] ^ v)

with open("output.txt", "w") as filp:
    filp.write(f"{xorrox=}\n")
    filp.write(f"{enc=}\n")

```

* output.txt
```
xorrox=[1, 209, 108, 239, 4, 55, 34, 174, 79, 117, 8, 222, 123, 99, 184, 202, 95, 255, 175, 138, 150, 28, 183, 6, 168, 43, 205, 105, 92, 250, 28, 80, 31, 201, 46, 20, 50, 56]
enc=[26, 188, 220, 228, 144, 1, 36, 185, 214, 11, 25, 178, 145, 47, 237, 70, 244, 149, 98, 20, 46, 187, 207, 136, 154, 231, 131, 193, 84, 148, 212, 126, 126, 226, 211, 10, 20, 119]
```

### Explain code
Đây là dạng bài XOR thường thấy trong các giải CTF.

Đầu tiên, chúng ta có 
* flag đươc lấy từ file.txt
* key được tạo ngẫu nhiên là tập các số tự nhiên trong khoảng [1, 256], và có độ dài bằng độ dài flag
```python
with open("flag.txt", "rb") as filp:
    flag = filp.read().strip()

key = [random.randint(1, 256) for _ in range(len(flag))]
```

1. Tập xorrox được tạo bằng cách sau:
    * xorrox[1] = 1 ^ key[1]
    * xorrox[2] = 1 ^ key[2] ^ key[1]
    * xorrox[3] = 1 ^ key[3] ^ key[2] ^ key[1]\
    ................................
    * xorrox[n] = 1 ^ key[n] ^ key[n-1] ^ key[n-2] ... ^ key[1]

2. Tập enc được tạo bằng cách XOR từng kí tự của flag và key.

### Solution:
Làm ngược lại những thao tác mà file encrypt đã làm, bỏ qua giá trị đầu tiên của key vì trong file encrypt không dùng đến nó, chúng ta có:
* key[1] = 1 ^ xorrox[1]: có được key[1]
* key[2] = 1 ^ xorrox[2] ^ key[1]: có được key[2]
* key[3] = 1 ^ kxorroxey[3] ^ key[2] ^ key[1]: có được key[3]\
................................
* key[n] = 1 ^ xorrox[n] ^ key[n-1] ^ key[n-2] ... ^ key[1]: có được toàn bộ key

Sau đó, XOR từng kí tự của key và enc chúng ta có được flag.

### Source code tham khảo:
``` python
xorrox=[1, 209, 108, 239, 4, 55, 34, 174, 79, 117, 8, 222, 123, 99, 184, 202, 95, 255, 175, 138, 150, 28, 183, 6, 168, 43, 205, 105, 92, 250, 28, 80, 31, 201, 46, 20, 50, 56]
enc=[26, 188, 220, 228, 144, 1, 36, 185, 214, 11, 25, 178, 145, 47, 237, 70, 244, 149, 98, 20, 46, 187, 207, 136, 154, 231, 131, 193, 84, 148, 212, 126, 126, 226, 211, 10, 20, 119]
key = [1]
for i in range(1, len(xorrox)):
    k = xorrox[i] ^ 1
    if i != 1:
        for j in range(1, i):
            k ^= key[j]
    key.append(k)
    print(chr(enc[i]^k), end="")
```
Sửa lại flag cho chuẩn định dạng đề "flag{...}".
### Flag: flag{21571dd4764a52121d94deea22214402}
