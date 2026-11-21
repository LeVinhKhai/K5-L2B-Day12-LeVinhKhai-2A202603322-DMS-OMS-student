# Khai báo dùng AI — Lê Vĩnh Khải
# Khai báo sử dụng AI — Lê Vĩnh Khải · G07

Tôi trực tiếp gán nhãn và kiểm tra 22 ảnh trên CVAT local. ChatGPT và Codex được sử dụng để hỗ trợ thao tác kỹ thuật, tham khảo guideline và trình bày báo cáo. Các nhãn trong bản nộp cuối do tôi quyết định; không sử dụng kết quả AI pre-label làm annotation cuối.

| # | Công cụ | Nội dung hỗ trợ | Cách sử dụng và kiểm tra |
|---|---|---|---|
| 1 | ChatGPT / Codex | Hướng dẫn quy trình CVAT, export, gộp XML và sử dụng `cabin_check.py`. | Tôi tự thực hiện và kiểm tra kết quả: 22 ảnh, 22 `frame_meta`, 0 lỗi, 0 cảnh báo. |
| 2 | ChatGPT / Codex | Hỗ trợ đọc kết quả peer diff, giải thích guideline và định dạng các file E3–E5. | Tôi tự review, lựa chọn nhãn và đối chiếu lại với guideline. Năm trường hợp E3 được ghi `verdict=mine`. |
| 3 | ChatGPT | Gợi ý diễn đạt nhật ký IR, cấu trúc báo cáo tự đánh giá và giải thích câu hỏi. | Tôi kiểm tra lại nội dung, chỉnh sửa và lựa chọn kết quả trước khi nộp. |

**Kết luận:** AI đóng vai trò công cụ hỗ trợ học tập và xử lý tài liệu. Việc gán nhãn, review và quyết định annotation cuối cùng được thực hiện bởi người học.
