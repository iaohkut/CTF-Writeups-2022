# Rahool's Challenge
> nc 0.cloud.chals.io 10294\
![Screenshot 2022-04-04 142858](https://user-images.githubusercontent.com/77691959/161501653-a82ba443-5815-44da-9c30-519cf498eb72.png)
#### Chúng ta nhìn thấy rằng có một đoạn text rất khả nghi, nó trông giống 1 câu văn gì đó.
> Ciphertext: ESDK EDS NFIMNGDJTB XEZVZ OWV KOYRTI KT ZCT BOZ CDIY DIK Z PJ K UNMTV DIK J PJ K AKMD NSUN OWV GPXY 
TEQSGH PWDFX RXKR UNZ P RC B LJJI KOJ VDXXFX MXXRU GAIVB
#### Thoạt nhìn chúng ta có thể thấy rằng nó có dạng của một loại mã chuyển vị.
#### Chúng ta có thể lên đây để kiểm tra xem nó có khả năng là loại mã chuyển vị nào: [cipher identifier](https://www.boxentriq.com/code-breaking/cipher-identifier)
![Screenshot 2022-04-04 143317](https://user-images.githubusercontent.com/77691959/161501649-f1c6f78d-bb51-4ae2-bd6e-4bdd2435a9a0.png)
#### Ohhhhhhhhhh, Chúng có khẳ năng cao chính là Vigenere cipher.
#### Sau đó có thể dùng [dcode](https://www.dcode.fr/vigenere-cipher) để brute force ciphertext mà không cần dùng đến key xem có khả quan chút nào không.
> Phaintext: NICE JOB DECRYPTING INPUT THE ANSWER AS THE KEY WITH THE E AS A THREE THE O AS A ZERO WITH THE WORD
ENGRAM AFTER WITH THE A AS A FOUR AND AOGNER RIGHT AFTER\
Key: RKBGVP

#### Dựa theo đoạn text vừa tìm được chúng ta có thể thấy rằng tiếp theo cần biến đổi khóa này để có thể khớp với input bài toán:
* THE KEY WITH THE E AS A THREE THE O AS A ZERO WITH 
* THE WORD ENGRAM AFTER WITH THE A AS A FOUR 
* AOGNER RIGHT AFTER

#### Đến với dữ kiện tiếp theo trong output của nc:
> Message:A + Key:B = 0 + B = O

#### Bằng một cách thần kì nào đó thì từ message "A" và key "B" thì chúng ta có ciphertext "O" mà không phải là "B".
#### Vậy nên chúng ta có một cách đó là sửa bảng encode của vigenere cipher.
#### Nhưng theo như trong bảng chữ cái Alphabet thì "B" và "O" cách nhau 13 đơn vị. Hmmmmmm, Rot13 chăng.
![2022-04-04_04-04](https://user-images.githubusercontent.com/77691959/161501562-480b4f31-d630-48ad-8ea9-4b213bca9ef2.png)
#### Yeahhhhhhh, chính là nó:
> Key: EXOTIC

#### Từ đó chúng ta có input: 3X0TICENGR4MAOGNER
![2022-04-04_04-16](https://user-images.githubusercontent.com/77691959/161502810-1f4f80f6-4ef4-4e0e-882a-3d6286c785f8.png)
### Flag: shctf{c0Me_baCk_s0on_w3_n33d_the_chAll3nge}