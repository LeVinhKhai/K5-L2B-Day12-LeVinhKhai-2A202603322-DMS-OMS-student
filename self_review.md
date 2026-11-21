# Tự đánh giá — Lê Vĩnh Khải · G07

## 1. Tự rà soát 4 cảnh

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| `S01_ir` | `frame_meta` | `missing` | Bản export ban đầu thiếu tag `frame_meta`. Đã bổ sung và kiểm tra lại bằng `cabin_check`. | Có. Bản final có đủ 22/22 tag. |
| `S08_ir` | `person` | `ok` | Peer diff ghi box chỉ có ở bản mine hoặc IoU thấp. Đã xử lý trong E3 với `verdict=mine`. | Giữ annotation hiện tại. |
| `D01` | `face.eye_left` | `ok` | Mine gán `open`, peer gán `unknown`. Kết luận E3 là `mine`, giữ `eye_left=open`. | Giữ nhãn hiện tại. |
| `D04` | `hand.side` | `ok` | Hai bản gán khác nhau về tay trái/phải. Kết luận E3 là `mine`, giữ nguyên các giá trị đã gán theo người lái. | Giữ nhãn hiện tại. |

## 2. Lỗi đáng chú ý nhất hôm nay

**Lỗi:** Bỏ sót tag `frame_meta` ở ảnh `S01_ir` trong bản export ban đầu.

**Vì sao mình mắc:** Chưa kiểm tra đầy đủ metadata của từng ảnh trước khi export và chạy kiểm tra cuối.

**Lần sau tránh bằng cách:** Tạo `frame_meta` trước khi vẽ box, kiểm tra tag ở từng ảnh và chạy `cabin_check` sau mỗi checkpoint để phát hiện lỗi sớm.

**Kết quả khắc phục:** Bản `export_final.zip` cuối cùng gồm 22 ảnh, có đầy đủ 22 tag `frame_meta`, đạt 0 ERROR và 0 WARN.

## 3. Ghi chú về disagreement_log

Sau khi so sánh với bản annotation của Nguyễn Đình Phú, công cụ phát hiện 81 điểm khác biệt. Tôi đã chọn xử lý 5 trường hợp và ghi kết luận `verdict=mine` trong `disagreement_log.csv`.

Trong 5 trường hợp đã xử lý, chưa có trường hợp nào được kết luận `verdict=peer` hoặc `both_wrong`. Vì vậy, chưa có đủ căn cứ để nêu một ví dụ cụ thể mà peer đúng và mình sai.

**Điều học được:** Kết quả diff cho biết hai bản annotation khác nhau, không tự chứng minh bên nào đúng. Việc phân xử phải dựa trên quan sát trực tiếp, guideline và trao đổi với coach nếu còn mơ hồ. Đặc biệt, các trường hợp khác biệt về mắt, tay và bounding box cần kiểm tra kỹ thay vì chỉ dựa vào kết quả checker.