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



