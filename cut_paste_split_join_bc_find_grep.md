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

Ví dụ về `paste` (1/3)
- names.txt
  - Alice
  - Bob
  - Charlie
- phones.txt
  - 607-233-2464
  - 607-257-2884
  - 605-987-7886

































