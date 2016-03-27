# Phím tắt, lịch sử, bí danh lệnh, quy ước ký tự, và nén file.


## Vim - Lời khuyên hữu ích

**Tìm kiếm và thay thế:**
Tìm kiếm với từ khóa search_term:

- `/search_term`

Thay thế một từ khóa hoặc mẫu (pattern) cho bằng chuỗi (string) với tùy chọn (options):

- `:%s/pattern/string/[option]`

Khi bạn tìm thấy từ khóa search_term lần đầu, nhấn phím **n** để đến vị trí xuất hiện tiếp theo. Phím **N** để lùi lại vị trí trước đó.

## Tools - Lời khuyên hữu ích

**Liệt kê danh sách file:**
Tùy chọn dưới góc nhìn khách quan người dùng:
- `ls -lh`

Liệt kê mỗi file trên một dòng:
- `ls -1`

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

- Nếu bạn đã đăng nhập vào máy chủ (server), chỉ cần gõ `bash`.
- Bạn muốn hệ thống tự động chạy bash shell khi ta đăng nhập, có một cách để thực hiện là chỉnh sửa file `./login` - nó sẽ chạy bash khi bạn đăng nhập vào máy chủ.

Để chạy bash tự động, thêm dòng dưới đây vào cuối file `./login`:
- `if ( -f /bin/bash ) exec /bin/bash --login`

Nếu bạn có quyền root, chỉ cần chỉnh sửa `/etc/passwd` và tìm dòng tương ứng với người dùng hiện thời.

## Sử dụng Bash một cách hiệu quả

Bài học này bao gồm:
- Phím tắt của shell
- Tái sử dụng lịch sử
- Lệnh giả lập (aliasing)
- Những kí tự mở rộng
- Nén file

## Phím tắt của shell

Cách đưa câu lệnh vào nhanh và dễ hơn:
- Sử dụng phím **tab** để hoàn tất phần còn lại của câu lệnh. Ví dụ, bạn muốn có câu lệnh **chmod**, gõ **chm** sau đó nhấn **tab** bạn sẽ được **chmod**.
- Phím **Up-Down** : duyệt lại lịch sử các câu lệnh đã dùng. Do đó bạn không cần phải gõ lại bất kì câu lệnh nào
- **Ctrl + e**: nhảy đến vị trí cuối dòng
- **Ctrl + a**: nhảy đến vị trí đầu dòng
- **Ctrl + u**: xóa mọi thứ từ vị trí đang đứng đến đầu dòng
- **Ctrl + k**: xóa mọi thứ từ vị trí đang đứng đến cuối dòng
- **Ctrl + l**: làm sạch màn hình

Những phím tắt khác:
- http://www.aboutlinux.info/2005/08/bash-shell-shortcuts.html

## Tái sử dụng lịch sử: toán tử `Bang (!)`

Sử dụng toán tử "Bang" (!) để gọi lại câu lệnh từ lịch sử chỉ với một hoặc vài kí tự đi kèm.
Ví dụ:
- `chmod 777 hello_world.sh`
- `!c`
- -> `chmod 777 hello_world.sh`
- Sử dụng toán tử `!` có thể giảm bớt số lần gõ phím khi phải thực hiện cùng một việc

## Tái sử dụng lịch sử: tìm kiếm

Bạn có thể tìm kiếm một câu lệnh thông qua lịch sử sử dụng bằng tổ hợp phím **Ctrl + R**:
- Nhấn **Ctrl + R** và gõ vào câu lệnh muốn tìm, kết quả giống với lịch sử sẽ được hiển thị
- Nhấn tiếp **Ctrl + R** để xem tiếp các kết quả giống nhau khác
- Nếu đã giống với kết quả mong muốn, nhấn **Enter** để thực hiện lại (re-executed) câu lệnh đó
- Nhấn **ESC** để sao chép (copy) câu lệnh đó mà không thực hiện nó
- Nhấn **Ctrl + G** để thoát khỏi việc tìm kiếm và quay lại giao diện ban đầu

Ví dụ:
- `(reverse-i-search)'c': chmod 777 hello_world.sh` 

## Lệnh giả lặp (Aliases)

