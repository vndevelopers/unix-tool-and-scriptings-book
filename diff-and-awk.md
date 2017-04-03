diff và awk

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









