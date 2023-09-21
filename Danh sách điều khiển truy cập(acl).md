## Chuẩn bị lab ##
Khởi động lab: labtainer -r acl

Sau khi khởi động, 3 cửa sổ terminal hiện ra. Lần lượt login theo các tài khoản sau:
![image](https://user-images.githubusercontent.com/108949637/269626662-9f7fae5c-51d1-478e-82b5-456242074e7e.png)

## Nhiệm vụ 1 ##
- Trên terminal Alice, nhập các lệnh sau để đến thư mục /shared_data và liệt kê các quyền trên file:

  `cd /shared_data`

  `ls -l`

- Kiểm tra Alice có thể đọc file accounting.txt không, dùng lệnh cat để đọc file: `cat accounting.txt`
- Nhìn lại danh sách quyền truy cập các file. Với file accounting.txt có cài đặt quyền là: `-rw-rw----+`
- Biểu tượng + ở cuối cho biết tệp này có thêm quản lý bằng ACL ngoài các quyền UNIX tiêu chuẩn của "rw" cho người dùng và nhóm người dùng. Dùng lệnh sau để kiểm tra quyền ACL của file: `getfacl accounting.txt`
- Chú ý có 1 trong 3 người dùng có quyền sửa đổi file `passcode.txt`, chuyển đến terminal của người đó nhập lệnh: `echo "more stuff" >> /shared_data/accounting.txt`
- Quay lại terminal Alice, nhập thử lệnh `echo "test" >> /shared_data/accounting.txt` để xác nhận Alice không có quyền sửa đổi file này
## Nhiệm vụ 2 ##
- Trên terminal Bob, cho phép Alice đọc file `/shared_data/bob/bobstuff.txt` bằng lệnh: `setfacl -m "u:alice:r" /shared_data/bob/bobstuff.txt`
## Nhiệm vụ 3 ##
- Trên terminal Alice, tạo file mới trong `/shared_data/alice`: `touch test.txt`
- Nhập lệnh sau để cho phép ngoài Alice chỉ có Bob mới đọc được các file mới tạo:

`setfacl -dm "u:bob:r" /shared_data/alice/`

`setfacl -dm "o""--x" /shared_data/alice/`

- Tạo file mới và kiểm tra quyền:

`echo "attt-ptit" > ./alice/attt.txt`

`getfacl ./alice/attt.txt`

- Lần lượt nhập thử lệnh sau trên terminal của Bob và Harry để kiểm tra quyền của họ: `cat /shared_data/alice/attt.txt`

## Nhiệm vụ 4 ##