Sử dụng **Bash** càng nhiều, bạn sẽ thấy nó có rất nhiều tùy chọn và tiện ích cho phù hợp với công việc của bạn. Một ví dụ điển hình `ls -l` để xem quyền của người dùng (user) đối với file hoặc thư mục (directory), hoặc là `rm -i` để chắc chắn rằng bạn không xóa nhầm file một cách ngẫu nhiên hay vô ý. Sẽ tốt hơn nếu ta tạo ra những phím tắt (shortcuts) cho chúng bằng những từ khóa mang ý nghĩa rõ ràng hơn?

Alias:
- `alias tên_mong_muốn=câu_lệnh` (`alias name=command`)
- Lệnh giả lặp cho phép bạn đổi tên hoặc đơn giản nó thay vì phải gõ một câu lệnh dài.
- Bạn có thể thiết lập lệnh giả lập cho phiên làm việc hiện tại ở màn hình nhận lệnh (command promt)
- Để thiết lâp một lệnh giả lập một cách lâu dài và cố định (sử dụng cho các phiên làm việc khác), thêm lệnh giả lặp vào file `.bashrc` hoặc là `.bash_profile` ở thư mục `/home` (home directory).

## Ví dụ về lệnh giả lặp (Alias)

- `alias ls='ls --color=auto'`
- `alias dc=cd`
- `alias ll='ls -l'`

- Cần phải trích dẫn (quote) nếu lệnh giả lặp nhiều hơn một từ, đó là cặp kí tự `'`
- Chú ý: nếu bạn tác động (poking) vào `.bashrc`, bạn nên biết rằng bất kì dòng nào bắt đầu bởi `#` là chú thích (comment out) và sẽ không được thực hiện (executed).

## Mở rộng (expansion) về shell

Trong Bash shell, nếu ta đưa vào câu lệnh:
- `echo Hello Vietnam`
- -> Hello Vietnam
Nhưng nếu ta nhập vào:
- `echo *`
- -> hello_world.sh Lect1.pdf Lect2.pdf

Điều gì đã xảy ra?
Shell mở rộng toán tử `*` liệt kê tất cả các file tại thư mục bạn đang đứng. Đó là một ví dụ về mở rộng đường dẫn (path expansion), một loại mở rộng của shell.

## Ngữ nghĩa của các kí tự đặc biệt

Shell có những kí tự đặc dưới đây:
- `$ * < > & ? { } [ ]`
- Mặc định, shell sẽ hiểu chúng là kí tự đặc biệt trừ khi ta bỏ qua (escape) chúng hoặc để chúng trong trích dẫn (quote). Ví dụ, `\$`, `\&` hoặc `"$"`, `"*"`.
- Khi chúng ta gọi một câu lệnh, việc đầu tiên là shell sẽ chuyển chuỗi các kí tự ta đã nhập vào sang câu lệnh UNIX mà hệ thống có thể hiểu được.
- Khả năng hiểu được (hay con gọi là thông dịch) (interpret) và mở rộng câu lệnh là một trong những sức mạnh vô cùng to lớn của shell scripting.

Chúng ta sẽ tiếp tục với các kí tự đặc biệt còn lại trong khóa học này.

## Mở rộng (expansion) về shell (tiếp theo)

`* ^ ? { } [ ]` được gọi là các kí tự đại diện (wildcard)  mà shell sử dụng để tìm kiếm chuỗi (string) hoặc mẫu (pattern) thỏa mản các điều kiện cho trước:
- Bất kì chuỗi nào cũng được chấp nhận.
- Chỉ kí tự đơn lẻ.
- Một nhóm tự hoặc cụm từ.
- Chỉ giới hạn trong tập kí tự cho trước.

- `*` tất cả các kí tự đều thỏa, kể cả chuỗi rỗng (null string).
- Ví dụ:
- ![](Screenshot1.jpg)

- `?` chỉ lấy kí tự đơn lẻ
- Ví dụ:
- ![](Screenshot2.jpg)

- `[...]` thỏa tất cả các kí tự trong cặp ngoặc vuông
- Ví dụ:
- ![](Screenshot3.jpg)

- `[^...]` thỏa tất cả các kí tự không nằm trong cặp ngoặc vuông
- Ví dụ:
- ![](Screenshot4.jpg)






