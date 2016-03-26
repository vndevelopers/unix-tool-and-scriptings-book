# Tóm lược về UNIX

## Mục tiêu khóa học

**Đào tạo chuyên sâu từ cơ bản đến nâng cao các công cụ và ngôn ngữ kịch bản của UNIX** : chúng ta sẽ học cách gắn kết các chương trình đơn giản lại với nhau để thực thi những tác vụ cực kỳ hiệu quả.

**Một số chủ đề bao gồm :**
- Shell, hệ thống file Unix và các công cụ đơn giản.
- Gắn kết các công cụ, chương trình với nhau (kỹ thuật đường ống)
- Một số công cụ phức tạp
- Biểu thức chính quy (RegEx)
- Xử lý luồng (stream)
- Kịch bản xử lý (scripting)
- Ngôn ngữ kịch bản
- Ngôn ngữ Python


## Script là gì ?
Là những chương trình dành cho những môi trường có thể diễn giải và tự động thực thi các tác vụ mà có thể thay thế bằng cách thực thi từng tác vụ một. (Wikipedia)

- Thông dịch (không phải biên dịch)
- Ít sử dụng các cấu trúc dữ liệu
- Thường xuyên sử dụng trong việc xử lý luồng (stream)

### Ví dụ đơn giản
Chúng ta cần đổi quy ước đặt tên của hàng triệu files từ `24-09-2007-picturename.jpg` thành `2007-09-24-picturename.jpg` (đổi từ tiền tố ngày `dd-mm-YYYY` sang `YYYY-mm-dd`)

```shell
for fn in *.jpg
  do mv $fn ‘echo $fn |\
  sed ‘s/([0-9]+)-([0-9]+)-([0-9]+)/\3-\2-\1/’‘
done
```

### Yêu cầu cơ bản
- Không cần thiết đã biết qua môi trường UNIX
- Khóa học này bao gồm CS 2042 (công cụ) và CS 2044 (kịch bản xử lý)
- Hiểu cơ bản về lập trình (nhưng có lẽ cũng không cần thiết)

### Tại sao bạn nên học cái này ?


> If (you’ve never used Unix before and) you think you’re a power
user now, just wait. You don’t know what real power is. - **William E. Shotts, Jr., The Linux Command Line**

> Nếu (bạn chưa dùng Unix bao giờ) và bạn nghĩ là một người dùng hiệu quả, thì hãy suy nghĩ lại. Bạn chưa biết hiệu quả thực sự là gì đâu. **William E. Shotts, Jr., The Linux Command Line**

- Cho phép chúng ta hoàn thành những tác vụ một cách những tác vụ phức tạp đòi hỏi những thao tác thủ công khó khăn.
- Một tập hợp vô hạn những cách kết hợp những chương trình và công cụ để thực hiện những tác vụ phức tạp.
- Phần thưởng : Có được kỹ năng máy tính cực kỳ tốt sau vài năm nữa từ bây giờ.
- Không giới hạn việc tinh chỉnh cài đặt trên máy tính cá nhân. Unix là một bộ công cụ được trang bị đầy đủ chứ không phải một con dao Thụy Sĩ lớn có thể giải quyết mọi vấn đề. (Thuật ngữ Swiss Army Knife để chỉ cái gì đó rất tốt để làm dường như mọi thứ)
- Đơn giản là nó vui & thú vị !

### Câu hỏi phỏng vấn quen thuộc kỹ sư phần mềm

Hãy viết một câu lệnh Unix để lấy ra danh sách những chương trình bạn hay sử dụng nhất.

Câu trả lời :
```shell
history | awk ’{print $2}’ | sort | uniq -c | sort -nr |head
```

Kết quả mẫu :
```
229 screen
146 exit
136 ls
81 vi
64 w
47 math
43 cp
33 cd
25 who
23 history
```
