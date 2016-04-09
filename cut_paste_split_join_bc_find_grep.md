# cut, paste, split, join, bc, find, grep

## Cắt (cut) và dán (paste) không sử dụng chuột và cửa sổ giao diện

### **Cắt chuỗi**

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