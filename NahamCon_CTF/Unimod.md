### Challenge crypto: Unimod

> I was trying to implement ROT-13, but got carried away.\
Author: @Gary4657

1. unimod.py
```python
import random

flag = open('flag.txt', 'r').read()
ct = ''
k = random.randrange(0,0xFFFD)
for c in flag:
    ct += chr((ord(c) + k) % 0xFFFD)

open('out', 'w').write(ct)

```
2. out
> 饇饍饂饈饜餕饆餗餙饅餒餗饂餗餒饃饄餓饆饂餘餓饅餖饇餚餘餒餔餕餕饆餙餕饇餒餒饞飫

### Explain
Đây là dạng mã Caesar huyền thoại, nhưng khác biệt ở đây là nó không nằm trong khoảng thường thấy.

### Solution:
Chúng ta cần chuyển đổi tất cả các kí tự trong file out sang dạng decimal.

Sau đó dựa vào định dạng flag có sẵn để tìm được giá trị k được tạo ngẫu nhiên.

Và cuối cùng tìm ra flag theo decimal tìm được.

Source code tham khảo: 
``` python
flag_ct = open('/home/tunc/Downloads/out', 'r').read()
list_ct = []

for i in range(len(flag_ct)):
    list_ct.append(ord(flag_ct[i]))

Max = int("0xFFFD", 16)

for i in range(Max):
    if (102 + i ) % Max == list_ct[0]:
        k = i
        break
    
for i in range(len(list_ct)):
    print(chr(list_ct[i] - k), end="")
```
### Flag: flag{4e68d16a61bc2ea72d5f971344e84f11}.
