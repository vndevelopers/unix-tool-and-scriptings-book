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

## Liên kết file

Giống như Window, chúng ta có thể tạo liên kết đến file và các thư mục. Có 2 loại liên kết:
- Liên kết thô (hard link).
- Liên kết tượng trưng (symbolic link).

Tạo liên kết:
- `ln -[tùy_chọn] <file_mục_tiêu> [tên_liên_kết]`
  - Tạo một liên kết tới `<file_mục_tiêu>` qua `[tên_liên_kết]`, mặc định đang đứng ở thư mục hiện hành.
  - Liên kết này sẽ trỏ đến cùng một file trên hệ thống. Liên kết này không khác gì so với file gốc.
  - Nói cách khác, file gốc và liên kết trỏ đến cùng một đối tượng bên dưới.

## Liên kết tượng trưng

Liên kết tượng trưng:
- `ln -s <file_mục_tiêu> [tên_liên_kết]`
  - Tạo một liên kết tượng trưng tới file hoặc thư mục.
  - File liên kết chứa đường dẫn đến file gốc hoặc thư mục.
  - Nói cách khác, liên kết tượng trưng trỏ đến một file khác.

## Các loại file

Thường có hai loại. Loại thứ nhất là file văn bản thuần túy (plain text, gọi ngắn gọn là văn bản).
- File văn bản: định dạng mà con người có thể đọc được. Thường được dùng cho các mục đích:
  - Tài liệu
  - Hướng dẫn cài đặt ứng dụng
  - Mã nguồn
  - File log (file ghi lại thông tin)
  - Bất kì thứ gì mà con người có thể đọc được ở phiên cuối cùng.
- Chẳng hạn những thứ mà bạn tạo bằng notepad.
- Có thể chỉnh sửa bởi các editor (phần mềm chỉnh sửa văn bản).

## File nhị phân

File nhị phân dùng để viết mã máy (ngôn ngữ mà máy có thể hiểu được). 
- Con người không thể đọc, hiểu được (không tính các trường hợp sử dụng hex editor (chương trình dịch ngược mã máy)).
- Thường dùng cho các loại file thực thi, thư viện, file media (ví dụ: mp3, mp4...), .zip...
- Phải cần một số chương trình có đầu ra là file nhị phân để tạo ra nó.

## Đây là loại file nào?

Hiển thị loại file:
- `file <tên_file>`

## Đọc file

Chỉ đọc file mà không cần phải chỉnh sửa, ta có lệnh:
- `cat <file>`
  - In ra nội dung file trên cửa sổ terminal.
- `cat <file_1> <file_2>`
  - In ra nội dung lần lượt file_1 đến file_2
- `more <file>`
  - Cho phép cuộn từng trang một tại một thời điểm
- `less <file>`
  - Cho phép cuộn lên hoặc xuống từng trang một hay dòng một.

## Bắt đầu và kết thúc

Đôi khi bạn chỉ cần xem đầu file (tiêu đề) hoặc kết thúc của file (kết quả).
- `head -[số_dòng] <file>`
- `tail -[số_dòng] <file>`
  - In ra -[số_dòng] đầu/cuối file.
  - Mặc định là 10 dòng.
- Ví dụ: `tail /var/log/Xorg.0.log`: in ra 10 dòng cuối của file log.

## In ra terminal

Chúng ta đã thấy có nhiều cách khác nhau để in một văn bản ra màn hình. Nếu bạn muốn in ra một chuỗi, sử dụng:
- `echo <text_string>`
  - In chuỗi đầu vào ra terminal
  - `echo This is a string`
  - `echo ’This is a string’`
  - `echo "This is a string"`
    - tất cả đều in ra giống nhau
- Chúng ta sẽ nói lý do tại sao đề cập đến 3 trường hợp này ở các bài học sau.

## Thao tác với file văn bản

Shell được thiết kế để người dùng có thể tương tác với file văn bản một cách toàn diện và hiệu quả. Trước khi đến với vài thứ thú vị mới - bạn cần một viên thuốc để tỉnh táo chứ??

## Thao tác với file văn bản - dành cho người mới

- Lệnh `nano <file>`
  - Mở file> cho việc chỉnh sửa.
  - Chỉnh sửa bằng terminal editor (các bạn đã tìm hiểu về khái niệm terminal ở chương 1).
  - Vì bãn đang sử dụng UNIX, nên editor này sẽ tốt cho bạn trong khóa học.
  - Những phím tắt cho việc lưu, thoát bắt đầu bởi phím Crtl.

**Chuyển sang chế độ nâng cao (try hard)**

## VIM = awesome!

- Vim là trình chỉnh sửa văn bản gọn nhẹ và đầy sức mạnh.
- Vim là từ viết tắt của **V**i **IM**proved.
  - Vi là trình chỉnh sửa văn bản cũ hơn, có thể xem là tiền thân của Vim.
- Vim được hỗ trợ cho mọi hệ thống, kể cả Window.
- Với Vim, việc chỉnh sửa văn bản sẽ nhanh hơn rất nhiều so với hầu hết các chương trình khác.
  - Mặc dù có những điểm cần phải nâng cấp.

## Phương thức chỉnh sửa văn bản

- Một trong các lí do mà Vim cho phép bạn chỉnh sửa văn bản nhanh hơn là vì nó làm việc trong các  chế độ (modes).
- Khi không có mode, người dùng có thể tương tác bằng cách sử dụng bàn phím / chuột, hoặc một tổ hợp phím nhùng nhằng, phức tạp bởi các phím ctrl, alt, ...
- Vim sử dụng các mode để đẩy tốc độ chỉnh sửa lên nhanh nhất có thể  mà không phụ thuộc vào các phím lệnh (command key) hoặc menu.

Bạn có thể chỉnh sửa văn bản chỉ bằng bàn phím với một tốc độ không tưởng.

## 3 chế độ (mode) chính của Vim

Chế độ chỉnh sửa (normal mode):
- Nhấn một phím để thực hiện lệnh mong muốn hoặc chuyển sang chế độ khác.
- Cho phép bạn xem văn bản nhưng không được chỉnh sửa.
- Vim bắt đầu ở chế độ thông thường (normal).
- Bạn có thể nhảy đến chế độ normal bằng cách nhấn phím Escape (Esc).

Chế độ trực quan (visual mode):











