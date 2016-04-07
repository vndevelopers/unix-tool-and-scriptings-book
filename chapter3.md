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
  - `umask 077`: cấp tất cả quyền cho người dùng, không cho truy cập thừ bất kì ai
  - `umask g-w`: kí hiệu thay thế: cho phép nhóm có quyền ghi.
  - `umask -S`:  hiển thị các mode đã bị loại bỏ qua kí hiệu tượng trưng

## Bảng tóm tắt - quyền sở hữu file

- Mỗi file được gán cho một người dùng và một nhóm (thường viết dạng `user:group`).
- Phải có quyền root để thay đổi quyền sở hữu file.
- Để biết bạn thuộc nhóm nào, gõ `groups` hoặc `id`.

## Thay đổi quyền sở hữu

Nếu bạn  muốn thay đổi nhóm của file mà bạn sở hữu, dùng lệnh **ch**ange **gr**ou**p**
- `chgrp nhóm <đối_tượng>`
  - Thay đổi nhóm sở hữu của file.

Nếu bạn có quyền root và bạn muốn đổi quyền sở hữu của ai đó đối với file, dùng lệnh **ch**ange **own**ership.
- `chown người_dùng/nhóm <đối_tượng>`
  - Thay đổi quyền sở hữu của file <đối_tượng>
  - Nhóm thì có thể có hoặc không.
  - Dùng flag `-R` để thay đổi cách đệ qui đối với thư mục và các file bên trong.

## Đệ qui

Hầu hết các câu lệnh (mà nó có tính suy diễn, logic) có tùy chọn đệ qui. Nó dùng để gây tác động đến tất cả các file trong các thư mục con của đối tượng.
- Dùng `-r` hoặc `-R` (kiểm tra tại manpage để rõ hơn với các lệnh khác nhau).
- Ví dụ: `chmod -R o-w ~/Document/`
  - Bỏ đi quyền ghi vào file cho đối tượng khác (other) cho các file bên trong thư mục ~/Document/



















