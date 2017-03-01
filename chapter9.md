# sed, cron

## sed

Chúng ta sẽ sử dụng sed như là một công cụ chỉnh sử luồng \(stream editor\), nhưng thật ra thì nó là một ngôn ngữ lập trình hoàn chỉnh.

`sed [options] [script] [file]`

* Công cụ chỉnh sửa luồng cho việc lọc và biến đổi chuỗi
* Chúng ta sẽ tập trung vào cú pháp ``sed 's/<regexp>/<text>` [file]``
* Mẫu này sẽ thay thế mọi chuỗi khớp với biểu thức `<regexp>` bằng chuỗi `<text>`
* `sed` sẽ tìm kiếm từng dòng một theo biểu thức chính quy

### sed và tr

Điều khác biệt giữa `sed` và `tr` là gì ?

* `sed` có thể so khớp biểu thức chính quy
* `sed` có thể thay thế nhiều thứ hơn nữa chứ không đơn thuần các mẫu tự

### Ví dụ đơn giản

`sed 's/not guilty/guilty/g' filename`

Câu lệnh này sẽ thay thế **not guilty** thành **guilty** trong nguồn input và xuất ra luồng stdout

Sẽ thế nào nếu chúng ta không có tham số **g** ?

Nếu không có tham số **g**, nó chỉ thực hiện thay thế 1 lần trên mỗi dòng.

### sed trong việc xóa

Tương tự như `tr` chúng ta có thể thực hiện việc xóa với `sed`

`sed '/regexp/d'` - sẽ xóa tất cả những dòng có chứa nội dung khớp với biểu thức **regexp**

**Ví dụ:**

`sed '/[Dd]avid/d' filename > filename2`

Lệnh này sẽ xóa tất cả các dòng có chứa từ **David** hoặc **david**, sau đó lưu vào file có tên là **filename2**

### sed hiểu biểu thức chính quy

`sed ’s/[[:alpha:]]\{1,3\}[[:digit:]]*@cornell\.edu//g’`

**Câu hỏi**: câu lệnh này sẽ làm gì ?

sử dụng `-r` trên Linux \(`-E` trên OS X\) để sử dụng biểu thức chính quy mở rộng.

### sed rất tham lam

sed sẽ so khớp biểu thức chính quy được cung cấp với chuỗi dài nhất mà nó có thể

```
$ echo filename1
a b col d e f lapse h i j k lapse m n
$ sed 's/col.*lapse/collapse/g' filename1
a b collapse m n
$ echo filename2
a b c col d e f col g h i lapse
$ sed 's/col.*lapse/collapse/g' filename2
a b c collapse
```

### sed có thể lưu kết quả khớp

* sed có thể lưu kết quả khớp trong những thanh ghi
* chúng ta sẽ dụng những ngoặc đơn để đánh dấu những kết quả khớp
* kết quả khớp được lưu trong thanh ghi `\1`, kết quả khớp thứ 2 sẽ lưu trong thanh ghi `\2` và cứ thế.

**Ví dụ:**

```
sed 's/^\([A-Z][A-Za-z]*\), \([A-Z][A-Za-z]*\)/\2 \1/'
```

* Tìm kiếm những từ bắt đầu với ký tự hoa ở đầu dòng, phân chia bằng 1 dấu phẩy và một khoảng trắng
* Đặt biểu thức vào bên trong dấu ngoặc** \( \) **để chỉ cho công cụ chỉnh sửa sẽ lưu kết quả khớp
* Vì **\( \) **là ký tự đặc biệt nên chúng ta sẽ **escape** chúng.
* Chúng ta truy cập kết quả khớp được lưu bằng thanh ghi `\1` và `\2`
* Đoạn mã này có thể chuyển đổi một dữ liệu có dạng từ **Lastname, Firstname** thành **Firstname Lastname**

### Lựa chọn dòng

Bạn có thể lựa chọn cụ thể những dòng bằng con số hoặc biểu thức chính quy

* `sed '1,20s/john/John/g' file` - kiểm tra dòng 1 đến dòng 20
* `sed '/^The/s/john/John/g' file` - kiểm tra dòng bắt đầu bằng từ **The**

Ký tự `&` sẽ đại diện cho toàn bộ kết quả khớp:

`sed 's/[a-z]\+/"&"/g'`

sẽ thay thế các từ bằng chính các từ nhưng trong ngoặc kép

### Và còn hơn thế nữa với sed

Làm sao chúng ta sử dụng sed để bỏ những từ khớp biểu thức chính quy ? `sed 's/regexp//g' file`

Ví dụ: 

`sed 's/[[:alnum:]]//g' Frankenstein.txt`

Tiếp theo chúng ta sẽ cắt bỏ tiền tố của đường dẫn thư mục \(ví dụ chuyển từ `/usr/local/src` thành `src`\)

