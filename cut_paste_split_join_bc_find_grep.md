# cut, paste, split, join, bc, find, grep

## Cắt (cut) và dán (paste) không sử dụng chuột và cửa sổ giao diện

## **Cắt chuỗi**

Rút trích ra từng phần từ mỗi dòng của dữ liệu đầu vào.
- `cut [-b] [-c] [-d delim] [-f list] [-s] [file]`
  - `delim` là dấu phân/ngăn cách các trường (fields) riêng biệt với nhau.
  - `list` bao gồm một trong các giá trị sau N, N-M, N-

Options (tùy chọn):
- `-b`: trích xuất dữ liệu theo một khoảng các byte.
- `-c`: trích xuất dữ liệu theo một khoảng các kí tự.
- `-d`: một dấu ngăn cách cụ thể (mặc định là **`tab`** (**`\t`**))
- `-f`: ngăn cách một khoảng các trường riêng biệt một cách cụ thể bởi dấu ngăn cách.
- `-s`: chặn dòng lại nếu không tìm thấy dấu ngăn cách.

## Ví dụ về cắt chuỗi

Ta có file **employee.txt** với nội dung như sau:
- Alice:607-233-2464:15 Sunny Place, Ithaca, NY:14850:female
- Bob:607-257-2884:504 Brown St, Ithaca, NY:14850:male
- Charlie:605-987-7886:99 Berry Lane, Palo Alto, CA:94304:male
- This line doesn't have a demiliter

Ví dụ:
- cut -d : -f 1 -s employee.txt: in ra tên
- cut -d : -f 3,4 -s employee.txt: in ra địa chỉ và mã bưu điện (mã vùng)
- cut -d : -f 2 employee.txt: in ra số điện thoại và dòng cuối cùng
- cut -d : -c 1 employee.txt: in ra kí tự đầu tiên và kí tự đầu tiên của dòng cuối.

## Dán (paste)

Dán nối tiếp các file cạnh nhau
- `paste [option] [file_1 ...]`

Option:
- `-d`: ngăn cách các trường riêng biệt bằng kí tự cụ thể (thay cho **`tab`**).
- `-s`: dán một cách tuần tự thay vì cạnh nhau.

## Ví dụ về `paste` (1/3)

names.txt
  - Alice
  - Bob
  - Charlie
 
phones.txt
  - 607-233-2464
  - 607-257-2884
  - 605-987-7886

Ví dụ:
- `paste names.txt phones.txt`:
- Alice 607-233-2464
- Bob 607-257-2884
- Charlie 605-987-7886

## Ví dụ về `paste` (2/3)

names.txt
  - Alice
  - Bob
  - Charlie
 
phones.txt
  - 607-233-2464
  - 607-257-2884
  - 605-987-7886

Ví dụ:
- `paste -d : names.txt phones.txt`:
- Alice:607-233-2464
- Bob:607-257-2884
- Charlie:605-987-7886

## Ví dụ về `paste` (3/3)

names.txt
  - Alice
  - Bob
  - Charlie
 
phones.txt
  - 607-233-2464
  - 607-257-2884
  - 605-987-7886

Ví dụ:
- `paste -s : names.txt phones.txt`:
- Alice Bob Charlie
- 607-233- 607-257-2884 605-987-7886

## Chia nhỏ file (split)

Chia file thành nhiều mẫu nhỏ, chẳng hạn: các file mới xaa, xab, ...
- `split -option file_1 [prefix]`
- Tùy chọn:
  - `-l`: số dòng trong mỗi file.
  - `-b`: số byte trong mỗi file.
  - `-prefix`: tên tiền tố của các file được xử lí.

## Gộp file (join)

Gộp những dòng có từ khóa giống nhau giữa hai file khác nhau.
- `join [option] file_1 file_2`
- Tùy chọn:
  - `-1 field`: gộp theo trường (field) của file 1.
  - `-2 field`: gộp theo trường (field) của file 2.
  - `-a xxx`: hiển thị các dòng không có cặp trùng của file xxx.

## Ví dụ gộp file

age.txt
- Alice 12
- Bob 30
- Charlie 23

salaries.txt
- Bob 129,000
- Charlie 75,000

`join age.txt salaries.txt`
- Bob 30 129,000
- Charlie 23 75,000

`join -a1 age.txt salaries.txt`
- Bob 30 129,000
- Charlie 23 75,000
- Alice 12

## Tính toán cơ bản (basic calculator)

Thực hiện những phép toán cơ bản của số học và logic.
- Tùy chọn:
  - `-l field`: tăng độ chính xác lên đến 20 chữ số, mặc định là 0.

Ví dụ:
- `echo "1/3" | bc`
  - 0
- `echo "1/3" | bc -l`
  - 0.33333333333333333333
- `echo "1>3" | bc -l`
  - 0
- `echo "1<3" | bc -l`
  - 1























