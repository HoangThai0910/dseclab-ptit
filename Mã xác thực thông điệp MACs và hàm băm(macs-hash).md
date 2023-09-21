## Khởi động lab ##
Trên terminal nhập: `labtainer -r macs-hash`
## Nhiệm vụ 1 ##
- Dùng `ls` để xem các file trong hệ thống
- Sử dụng `shasum` để thử 7 thuật toán mã hóa với tệp:

`shasum -a 1 foo.txt`

`shasum -a 224 foo.txt`

`shasum -a 256 foo.txt`

`shasum -a 384 foo.txt`

`shasum -a 512 foo.txt`

`shasum -a 512224 foo.txt`

`shasum -a 512256 foo.txt`

## Nhiệm vụ 2 ##
- Nhập `lynx verydodgy.com`

![image](https://user-images.githubusercontent.com/108949637/269705709-c4ed2694-b678-46cb-9c82-16bcf7970b36.png)

Sử dụng phím mũi tên lên xuống để chọn file, phím `D` để tải xuống, phím mũi tên trái để quay lại.

![image](https://user-images.githubusercontent.com/108949637/269706101-b3b8ca9b-5f55-481b-83d5-11728c09d381.png)

Standard download options: Save to disk -> Enter -> Đặt tên file -> Enter. Chú ý tải cả 2 file floppy57.fs và SHA256.sdx

Tạo giá trị băm SHA256 với file vừa tải xuống: `shasum -a 256 floppy57.fs`
## Nhiệm vụ 3 ##
Tạo file iou.txt với nội dung "Bob owes me 200 dollars": `echo "Bob owes me 200 dollars" >> iou.txt`

Tạo giá trị băm SHA256 của file iout.txt: `shasum -a 256 iou.txt`
## Nhiệm vụ 4 ##
Thực hiện lệnh sau để tìm dữ liệu ngẫu nhiên mà khi băm, 6 số cuối dạng hex của bản tóm lược sẽ trùng với 6 số cuối dạng hex của bản tóm lược file declare.txt: `./collide1.sh declare.txt 1`
## Nhiệm vụ 5 ##
Chạy file collide2.py: `./collide2.py`
## Nhiệm vụ 6 ##
Cho giá trị băm HMAC-SHA1 của file declare.txt là "986eb8a92e561f550a911352c8b2cf5fd0465342", biết rằng key là chữ số từ 0 đến 9. Như vậy ta chỉ cần thử từng giá trị key đến khi giá trị băm thu được trùng khớp với đề bài. Sau khi thử ta biết được key cần tìm là 6:

`openssl dgst -sha1 6 declare.txt`

![image](https://github.com/HoangThai0910/dseclab-ptit/assets/108949637/1b27dce5-0933-447f-9afb-cf7689c0e9eb)

## Kết thúc lab ##
Trên terminal đầu tiên nhập: `labtainer -r macs-hash`