Ví dụ:

`pwd | sed 's/.*\///'`

* Biến đổi tất cả những gì nằm trước dấu `/` thành không có gì
* Chú ý là dấu `\` là để escapse dấu `/`

### Mã sed

sed là một ngôn ngữ lập trình hoàn chỉnh và ta có thể viết những đoạn mã sed.

* Mọi file bắt đầu bởi `#!` để là một file mã

Ví dụ:

Tạo một file mã có tên là trim.sed

```
#! /usr/bin/sed -f
s/^ *//
s/ *$//
```

Bạn có thể chạy đoạn mã này từ shell như mọi chương trình khác

```
$ echo " this is a test " | ./trim.sed
this is a test
```

Bây giờ chúng ta đã có một đoạn mã nhắm cắt bỏ khoảng trắng đầu chuỗi

### Sử dụng sed trong vim

Thay thế mẫu khớp với biểu thức chính quy bằng một chuỗi:

`:%s/regexp/string/[options]`

### Trò chơi Arkanoid bằng sed

sed là một một ngữ lập trình hoàn chỉnh. Thực tế rằng có người đã viết một trò chơi chỉ bẳng mã sed.

![](/images/chap9/sed-arkanoid.png)

[_http://aurelio.net/soft/sedarkanoid/_](http://aurelio.net/soft/sedarkanoid/)

Và còn nhiều hơn nữa về sed tại :

[http://www.grymoire.com/Unix/Sed.html](http://www.grymoire.com/Unix/Sed.html)

### cron

cron là một chương trình cho phép những người dùng unix thực thi những câu lệnh hoặc đoạn mã một cách tự động vào một thời gian xác định.

* cron là một dịch vụ chìm, nghĩa là chỉ cần chạy nó lên một lần, sau đó sẽ tự sắp xếp ngủ đông tới khi nó cần chạy
* Được cài trên hầu hết phiên bản Linux và được chạy bởi một đoạn mã khởi động cùng hệ thống, vì thế bạn không cần phải chạy nó một cách thủ công
  * Có thể kiểm tra bằng `ps -e | grep cron`
  * Tùy theo hệ điều hành mà nó có thể hiển thị là **cron** hay **crond**
* Chúng ta có thể kiểm soát và điều khiển dịch vụ cron bằng nhiều khác nhau...

### cron và root

Nếu bạn nhìn vào thư mục `/etc`, bạn có thể tìm thấy các thư mục con có tên

* cron.hourly
* cron.daily
* cron.weekly
* cron.monthly
* Nếu bạn đặt những đoạn mã vào những thư mục này, nó sẽ được chạy mỗi phút, mỗi ngày, mỗi tuần, mỗi tháng tùy theo tên của thư mục

* Chú ý: Nếu chúng ta làm thế với mã sao lưu dữ liệu thì chúng ta nên thay thế **~** thành **/home/hussam** vì đoạn mã sẽ được chạy dưới quyền root.

### Sự linh động của cron

Nếu bạn muốn linh động hơn trong việc đặt kế hoạch chạy thì bạn có thể chỉnh sửa file crontab

* Những file crontab là những file cấu hình của cron
* Bạn có thể tạo ra nó mà không cần quyền root !

Chạy lênh `cat /etc/crontab` để có một cái nhìn vào file

```
# /etc/crontab: system-wide crontab
# Unlike any other crontab you don’t have to run the ‘crontab’
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# that none of the other crontabs do.
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin
# m h dom mon dow user command
17 * * * * root cd / && run-parts --report /etc/cron.hourly
25 6 * * * root test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6 * * 7 root test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6 1 * * root test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc cron.monthly )
```

### Cú pháp crontab

```
a.    b.    c.    d.    e.    [câu lệnh sẽ được chạy]
```

* a. phút \(0-59\)
* b. giờ \(0-23\)
* c. ngày trong tháng \(1-31\)
* d. tháng \(1-12\)
* e. thứ trong tuần \(0-6\) \(chủ nhật = 0\)

Giá trị có thể là \* \(tất cả các giá trị hợp lệ\), một khoảng thì cách nhau bởi dấu gạch ngang, một số, một tập hợp các giá trị cách nhau bởi dấu phẩy hoặc một bước nhảy \(ví dụ \*/2 sẽ là mỗi 2 giờ\)

### crontab cho nhiều người dùng

* Để sửa file crontab của bạn, gõ `crontab -e`
* Để xem file crontab của bạn, gõ `crontab -l`
* Để xóa file crontab của bạn, gõ `crontab -r`

Một file mẫu:

```
30    18    *    *    *    /home/hussam/backup.sh
```

Nó sẽ chạy mã sao lưu mỗi ngày vào lúc 6:30 chiều.

