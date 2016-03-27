# wc, sort, uniq, tr, kỹ thuật đường ống và điều hướng, tee, backticks

## Vim: Mẹo nhỏ của ngày !

**Hiển thị số dòng code trong Vim**

```
:set nu
```

**Ẩn số dòng code trong Vim**

```
:set nonu
```

**Đi đến một dòng bất kì theo số**

```
:số_thứ_tự_dòng
```

## Đếm

**wc**

- Có bao nhiêu dòng code trong chương trình tuyệt vời của tôi ?
- Có bao nhiêu từ trong tài liệu ?
- Tốt cho việc *chém gió* (nói dóc)

**Đếm số từ, ký tự, lòng và byte với `wc`**

- `wc -l` : đếm số dòng
- `wc -w` : đếm số từ
- `wc -m` : đếm số ký tự
- `wc -c` : đếm số bytes

## Sắp xếp

**sort**

Sắp xếp các dòng của file chuỗi theo (a -> z)
- `sort -ru file`
    - sắp xếp `file` theo ký tự ngược lại (reverse) và bỏ các dòng trùng lắp
- `sort -n -k 2 -t : file`
    - sắp xếp file theo số nằm ở cột thứ 2, các cột cách nhau bởi dấu hai chấm `:`

*Ví dụ :*
Giả sử có 1 file (numbers.txt) với các số 1, 5, 8, 11, 62 nằm ở các dòng khác nhau, thì:

```
$ sort numbers.txt
1
11
5
62
8
```

```
$ sort numbers.txt -n
1
5
8
11
62
```

## Duy nhất

**uniq**

- `uniq file` - Bỏ qua tất cả các dòng có giá trị trùng
- `uniq -c file` - Bỏ qua tất cả các giá trị trùng, nhưng có thêm số lần lặp ở trước mỗi dòng

## Xử lý ký tự !

**Hàm thông dịch ký tự**

`tr [các tùy chọn] <danh sách ký tự 1> [danh sách ký tự 2]`
- Thông dịch hay xóa bỏ các ký tự
- Danh sách ký tự là một chuỗi các ký tự
- Mặc định, tìm kiếm ký tự ở **danh sách ký tự 1** và thay thế bằng ký tự có vị trí tương ứng ở **danh sách ký tự 2**

**Ví dụ:**

`tr 'AEUIOU' 'aeiou'` - thay thế các nguyên âm viết hoa thành nguyên âm viết thường

## Kỹ thuật đường ống và chuyển hướng (pipes and redirection)

- `tr` chỉ nhận đầu vào (input) chuẩn (stdin)
    - ví dụ: đầu vào từ bàn phím
- Thế nếu chúng ta muốn làm việc với file thì sao ?
    1. Kỹ thuật đường ống (piping) : `cat somefile | tr 'AEUIOU' 'aeiou'`
    2. Chuyển hướng đầu vào : `tr 'AEUIOU' 'aeiou' < somefile`

> Kỹ thuật đường ống và chuyển hướng đầu vào / ra rất là quan trọng và hữu ích trong suốt UNIX

## Ôn lại về chuyển hướng

**Ứng dụng trong UNIX được giao tiếp với luồng đầu vào / ra (Input / Output) :**
- \#0 : luồng đầu vào chuẩn; STDIN (thường là bàn phím)
- \#1 : luồng đầu ra chuẩn; STDOUT (thường là cửa sổ dòng lệnh)
- \#2 : luồng báo lỗi chuẩn; STDERR (phụ thuộc theo cấu hình hệ thống, nhưng thường là cửa sổ dòng lệnh)

**Triết lý UNIX**

> Trong UNIX, bạn sẽ tìm ra nhiều công cụ đặc trưng trong 1, 2 thứ, và chúng làm nó rất tốt! Để làm những chức năng phức tạp hơn bằng cách ghép nối từng công cụ một bằng kỹ thuật đường ống hoặc chuyển hướng vào/ra

## Luồng dữ liệu chuẩn

![Standard Stream](images/chap5/standard_streams.png)
