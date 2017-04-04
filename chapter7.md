## ssh, scp, processes: nice, kill, top; jobs

### Truy cập từ xa

Bạn có thể sử dụng "shell bảo mật" \(secure shell - ssh\) để kết nối với một máy tính từ xa.

```
ssh [username@]<địa chỉ IP máy tính từ xa>
```

* Nếu bỏ trống `username` thì sẽ dùng `username` của máy hiện tại \(máy client\)
* Máy tính từ xa phải được cấu hình chấp nhận kết nối `ssh` :
  * ssh deamon \(dịch vụ ssh\) phải đang chạy và lắng nghe trên một cổng mạng đang được mở \(mặc định là cổng số 22\)

### Thực thi lệnh từ xa

ssh có thể được dùng để thực thi nhiều lệnh trên máy tính từ xa. Ví dụ

```
ssh ha232@csug01.csuglab.cornell.edu ls
```

Dòng lệnh này sẽ thực thi lệnh `ls` trên máy tính `csug01.csuglab.cornell.edu` và dữ liệu xuất ra màn hình trước khi `ssh` đóng kết nối.

* Cờ \(flag\) `-f` sẽ làm cho `ssh` chạy nền trước khi chạy câu lệnh từ xa.
* Cờ \(flag\) `-Y` hoặc `-X` \(tương tác\) sẽ chuyển tiếp chế độ X11 \(giao diện người dùng\) đến máy client.

Ví dụ này sẽ chạy trình duyệt Firefox trên máy tính từ xa

```
ssh -Y ha232@csug01.csuglab.cornell.edu firefox
```

### Tập tin xác nhận

* Một tập tin xác nhận sẽ xác thực với máy tính từ xa thay vì phải sử dụng cặp username/password.
* Cho phép bạn xác thực bản thân 1 bước nữa bởi `cụm từ xác nhận` \(có thể trống\)
* Thường bao gồm một cặp khóa `công cộng / riêng` cho việc mã hóa bất đối xứng \(ví dụ như RSA\)

Nếu bạn không muốn nhập mật khẩu mỗi lần đăng nhập thì có thể

```
ssh-keygen -t dsa
```

sau đó làm theo hướng dẫn, rồi thêm khóa công cộng mà bạn vừa tạo được \(thường nằm ở `~/.ssh/id_rsa.pub`\) vào tập tin `~/.ssh/authorized_keys` trên máy tính từ xa.

### Tập tin cấu hình ssh

Nếu bạn không muốn phải thiết lập những `cờ` \(flags\) lặp lại nhiều lần, hãy sử dụng tập tin cấu hình ssh `~/.ssh/config`

Dưới đây là một tập tin cấu hình mẫu

```
host office
hostname mishmish.cs.cornell.edu

host tiger
hostname tiger.cs.cornell.edu
user Alice
ForwardX11 yes
IdentityFile ~/.ssh/id_rsa
```

Từ đây, lệnh `ssh office` sẽ kết nối tới `mishmish.cs.cornell.edu` và `ssh tiger` sẽ kết nối tới `tiger.cs.cornell.edu` với username là `Alice`, sử dụng file xác nhận `~/.ssh/id_rsa` và chuyển tiếp X11.

### Sao chép bảo mật \(secure copy - scp\)

* Sao chép tập tin một cách bảo mật qua mạng lưới bằng việc sử dụng mã hóa truyền tải ssh.

Sao chép tập tin tới một máy tính từ xa

```
scp file [username]@remote_machine:
```

Sao chép tập tin từ một máy tính từ xa

```
scp [username]@remote_machine:file .
```

* Cần phải có dấu ':' sau tên/địa chỉ của máy tính từ xa. Đường dẫn trên máy tính từ xa bắt đầu từ thư mục home có thể được xác định sau dấu ':'

Sao chép thư mục bằng việc sử dụng cờ -r

```
scp -r pics/ remote_machine:
```

### Những lệnh truyền tải dữ liệu khác

#### wget

```
wget [tùy chọn] [URL]
```

Tải về tập tin từ một địa chỉ từ xa thông qua giao thức HTTP. Những tùy chọn phổ biến:

