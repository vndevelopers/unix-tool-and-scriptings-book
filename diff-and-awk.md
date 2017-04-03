# diff và awk

### Lưu ý về lệnh sed

```
sed 's/regexp/string/ file'
```

* Xử lí từng dòng một trong bộ nhớ chính.
* Gửi đầu ra đến stdout \(xuất chuẩn\)
* Không thay đổi file.

Đừng bao giờ thực hiện câu lệnh này:

```
sed 's/regexp/string/ file' > file
```

* file sẽ được thay thế bởi file rỗng trước khi sed bắt đầu xử lí

```
sed 's/regexp/string/' file > outfile
```

* Xử lí từng dòng một trong bộ nhớ chính.
* Gửi đầu ra đến outfile
* Không thay đổi file
* Kiểm tra outfile cho đầu ra mong đợi.
* Sau đó đổi tên file
* ```
  mv outfile file
  ```

  Làm thế nào để kiểm tra đầu ra?

### Câu lệnh diff

```
diff file1 file2
```

* n{c,a,d}m: sự thay đổi trên 1 dòng \(c\), thêm vào \(a\), xóa đi \(d\) xảy ra trên dòng n của file1 so với dòng m của file2

* &lt;: nghĩa là dòng đó không có trong file1

* &gt;: nghĩa là dòng đó không có trong file2

### Giới thiệu về AWK

AWK là một loại ngôn ngữ dành cho việc xử lí văn bản - cơ sở dữ liệu

* Cho phép ta dễ dàng thao tác trên nhiều trường \(fields\) thay vì trên tất cả các dòng
* Hoạt động theo pattern-action \(mẫu-thao tác\) giống như sed
* Hỗ trợ các loại số \(và các phép tính\) cùng luồng điều khiển \(trạng thái if-else\)
* Mở rộng về các loại chuỗi và mảng \(tập hợp mảng\)

### AWK không phải là awkward \(vụng về\)

* Được tạo ra ở Bell Lab vào năm 1970 bởi  Alfred **A**ho, Peter **W**einberger, and Brian **K**ernighan \(awk\)
* Là tổ tiên của ngôn ngữ Perl và họ hàng với

  * sed -P

* Rất nhiều công dụng.

### Bạn đã từng biết đến gawk?

* gawk là hiện thực hóa của GNU với chương trình ngôn ngữ AWK. Trên BSD/OS X nó là awk.
* awk cho phép ta thiết lập các filters \(bộ lọc\) để xử lí văn bản dễ dàng như các con số \(và nhiều hơn nữa\)
* Cấu trúc cơ bản của một chương trình awk
* ```
  pattern1 {command}
  pattern2 {command}
  ```
* Mẫu có thể là các biểu thức chính quy. Gawk đến từng dòng một, kiểm tra từng mẫu một và nếu nó được tìm thấy, thì câu lệnh sẽ được thi hành.

### Tại sao lại là gawk mà không phải sed?

* Tiện lởi cho việc xử lí số.
* Biến số và luồng điều khiển trong các thao tác.
* Cách tiện lợi để truy cập vào các trường bên trong các dòng.
* Linh động trong việc in ra.
* Có sẵn các hàm toán học và chuỗi.

### Vài ví dụ đơn giản

```
gawk '/[Mm]onster/ {print}' Frankenstein.txt
gawk '/[Mm]onster/' Frankenstein.txt
gawk '/[Mm]onster/ {print $0}' Frankenstein.txt
```

* In ra tất cả các dòng trong file Frankenstein có chứa từ Monster hoặc monster
* Nếu bạn không chỉ rõ thao tác, gawk sẽ mặc định in ra các dòng đó.
* Tham số $0 được xem như dòng đầy đủ.
* Gawk hiểu được các biểu thức chính quy mở rộng, vì vậy chúng ta không cần phải thêm +, ?, ...

### Begin và End

* Gawk cho phép một đoạn code chỉ được thực thi một lần duy nhất , tại lúc bắt đầu hoặc lúc kết thúc

```
gawk 'BEGIN {print "Starting search"}
    /[Mm]onster/ { count++}
END {print "Found " count " monsters in the book!}
' Frankenstein.txt
```

* Gawk không yêu cầu phải khởi tạo giá trị cho biến
* Số nguyên được mặc định là 0, còn chuỗi là "" \(NULL\)



