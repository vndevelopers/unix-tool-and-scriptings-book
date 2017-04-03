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





