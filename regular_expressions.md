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

Ví dụ:
- `grep 't.a'`: in ra tất cả các dòng có chứa các từ như tea, taa, and steap ...

## Cảnh báo

Giống như kí tự mở rộng của shell, RegExp là trường hợp nhạy cảm. Điều gì sẽ xảy ra nếu bạn muốn khớp bất kì kí tự nào theo trường hợp bên dưới?
- `[a-Z]` sẽ khớp với các kí tự nào?

Phân bố, sắp xếp kí tự:
- Mỗi loại ngôn ngữ, chương trình sắp xếp các kí tự theo các cách khác nhau. Trong ngôn ngữ lập trình C, các kí tự từ A-Z sẽ được ấn định bởi các số từ 65-90, trong khi đó từ a-z là 97-122. Vì vậy khoảng từ `[a-Z]` là 65-122. 
  - Có vài các kí tự không thuộc alphabet trong khoảng `[a-Z]`.
  - Để chỉ ra các từ một cách an toàn và rõ ràng chúng ta nên dùng `[a-zA-Z]`.
- Chú ý: không phải mọi ngôn ngữ đều sắp xêp giống C. Ví dụ, một từ điển có thể sắp xếp các kí tự theo kiểu aAbBcC...

## May mắn thay, chúng ta có thể lấy các khoảng này một cách dễ dàng

Những cách viết gọn cho các khoảng của các kí tự:
- Lớp các kí tự POSIX (tham khảo POSIX tại: [](https://en.wikipedia.org/wiki/POSIX))
  - `[:alnum:]`: các kí tự số
  - `[:alpha:]`: các kí tự alphabetic
  - `[:digit:]`: số
  - `[:punct:]`: các kí tự dấu chấm câu (chẳng hạn: !, ., ?...)
  - `[:lower:]`: các kí tự viết thường
  - `[:upper:]`: các kí tự viết hoa
  - `[:lower:]`: các kí tự khoảng trắng (space, tab, ...)

Ví dụ:
- `ls | grep [[:digit:]]`: liệt kê tất cả các file có chứa số trong tên file.












