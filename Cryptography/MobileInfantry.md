# Mobile Infantry
> nc 0.cloud.chals.io 27602\
Point: 100\
Author: v10l3nt

Khi chạy lệnh trên terminal, nó yêu cầu mình nhập một cái gì đó, Đầu tiên mình thử nhập chuỗi kí tự bất kì thì có thông báo chuỗi không hợp lệ, và nó cho mình source code kiểm tra đầu vào hợp lệ. 
```python
def len_check(pad):
    if len(pad) != 38:
        return False
    return True
```
Chúng ta có thể dễ dàng nhìn thấy nó yên cầu chuỗi phải có độ dài là 38 kí tự. Vậy nên chúng ta tiếp tục nhập vào một chuỗi ngẫu nhiêu dài 38 kí tự thì tiếp tục nhận tiếp source codde thứ hai vẫn là kiểm tra đầu vào hợp lệ nâng cấp cho code ban đầu.
```python
def check1(pad):
    for i in range(0, int(len(pad)/2)+1):
        if not pad[i].isupper():
            return False
    return True
```
Xem source code, có thể thấy rằng nó yêu cầu từ kí tự 0 đến trước kí tự 20 phải là viết hoa. Sau đó chúng ta tiếp tục sửa input sao cho tất cả chuỗi đều là viết hoa.
Và nhận được source coded thứ ba.
```python
def check2(pad):
    for i in range(int(len(pad)/2)+1, len(pad)):
        if not pad[i].islower():
            return False
    return True
```

Ở source code này chúng yêu cầu bạn pk kiểm soát sao cho 18 kí tự sau phải là dạng viết thường. Nhập input vừa sửa chúng ta tiếp tục nhận được source code thứ tư.
```python
def check3(pad):
    for i in range(0, int(len(pad)/2)):
        if ord(pad[i]) != ord(pad[i+1])-1:
            return False
    return True
```

Source code này chúng yêu cầu sao cho 20 kí tự đầu phải có dạng tăng dần theo bảng mã. Nhập input vừa sửa đổi chúng ta tiếp tục nhận được source code thứ năm.
```python
def check4(pad):
    for i in range(int(len(pad)/2)+1, len(pad)-1):
        if ord(pad[i]) != ord(pad[i+1])+1:
            return False
    return True
```

Ở source code này chúng yêu cầu chúng ta phải đảm bảo rằng 18 kí tự cuối phải có thứ tự giảm dần theo bảng mã. Tiếp tục sửa input và nhập vào pad. Và đến đây chúng ta nhận được thông báo đã bypass thành công nhưng vẫn chưa thấy flag cần tìm.
Tổng quan lại, source code bài này yêu cầu chúng ta cần nhập vào một chuỗi gồm:
* 38 kí tự
* 20 kí tự đầu phải là viết hoa và có thứ tự tăng dần
* 18 kí tự sau phải là viết thường và có thứ tự giảm dần.

Vậy nên chúng ta có đến 63 trường hợp có thể xảy ra.

#### Source code tìm các chuỗi thỏa mãn yêu cầu:
```python
import string 

lower = string.ascii_lowercase[::-1]
upper = string.ascii_uppercase

result = ""
for i in range(7):
    for j in range(9):
        result = upper[i:i+20] + lower[j:j+18]
        print(result)
```
Do mình khá ngu code nên đến đoạn này mình là nhập tay từng chuỗi một vào pad để kiểm tra input.\
Và nhận được chuỗi hợp lệ là: EFGHIJKLMNOPQRSTUVWXxwvutsrqponmlkjihg

#### Source code tham khảo: 
```python
from pwn import *

up = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
low = "abcdefghijklmnopqrstuvwxyz"

for i in range(7):
    for j in range(9):
        up_sub = up[i : i + 20]
        low_sub = "".join(list(reversed(low[j : j + 18])))
        pad = up_sub + low_sub

        io = remote("0.cloud.chals.io", 27602)

        for _ in range(100):
            line = str(io.recvline())[2:-3]
            print(line)
            if ( line == "Here in the mobile infantry, we also implement some stronger roughneck checks." ):
                break
        line = str(io.recvline())
        line = str(io.recv())[2:-1]
        print(line)

        io.send(pad + "\n")
        for _ in range(7):
            line = str(io.recvline())[2:-3]
            print(line)
            if "flag" in line:
                exit()
            if "[+] Welcome" in line:
                break
```
### shctf{Th3-On1Y-G00d-BUg-I$-A-deAd-BuG}
