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

