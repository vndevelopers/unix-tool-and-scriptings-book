# Regular Expressions - Biểu thức chính quy

**Regular Expressions**
- Một cấp độ mới về làm chủ dữ liệu.
- Mẫu khớp với biểu thức chính quy thì phức tạp hơn và vượt trội hơn việc mở rộng shell.
- Biểu thức chính quy là tập các chuỗi khớp với biểu thức.
- Đặc tính cơ bản trong hàng loạt các ngôn ngữ (java, C#, python, ruby, ...).
- Rất nhiều công cụ (tool) trong Unix lấy biểu thức chính quy làm đầu vào của nó, chẳng hạn như lệnh grep.
- Biểu thức chính quy có cú pháp khác với shell mở rộng.
- Chúng ta đặt chúng trong dấu nháy đơn để phân biệt với shell mở rộng.

## Quy tắc của biểu thức chính quy

Một vài biểu thức chính quy (viết tắt RegExp) thực hiện cùng một nhiệm vụ theo kí tự đại diện đã được chúng ta định nghĩa trước đó.
- Single character:
  - Wildcard: **`?`** RegExp: **`.`**
    - Khớp bất kì kí tự đơn nào.
  - Wildcard: **`[a-z]`** RegExp: **`[a-z]`**
    - Khớp một trong các kí tự đã cho biết.
    - Không ngăn cách đa kí tự bởi dấu **`,`** trong RegExp. (e.x: **`[a,b,q-v]`** thành **`[abq-v]`**).