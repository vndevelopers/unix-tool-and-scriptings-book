# Phím tắt, lịch sử, bí danh lệnh, quy ước ký tự, và nén file.


## Vim - Lời khuyên hữu ích

**Tìm kiếm và thay thế:**
Tìm kiếm với từ khóa search_term:

- /search_term

Thay thế một từ khóa hoặc mẫu (pattern) cho bằng chuỗi (string) với tùy chọn (options):

- :%s/pattern/string/[option]

Khi bạn tìm thấy từ khóa search_term lần đầu, nhấn **n** để đến vị trí xuất hiện tiếp theo. Phím **N** để lùi lại vị trí trước đó.

## Tools - Lời khuyên hữu ích

**Liệt kê danh sách file:**
Tùy chọn dưới góc nhìn khách quan con người:
- ls -lh

Liệt kê mỗi file trên một dòng:
- ls -1

## Shell (tiếp theo)

Có nhiều loại shell cho hệ thống UNIX và họ nhà UNIX:
- sh: Bourne Shell - rất phổ biến và được tạo bởi Stephen Bourne.
- bash: Bourne Again Shell - loại shell mặc định cho hệ điều hành GNU, những phiên bản của Linux và OSX
- csh: C Shell - tương tác và gần giống với C, loại shell mặc định cho hệ thống BSD-based.
- zsh: Z Shell - có thể xem đây là tích hợp những tinh hoa shell được lấy cảm hứng từ sh, bash, csh, ksh và tcsh.

Trong khóa học này, chúng ta chọn bash shell vì nó có đầy đủ các tiện ích, chức năng và là tiêu chuẩn tốt nhất với các shell còn lại

Để tìm hiểu thêm, ta có thể tham khảo tại Wikipedia:
- https://en.wikipedia.org/wiki/Comparison_of_command_shells

## Nếu Bash shell không được để mặc định trong máy tính

- Nếu bạn đã đăng nhập vào máy chủ (server), chỉ cần gõ bash.
- Bạn muốn hệ thống tự động chạy bash shell khi ta đăng nhập, có một cách để thực hiện là chỉnh sửa file ./login - nó sẽ chạy bash khi bạn đăng nhập vào máy chủ.

Để chạy bash tự động, thêm dòng dưới đây vào cuối file ./login:
- if ( -f /bin/bash ) exec /bin/bash --login

Nếu bạn có quyền root, chỉ cần chỉnh sửa /etc/passwd và tìm dòng tương ứng với người dùng hiện thời.























