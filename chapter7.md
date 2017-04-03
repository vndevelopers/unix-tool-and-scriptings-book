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



### Processes \(tiến trình\) và Jobs \(công việc\)



























