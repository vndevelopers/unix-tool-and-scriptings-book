# Hệ thống file UNIX

**Ở bài học trước, chúng ta đã tìm hiểu sơ lược về hệ thống UNIX và những phiên bản của nó**

**Hôm nay sẽ đi chi tiết. Hãy xoắn tay áo của bạn lên và nhúng tay vào để trải nghiệm, đừng ngại bẩn nhé.**

## Lưu ý nhỏ

Những câu lệnh trong bài học sẽ có kiểu chữ như sau: `câu lệnh`

Một bảng tóm tắt về cách gọi câu lệnh sẽ được thể hiện dạng một danh sách gồm câu lệnh và các  đồi số  (arguments)/cờ (flags) tùy chọn đi kèm.
Ví dụ: `Câu_Lệnh [tùy_chọn_1] [tùy_chọn_2]`

Để thực thi một câu lệnh, ta chỉ cần gõ nó vào cửa sổ dòng lệnh và nhấn Enter.

## Hệ thống file UNIX

Thư mục gốc (root) được kí hiệu bởi kí tự đơn `/` (bất kể bạn có bao nhiêu ổ cứng, phân vùng hay các bộ nhớ ngoài đi kèm).

File và thư mục (directories) là một trường hợp đặc biệt:
- `hello.txt != Hello.txt`

