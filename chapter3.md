# Bổ sung hệ thống file và trình soạn thảo UNIX: nano and vim (cơ bản).

## Bảng tóm tắt - câu lệnh

Các lệnh cơ bản:
- `ls`: hiển thị nội dung thư mục.
- `cd`: chuyển thư mục
- `pwd`: cho biết vị trí thư mục hiện hành.
- `rm`: xóa file.
- `rmdir`: xóa thư mục.
- `cp`: sao chép file.
- `mv`: di chuyển file.


## Bảng tóm tắt - phân quyền

Có định dạng: **-{% em type="red" %}rwx{% endem %}{% em type="blue" %}rwx{% endem %}{% em type="green" %}rwx{% endem %}**
- {% em type="red" %}Quyền người dùng{% endem %}
- {% em type="blue" %}Quyền của nhóm{% endem %}
- {% em type="green" %}Quyền của người/nhóm khác{% endem %}
- R = Read (đọc), W = Write (viết, ghi), X = Execute (thực thi).
- Thư mục bắt đầu bởi kí tự **`d`** thay vì **`-`**.
- Xem các flags `r`, `w` và `x` như là các biến nhị phân.
  - 1: bật (ON)
  - 0: tắt (OFF)
- $$r . 2^2 + w . 2^1 + x . 2^0$$
- Ví dụ:
  - `chmod 755`: rwxr-xr-x
  - `chmod 600`: rw-------
  - `chmod 777`: rwxrwxrwx

## Quyền mặc định

Câu lệnh này sẽ tác động lên quyền của tất cả các file mà bạn đã tạo ra (trong phiên làm việc của bạn)
- Lệnh `umask`
  - `umask mode`: loại bỏ chế độ (ở đây là đọc, ghi hoặc thực thi) ra khỏi file
  - `umask` giống như một bộ lọc mà nó loại bỏ đi quyền của file hoặc thư mục đã tạo ra theo thứ tự vị trí **bit** được bật lên 1.
- Ví dụ:
  - `umask 077`: 