* -r: sao chép đệ quy.
* -l\[số\]: có bao nhiêu mức độ giảm xuống khi đi theo đường dẫn.
* -c: tiếp tục tải về từng phần

#### curl

```
curl [tùy chọn] [URL...]
```

Truyền tải dữ liệu từ/tới máy chủ web

Để có thêm thông tin về các lệnh này, tham khảo trang chủ của nó.

## Processes \(tiến trình\) và Jobs \(công việc\)

### Tiến trình? Tiến trình là gì?

Định nghĩa: tiến trình là một phần đang được thực thi \(instance\) của một chương trình đang chạy. Một chương trình có thể có nhiều instance khác nhau. Mỗi instance tương đương với một tiến trình.

* Cụ thể hơn một chương trình vì nó đang được thực thi
* Cụ thể hơn một chương trình đang chạy vì một chương trình tương tự có thể chạy đồng thời nhiều lần hoặc nhiều tiến trình 

Ví dụ: nhiều người dùng có thể chạy đồng thời một chương trình trên cùng một máy tính. Mỗi instance của chương trình đang chạy là những tiến trình riêng biệt.

### Định danh tiến trình

Làm sao ta có thể giao tiếp với một tiến trình từ tiến trình khác?

* Mỗi tiến trình được ấn định duy nhất một "process ID \(định danh tiến trình - PID\)" khi nó được khởi tạo
* Những PID này khác nhau giữa các instance riêng biệt của cùng một chương trình.

Lệnh lấy thông tin của các tiến trình:

```
ps [tùy chọn]
```

* Ghi lại thông tin của các tiến trình đang chạy, gồm cả PID

Mặc đinh, lệnh ps không hoàn toàn hữu ích vì nó chỉ liệt kê các tiến trình được bắt đầu bởi người dùng trong thiết bị đầu cuối \(terminal\) hiện tại. Thay vào đó ta có thể ...

* ps -e: liệt kê tất cả các tiến trình đang chạy trong hệ thống
* ps -ely: cho nhiều thông tin về tiến trình hơn những gì bạn mong đợi
* ps -u username: liệt kê tất cả các tiến trình của người dùng có tên username.

Để lấy thông tin về một tiến trình cụ thể, sử dụng kĩ thuật đường ống và lệnh grep

```
ps -e | grep firefox
```

* Hiển thị các thông tin của tất cả tiến trình firefox

### Đa nhiệm \(Multitasking\)

* Lưu ý rằng dù hệ thống UNIX dường như chạy hàng chục hay hàng trăm tiến trình cùng lúc, nhưng một CPU chỉ có thể chạy một tiến trình tại một thời điểm.
* Việc chuyển đổi giữa các tiến trình làm ta nghĩ rằng chúng đang chạy đồng thời.

### Độ ưu tiên \(Priority\)

* Giả sử rằng bạn muốn chạy một chương trình tính toán khoa học trong một thời gian dài có thể là vài ngày và nó ngốn hết 100% CPU. Những người dùng khác thấy vậy và nghĩ rằng bạn không tôn trọng họ \(ngốn hết tài nguyên\).
* Có cách nào để báo cho máy chủ giảm độ ưu tiên cho tiến trình của bạn?
* Có cách nào để tăng độ ưu tiên cho những công việc quan trọng?

* Những lập trình viên của UNIX thấy được điều này và họ ấn định cho mỗi tiến trình một giá trị ưu tiên khi nó khởi chạy.

### Trở nên thân thiện trong mắt mọi người!

Bắt đầu chạy một tiến trình mà chưa có độ ưu tiên mặc định

Câu lệnh nice

```
nice [tùy chọn] câu_lệnh
```

* Chạy câu lệnh với một giá trị nice cụ thể \(mặc định là 10\)
* Giá trị nice nằm trong khoảng -20 \(độ ưu tiên cao nhất\) và 19 \(độ ưu tiên thấp nhất\)
* Chỉ có root mới cho tiến trình một giá trị nice âm
* Chạy câu lệnh mà không có nice thì có độ ưu tiên 0

Ví dụ

```
nice -n 10 azureus
```

Tiếp tục kéo torrent tiếp theo đoạn đã tải về với hết tài nguyên máy.

### Tùy chỉnh độ ưu tiên









