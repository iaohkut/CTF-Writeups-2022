### Challenge crypto: Off The Grid

> Description: A space pirate was able to infiltrate the Galactic Federation HQ and plant a virus that's locked everyone out! Whenever they boot their machines, all that they see is this strange grid. Whoever this space pirate is, he sure doesn't play fair.

### Files: 
* CryptoGrid.png:\
![playfair](https://user-images.githubusercontent.com/77691959/165580225-be1ffe0e-ab5e-4685-b98c-e5efc9d7da1f.png)

* enc.txt:
```
UIKOTHNVGELBKCRNPDDN
```

Từ hình ảnh đề bài và nhiều chút OSINT thì tôi đã tìm được một loại mật mã khác giống với cấu trúc trong ảnh, là [Playfair cipher](https://en.wikipedia.org/wiki/Playfair_cipher).\
Để chắc chắn đúng thì trong đoạn mô tả của thử thách có nhắc đến rằng ***" he sure doesn't play fair "***, vậy nên đây chắc chắn là một thử thách playfair cipher.

Playfair cipher có cấu trúc của một ma trận n*n, mỗi vị trí sẽ là một kí tự trong bảng chữ cái alphabet:

![2022-04-27_13-17](https://user-images.githubusercontent.com/77691959/165583004-2631caf1-90a3-4715-8a8b-3c497d1e80cc.png)

Sau đây là một số ví dụ cách **Playfair cipher** mã hóa:

* màu xanh là plaintext
* màu đỏ là ciphertext

![play1](https://user-images.githubusercontent.com/77691959/165584215-e061ecdf-8dcc-4c48-aaca-9b1de4025e77.png)
![play2](https://user-images.githubusercontent.com/77691959/165584216-93cc12bd-f6b8-425b-a2d1-371916761d45.png)
![play3](https://user-images.githubusercontent.com/77691959/165584218-a6365dff-c364-4f5a-9a96-b80ec192817e.png)
![play4](https://user-images.githubusercontent.com/77691959/165584222-28b50e42-e93c-44a9-83ce-a3236102ba93.png)
![play5](https://user-images.githubusercontent.com/77691959/165584225-be0af749-83d3-4b49-b337-ae54912929aa.png)
![play6](https://user-images.githubusercontent.com/77691959/165584226-fd26ada3-03c1-4ebc-9580-471d688d94b2.png)

### Solution

Bây giờ chúng ta có ciphertext trong file enc.txt, chia chúng thành từng cặp:

> UI KO TH NV GE LB KC RN PD DN

Dựa vào hình ảnh đề bài cho thực hiện giải mã:

![2022-04-27_13-32](https://user-images.githubusercontent.com/77691959/165585640-56bb5ea2-cf84-4bec-8328-595b5da293dc.png)

Bao đoạn tin nhắn bằng cấu trúc flag.

### Flag: shctf{the_PRophecY_has_spoken}
