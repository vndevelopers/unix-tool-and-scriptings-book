# Hệ thống file UNIX

### Ở bài học trước, chúng ta đã tìm hiểu sơ lược về hệ thống UNIX và những phiên bản của nó

### Hôm nay sẽ đi chi tiết. Hãy xoắn tay áo của bạn lên và trải nghiệm, đừng ngại bẩn tay nhé.


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