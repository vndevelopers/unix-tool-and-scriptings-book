# Hệ thống file UNIX

### Ở bài học trước, chúng ta đã tìm hiểu sơ lược về hệ thống UNIX và những phiên bản của nó

### Hôm nay sẽ đi chi tiết. Hãy xoắn tay áo của bạn lên và nhúng tay vào để trải nghiệm, đừng ngại bẩn nhé.


## Lưu ý nhỏ

Những câu lệnh trong bài học sẽ có kiểu chữ như sau: `câu lệnh`

Một bảng tóm tắt về cách gọi câu lệnh sẽ được thể hiện dạng một danh sách gồm câu lệnh và các  đồi số  (arguments)/cờ (flags) tùy chọn đi kèm.
Ví dụ: `Câu_Lệnh [tùy_chọn_1] [tùy_chọn_2]`

Để thực thi một câu lệnh, ta chỉ cần gõ nó vào cửa sổ dòng lệnh và nhấn Enter.

## Hệ thống file UNIX

Thư mục gốc (root) được kí hiệu bởi kí tự đơn / (bất kể bạn có bao nhiêu ổ cứng, phân vùng hay các bộ nhớ ngoài đi kèm).

File và thư mục (directories) là một trường hợp đặc biệt:
- `hello.txt != Hello.txt`

Khác với Window, các thư mục trong UNIX được ngăn ra bởi kí tự /
- UNIX: `/home/user1/Documents/cs2043/2014/Lecture2/`
- Window: `D:\Documents\cs2043\2014\Lecture2\`

File ẩn được bắt đầu bởi dấu "." : .gimp

## Hệ thống phân cấp file trong UNIX

![](unix_filesystem.jpg)

## Những thư mục đó là gì?

`/dev`: có thể  truy cập các thiết bị phần cứng tại đây - thông thường bạn không cần đụng đến đống hỗn độn này.
`/lib`: chứa các thư viện, cùng với `/usr/lib`, `/usr/local/lib`, ...
`/mnt`: dùng để kết nối thêm các thiết bị lưu trữ khác vào hệ thống.
`/usr`: lưu trữ các chương trình được cài đặt bởi người dùng và các file liên quan.
`/etc`: cài đặt cho tầng hệ thống.

## Vậy thì những chương trình được cài đặt ở đâu?

Thông thường là ở các thư mục "nhị phân" (binary):
`/bin`: các chương trình ở tầng hệ thống.
`/usr/bin`: các chương trình ở mức người sử dụng.
`/usr/local/bin`: một vài chương trình ở mức người sử dụng.

## Thế tư liệu của tôi đâu?

File của bạn sẽ được tìm thấy trong thư mục `home`, thường ở:
- `/home/tên_người_dùng`

Bạn cũng có thể truy cập thư mục `home` thông qua một kí tự đặt biệt: `~`

Những điều này có vẻ thú vị thật, nhưng làm sao để  biết ở đây nó có gì và đi đến như thế  nào? Haiz...a...

## Tôi đang ở đâu?

Mặc định thì shell sẽ dùng đường dẫn hiện tại ở cửa sổ dòng lệnh. Nếu không bạn hãy thử:
**`P`rint `W`orking `D`irectory**
































