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