Khác với Window, các thư mục trong UNIX được ngăn ra bởi kí tự `/`
- UNIX: `/home/user1/Documents/cs2043/2014/Lecture2/`
- Window: `D:\Documents\cs2043\2014\Lecture2\`

File ẩn được bắt đầu bởi dấu "." : .gimp

## Hệ thống phân cấp file trong UNIX

![](unix_filesystem.jpg)

### Những thư mục đó là gì?

- `/dev`: có thể  truy cập các thiết bị phần cứng tại đây - thông thường bạn không cần đụng đến đống hỗn độn này.
- `/lib`: chứa các thư viện, cùng với `/usr/lib`, `/usr/local/lib`, ...
- `/mnt`: dùng để kết nối thêm các thiết bị lưu trữ khác vào hệ thống.
- `/usr`: lưu trữ các chương trình được cài đặt bởi người dùng và các file liên quan.
- `/etc`: cài đặt cho tầng hệ thống.

### Vậy thì những chương trình được cài đặt ở đâu?

Thông thường là ở các thư mục "nhị phân" (binary):
- `/bin`: các chương trình ở tầng hệ thống.
- `/usr/bin`: các chương trình ở mức người sử dụng.
- `/usr/local/bin`: một vài chương trình ở mức người sử dụng.

### Thế  còn tư liệu của tôi?

File của bạn sẽ được tìm thấy trong thư mục `home`, thường ở:
- `/home/tên_người_dùng`

Bạn cũng có thể truy cập thư mục `home` thông qua một kí tự đặt biệt: `~`

Những điều này có vẻ thú vị thật, nhưng làm sao để  biết ở đây nó có gì và đi đến như thế  nào ?

### Tôi đang đứng ở ?

Mặc định thì shell sẽ dùng đường dẫn hiện tại ở cửa sổ dòng lệnh. Nếu không bạn hãy thử:
- **P**rint **W**orking **D**irectory
- `pwd`
  - in ra đầy đủ đường dẫn của thư mục hiện thời.
  - rất thuận tiện khi bạn đi lạc đâu đó.
  - một biến môi trường rất quan trọng trong scritps.

### Xung quanh tôi có gì?

Trước khi ta định đến một nơi nào đó, hãy xem xung quanh ta có những gì.
- The **l**i**s**t command
- `ls [cờ (flags)] [file]`
  - In ra nội dung của thư mục (bao gồm cả thư mục con).
  - Hành vi tương tự như lệnh `dir` của DOS.
  - Tùy chọn:
    - `-l`: in ra chi tiết về file/thư mục (chúng ta sẽ tìm hiểu thêm về flag (cờ) sau).
    - `-a`: hiện ra file ẩn

### Sẵn sàng đi thôi

**c**hange **d**irectory
- `cd [tên_thư_mục]`
  - di chuyển từ thư mục hiện tại đến `[tên_thư_mục]`
  - nếu không đưa ra một thư mục cụ thể, mặc dịnh sẽ quay lại thư mục `/home`
  - chấp nhận cả đường dẫn tuyệt đối (`cd /home/user1/cs2043`) và tương đối (`cd cs2043`)

### Khi nào đường dẫn tương đối không được chấp nhận

**Đường dẫn tuyệt đối**
- Vị trí của file hoặc thư mục bắt đầu ở `/`

**Đường dẫn tương đối**
- Vị trí của file hoặc thư mục bắt đầu ở thư mục hiện thời

### Cách viết gọn cho đường dẫn tương đối

- `~`:  thư mục home của người dùng hiện tại
- `.`:  thư mục hiện tai (cực kì hữu ích - tôi hứa đấy!)
- `..`: thư mục cha của thư mục hiện tại

**Ví dụ**
- Nếu chúng ta bắt đầu ở `/usr/local/src`, sau đó:
  - `cd` hoặc `cd ~` => `/home/hussam`
  - `cd .` => `/usr/local/src`
  - `cd ..` => `/usr/local`

## Tạo file

Cách dễ nhất để tạo một file rỗng - hãy dùng lệnh `touch`.

Cách sử dụng:
- `touch [flags] <file>`
  - Có thể tùy chỉnh thời gian khởi tạo của một file cụ thể.
  - Nếu không sử dụng bất kì cờ (flags) nào, hệ thống sẽ dùng thời gian hiện tại.
  - **Nếu file chưa tồn tại**, lệnh `touch` sẽ tạo ra file đó.

Phần đuôi file (hay còn gọi là mở rộng của file) như .exe (file thực thi), .txt (file văn bản) trong hệ thống UNIX cũng như Window. Sử dụng lệnh `touch` để tạo một file thì ta sẽ thu được một file văn bản (text), vì vậy không cần phải thêm vào đuôi file .txt

## Tạo thư mục

Cực kì đơn giản.

**M**a**k**e **dir**ectory:
- `mkdir [flags] <thư_mục>`
  - Tạo thư mục mới.
  - Có thể sử dụng đường dẫn tương đối/tuyệt đối để tạo thư mục bên ngoài thư mục hiện tại.

## Xóa file

Không giống Window, một khi bạn đã xóa file bằng câu lệnh trong UNIX, thật không dễ dàng để bạn có thể khôi phục lại nó.
**R**e**m**ove file:
- `rm [flags] <tên_file>`
  - Xóa đi file <tên_file>
  - Sử dụng các kí hiệu (wildcards) chẳng hạn `*` để xóa nhiều file cùng lúc.
    - `rm *`: xóa hết file trong thư mục hiện tại.
    - `rm *.txt`: xóa hết file .txt trong thư mục hiện tại.
  - `rm -i <tên_file>`: thông báo, nhắc nhở trước khi xóa file đó.

## Xóa thư mục

Vì lệnh **`rm`** không xóa được thư mục. Thay vào đó ta dùng:
**R**e**m**ove **Dir**ectory.
- `rmdir [flags] <thư_mục>`:
  - Xóa một thư mục rỗng.
  - Thông báo lỗi nếu thư mục chứa bất kì nội dung nào (khác rỗng).

Xóa một thư mục và các thư mục con của nó, ta dùng lệnh **`rm`** với cờ (flag) **`-r`** (xóa một cách đệ qui (recursive)):
- `rm -r /home/user1/oldstuff`

## Sao chép dữ liệu (Copy)

**C**o**p**y
- `cp [flags] <file> <đích (destination)>`
  - Sao chép file từ nơi này sang nơi khác.
  - Để sao chép nhiều file cùng lúc, bạn có thể dùng các toán tử mở rộng (chẳng hạn **`*`**).
  - Để chép toàn bộ một thư mục, dùng lệnh `cp -r <thư_mục_nguồn (source)> <đích>`.
- Ví dụ: để sao chép toàn bộ file .mp3 vào thư mục `/Music`
  - `cp *.mp3 /home/user1/Music/`

## Di chuyển / dời file (Move)

Khác với lệnh sao chép, lệnh `mv` di chuyển thư mục một cách đệ quy mà không cần dùng flag **`-r`** (tương tự `cut` của Window).

**M**o**v**e
- `mv [flag] <nguồn> <đích>`
  - Di chuyển file hoặc thư mục từ nơi này sang nơi khác.
  - Còn dùng để **đổi tên**, `mv <tên_cũ> <tên_mới>`

## Cùng ôn lại một chút nhá

- `ls`: hiển thị nội dung của thư mục.
- `cd`: di chuyển sang thư mục khác.
- `pwd`: cho biết vị trí thư mục đang đứng.
- `rm`: xóa file.
- `rmdir`: xóa thư mục.
- `cp`: sao chép file.
- `mv`: di chuyển file.

## Giải thích về cờ/tùy chọn (flags/option)

Hầu hết tất cả các lệnh đều có cờ (flags) (còn gọi là tùy chọn (options)). Thường đi trước các đối tượng cần thực thi và bắt đầu bởi kí hiệu **`-`**.
- Một lựa chọn: `ls -l`
- Hai lựa chọn: `ls -l -a` hoặc `ls -la`
- Các lựa chọn được tính từ trái qua phải:
  - `rm -fi file` => in ra thông báo khi xóa file
  - `rm -if file` => không in ra thông báo khi xóa file

## Người bạn đồng hành cùng những câu lệnh

Làm sao để bạn có thể mường tượng được cách mà câu lệnh hoạt động như thế nào?
- Câu lệnh **Man**ual (cho biết về cách câu lệnh thực thi).
- `man <câu_lệnh>`
  - Đưa ra một trang hướng dẫn sử dụng câu lệnh đó (manpage).
  - Khác với tìm kiếm ở Web, đây là trang có sẵn của hệ thống UNIX.
  - Cho biết toàn bộ danh sách các lựa chọn / tham số đầu vào (parameter) có thể có.
  - Dùng **`/<từ_khóa(keywork)>`** để tìm kiếm `từ_khóa` trong manpage.
  - Nhấn phím `n` để tới các kết quả tìm kiếm thành công.


## Hãy cẩn thận

Có một vài sự khác biệt nho nhỏ với các lựa chọn (options) giữa các hệ thống với nhau.
- Ví dụ với lệnh `ls -B`:
  - BDS/OSX: ép các kí tự trong file in ra dưới dang `\xxx`, trong đó `xxx` là giá trị quy đổi ra số của các kí tự đó trong hệ cơ số 8 (octal).
  - Debian/Ubuntu: không liệt kê các thư mục kết thúc bởi kí tự `~`

Đây là lí do tại sao manpage là sự lựa chọn trước tiên của bạn, và Web chỉ đứng thứ hai thôi.

## Người dùng (Users), Nhóm (Groups)...

UNIX được thiết kế cho phép nhiều người dùng trên cùng một máy tính tại một thời điểm. Điều này nảy ra một vấn đề về bảo mật. Làm thế nào để đảm bảo đồng nghiệp của tôi có thể đọc thư (email), truy cập vào tài liệu hoặc thay đổi, xóa file trong khi tôi đang sử dụng chúng.
- Truy cập vào file tùy vào tài khoản (account) người dùng (user).
- Tất cả tài khoản được quản lí bởi **S**uper**u**ser (người dùng cấp cao), hay còn gọi tài khoản gốc (root account).
- Mỗi tài khoản có quyền tuyệt đối đối với file mà họ sở hữu, chỉ có thể được thay thế bởi root

## Giả thuyết Nhóm ...

File có thể được ấn định cho một nhóm các người dùng, cho phép đọc, chỉnh sửa hay/hoặc thực thi để giới hạn với nhóm người dùng nhỏ hơn.
- Ví dụ: mỗi thành viên của lớp học này được cấp một tài khoản trên cùng một máy chủ, bạn phải khéo léo để lưu giữ bài tập ở chế độ bí mật. Tuy nhiên nếu ta có một trang wiki chạy trên máy chủ này, mọi người có thể truy cập và chỉnh sửa một cách thuận tiện, ngoại trừ những người bên ngoài lớp.

## Quyền sở hữu file

- Mỗi file được gán cho một người dùng và một nhóm (thường viết dạng `user:group`).
- Ví dụ file của Alice thuộc vào `alice:user`,  file của root `root:root`.
- Phải có quyền root để thay đổi quyền sở hữu file - một người dùng bình thường không thể giành quyền sở hữu file của người khác và không thể chuyển quyền sở hữu file của họ cho người dùng khác hoặc một nhóm mà họ không tham gia.
- Để biết bạn thuộc nhóm nào, gõ `groups`.

## Tìm hiểu về quyền (Permissions)

Chúng ta có thể dùng lệnh `ls -l` để biết chủ sở hữu và quyền đối với file đó.
- `ls -l`: liệt kê file và thư mục với định dạng dài (thêm nhiều thông tin hơn).
- Ví dụ: `-rw-r--r-- 1 hussam users 3775 2009-08-17 15:52 index.html`

## Phân tích định dạng (format)

**-{% em type="red" %}rwx{% endem %}{% em type="blue" %}rwx{% endem %}{% em type="green" %}rwx{% endem %}**

- {% em type="red" %}Quyền người dùng{% endem %}
- {% em type="blue" %}Quyền của nhóm{% endem %}
- {% em type="green" %}Quyền của người/nhóm khác{% endem %}
- R = Read (đọc), W = Write (viết, ghi), X = Execute (thực thi).
- Thư mục bắt đầu bởi kí tự **`d`** thay vì **`-`**.

Vậy  định dạng `-rw-rw-r--` có nghĩa gì?
- Người dùng và nhóm của họ có thể đọc và ghi trên file đó, còn bất kì ai khác chỉ có thể đọc.

## Thay đổi quyền

Người dùng bình thường không thể thay đổi file hệ thống và cài đặt chương trình. Đó là một lợi thế rất lớn của UNIX mà nó có chặn được rất nhiều đoạn mã độc gây hại cho hệ thống. Với ý nghĩ đó, làm thế nào để bạn có thể thay đổi quyền đối với các file của bạn?
- **Ch**ange **Mod**e
- `chmod <chế_độ (mode)> <file/thư_mục>`
- Thay đổi quyền dựa trên mode.
- Định dạng của mode là sự kết hợp của 3 trường (fields):
  - Ai bị ảnh hưởng, có thể kết hợp các flags: `u`, `g`, `o` hoặc `a` (tất cả).
  - Thêm vào hay bớt đi quyền: **`+`** hoặc **`-`**.
  - Loại quyền nào được thêm vào hay bớt đi - kết hợp của `r`, `w` và `x`.

Ví dụ:
- `chmod ug+rw myfile`: thêm quyền đọc và thực thi cho người dùng và nhóm.
- `chmod a-r myfile`: bỏ đi quyền đọc file với tất cả mọi người.
- `chmod ugo-rwx myfile`: bỏ đi hết quyền của file.

**Một vài tiện ích**
- Xem các flags `r`, `w` và `x` như là các biến nhị phân.
  - 1: bật (ON)
  - 0: tắt (OFF)
- $$`r` \over {2^2} + `w` \over {2^1} + `x` \over {2^0}$$


a













