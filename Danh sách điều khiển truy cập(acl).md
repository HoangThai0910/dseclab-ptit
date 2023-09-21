## Chuẩn bị lab ##
Khởi động lab: labtainer -r acl

Sau khi khởi động, 3 cửa sổ terminal hiện ra. Lần lượt login theo các tài khoản sau:
![image](https://user-images.githubusercontent.com/108949637/269626662-9f7fae5c-51d1-478e-82b5-456242074e7e.png)

## Nhiệm vụ 1 ##
- Trên terminal Alice, nhập các lệnh sau để đến thư mục `/shared_data` và liệt kê các quyền trên file:

  `cd /shared_data`

  `ls -l`

- Kiểm tra Alice có thể đọc file accounting.txt không, dùng lệnh cat để đọc file: `cat accounting.txt`
- Nhìn lại danh sách quyền truy cập các file. Với file accounting.txt có cài đặt quyền là -rw-rw----+
- Biểu tượng + ở cuối cho biết tệp này có thêm quản lý bằng ACL ngoài các quyền UNIX tiêu chuẩn của "rw" cho người dùng và nhóm người dùng. Dùng lệnh sau để kiểm tra quyền ACL của file: `getfacl accounting.txt`
- Chú ý chỉ có 1 trong 3 người dùng có quyền sửa đổi file `passcode.txt` là Harry, chuyển đến terminal của Harry nhập lệnh:

`echo "more stuff" >> /shared_data/accounting.txt`
- Quay lại terminal Alice, nhập thử lệnh `echo "test" >> /shared_data/accounting.txt` để xác nhận Alice không có quyền sửa đổi file này
## Nhiệm vụ 2 ##
- Trên terminal Bob, cho phép Alice đọc file `/shared_data/bob/bobstuff.txt` bằng lệnh:

`setfacl -m "u:alice:r" /shared_data/bob/bobstuff.txt`
- Nhập lệnh `cat /shared_data/bob/bobstuff.txt` trên terminal của Alice và Harry để xác nhận Alice có quyền đọc file này còn Harry thì không
## Nhiệm vụ 3 ##
- Nhập lệnh sau để cho phép ngoài Alice chỉ có Bob mới đọc được các file mới tạo:

`setfacl -dm "u:bob:r" /shared_data/alice/`

`setfacl -dm "o::--x" /shared_data/alice/`

- Tạo file mới và kiểm tra quyền:

`echo "attt-ptit" > ./alice/attt.txt`

`getfacl ./alice/attt.txt`

- Lần lượt nhập thử lệnh sau trên terminal của Bob và Harry để kiểm tra quyền của họ: `cat /shared_data/alice/attt.txt`

## Nhiệm vụ 4 ##
Nhiệm vụ yêu cầu chúng ta sửa script `fun` sao cho khi Alice chạy thì nó sẽ tạo ra một bản sao của `accounting.txt` để Bob có thể đọc được. Hãy để ý rằng ở nhiệm vụ 2 Alice đã cho Bob quyền đọc các file trong `/shared_data/alice`. Như vậy chúng ta chỉ cần chèn lệnh để Alice copy nội dung file `accounting.txt` vào thư mục `/shared_data/alice`: `cp /shared_data/accounting.txt /shared_data/alice/hacked.txt`. Lệnh cp sẽ copy nội dung file accounting.txt vào một file mới tên là hacked.txt

Ở đây mình dùng lệnh nano để sửa nội dung script `fun`: `nano /shared_data/bob/fun`. Khi nội dung file hiện lên màn hình, mình thực hiện chèn câu lệnh trên

![image](https://user-images.githubusercontent.com/108949637/269648266-431bc067-5273-4c2b-8c01-2aee3b5cf55c.png)

Sau đó bấm `Ctrl+X` để thoát ra. Khi chương trình hỏi lưu thay đổi thì bấm `y -> Enter`

![image](https://user-images.githubusercontent.com/108949637/269648742-40ec1a52-d906-473e-b391-1236b83da9b3.png)

Trên terminal của Alice, truy cập vào thư mục của Bob bằng lệnh: `cd /shared_data/bob`. Sau đó nhập `./fun` để chạy script

Quay lại terminal của Bob, thực hiện đọc file vừa được tạo: `cat /shared_data/alice/hacked.txt`

![image](https://user-images.githubusercontent.com/108949637/269650404-f676a29b-8bf5-48ba-91f2-691adec56bcb.png)

Như vậy Bob đã xem trộm được nội dung của file `accounting.txt`

## Kết thúc lab ##
Trên terminal đầu tiên nhập : `stoplab acl`
