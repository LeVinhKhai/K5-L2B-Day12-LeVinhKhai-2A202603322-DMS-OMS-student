# Danh sách lớp v0 — Lê Vĩnh Khải · G07

Danh sách dùng đúng schema Cabin v1.0. Trong bộ G07, DMS dùng ảnh NIR thật (`real_IR`, D01–D06), còn OMS dùng ảnh RGB và IR mô phỏng (`IR_sim`, S01–S08). Không suy đoán màu sắc trên ảnh IR.

## DMS (Drive&Act, `real_IR`)

| # | Lớp / thuộc tính | Giá trị hợp lệ | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person.seat` | `driver` | Xác định vùng tài xế để liên kết trạng thái người lái với các đối tượng DMS khác. | Có trên `real_IR` nhờ vị trí và hình dạng; D01–D06 chỉ gán tài xế. |
| 2 | `person.seatbelt` | `worn_correct`, `worn_incorrect`, `not_worn`, `unknown` | Theo dõi việc sử dụng dây an toàn và phân biệt đeo đúng, đeo sai hoặc không đeo. | Có thể nhận ra dải dây trên `real_IR`; dùng `unknown` khi tối hoặc bị che. |
| 3 | `face.eye_left` | `open`, `closed`, `unknown` | Theo dõi trạng thái riêng của mắt trái để hỗ trợ phát hiện nhắm mắt kéo dài. | Có thể thấy khe mắt trên `real_IR`; phản xạ, kính hoặc che khuất thì `unknown`. |
| 4 | `face.eye_right` | `open`, `closed`, `unknown` | Theo dõi trạng thái riêng của mắt phải, không suy từ mắt trái. | Có thể thấy khe mắt trên `real_IR`; chỉ chọn `closed` khi thấy rõ hai mí khép. |
| 5 | `face.glasses` | `none`, `clear`, `sun`, `unknown` | Mô tả kính để đánh giá độ tin cậy của mắt và landmark. | Có thể nhận qua hình dạng trên `real_IR`, nhưng kính râm có thể trông trong suốt; không chắc thì `unknown`. |
| 6 | `face.gaze_zone` | `road`, `mirror_l`, `mirror_r`, `mirror_c`, `cluster`, `center`, `lap`, `other` | Phân loại vùng tài xế đang nhìn để phát hiện mất tập trung khỏi đường. | Có thể ước lượng từ hướng đầu và mắt trên `real_IR`; trường hợp không chắc dùng `other`. |
| 7 | `face13` và cờ điểm | `left_eye_outer`, `left_eye_inner`, `left_eye_upper`, `left_eye_lower`, `right_eye_outer`, `right_eye_inner`, `right_eye_upper`, `right_eye_lower`, `nose_tip`, `mouth_left`, `mouth_right`, `lip_upper`, `lip_lower`; cờ `occluded`, `outside` | Chuẩn hóa hình học khuôn mặt để ước lượng tư thế đầu, mắt và miệng. | Có trên `real_IR` khi mặt rộng ít nhất 60 px; điểm bị che dùng `occluded`, không đoán được dùng `outside`. |
| 8 | `hand.whose`, `hand.side`, `hand.on_wheel` | `whose`: `driver`, `passenger`; `side`: `left`, `right`; `on_wheel`: `yes`, `no`, `unknown` | Phân biệt tay của ai, tay trái/phải theo người và việc tay tài xế có chạm vô lăng. | Có thể nhận qua đường viền trên `real_IR`; tiếp xúc không rõ thì `on_wheel=unknown`. |
| 9 | `phone.state` | `held`, `mounted`, `lap` | Nhận diện điện thoại và bối cảnh sử dụng để hỗ trợ phát hiện xao nhãng. | Có thể nhận qua cạnh, góc hoặc màn hình trên `real_IR`; không thấy phần hình dạng điện thoại thì không vẽ box. |

## OMS (SVIRO RGB và `IR_sim`)

| # | Lớp / thuộc tính | Giá trị hợp lệ | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person.seat` | `rear_left`, `rear_middle`, `rear_right` | Xác định ghế nào đang có người để hỗ trợ giám sát chiếm chỗ và an toàn hàng ghế sau. | Có trên `IR_sim` theo hình dạng và vị trí; ghế gọi theo xe, nên trái ảnh là `rear_right`. |
| 2 | `person.seatbelt` | `not_worn`, `unknown` trong SVIRO | Theo dõi việc người ngồi có đeo dây an toàn hay không. | Có thể khó thấy trên `IR_sim`; SVIRO không có người thắt dây nên chỉ dùng `not_worn` khi thấy rõ, nếu không dùng `unknown`. |
| 3 | `child_seat.seat` | `rear_left`, `rear_middle`, `rear_right` | Xác định vị trí ghế trẻ em để quản lý bố trí ghế và nhắc kiểm tra khoang sau. | Có trên `IR_sim` chủ yếu nhờ hình dạng và vị trí, không dựa vào màu. |
| 4 | `child_seat.occupied` | `no`, `unknown` | Phân biệt ghế trẻ em thấy rõ là trống với trường hợp không nhìn rõ bên trong. | Có thể xác định trên `IR_sim` khi lòng ghế rõ; bị phủ hoặc tối thì `unknown`; schema không có `yes`. |
| 5 | `infant_seat.seat`, `infant_seat.facing` | `seat`: `rear_left`, `rear_middle`, `rear_right`; `facing`: `rear`, `front` | Xác định vị trí và hướng ghế em bé để hỗ trợ kiểm tra lắp đặt an toàn. | Có thể nhận trên `IR_sim` bằng hình học ghế; không suy từ màu. |
| 6 | `object.seat`, `object.type` | `seat`: `rear_left`, `rear_middle`, `rear_right`; `type`: `bag`, `box`, `cup`, `other` | Xác định đồ vật ở từng ghế, hỗ trợ phát hiện vật bỏ quên và phân biệt với người hoặc ghế trẻ em. | Có thể nhận trên `IR_sim` bằng hình dạng; loại không chắc dùng `other`. |
| 7 | `face` | `rectangle` (OMS chỉ yêu cầu box face; không đánh giá chi tiết trạng thái mắt, kính và vùng nhìn như DMS.) | Liên kết vùng mặt với người lớn trong khoang hành khách. | Có thể vẽ trên `IR_sim` nếu mặt còn nhìn thấy; không thấy cả mắt lẫn mũi thì không vẽ. |
| 8 | `frame_meta.modality`, `frame_meta.light`, `frame_meta.camera_blocked` | `modality`: `rgb`, `ir`; `light`: `day`, `night`, `unknown`; `camera_blocked`: `yes`, `no` | Ghi ngữ cảnh cảm biến của mỗi khung để tách RGB và IR khi huấn luyện hoặc đánh giá OMS. | Có. Với SVIRO `_ir`, dùng `modality=ir` nhưng phải hiểu là `IR_sim`; ảnh dựng có `light=unknown`. |

## 2 câu hỏi leo thang

1. **Câu hỏi:** Ở `S08_ir`, nếu hình người trông giống trẻ em nhưng GUIDE §3 khẳng định SVIRO không có trẻ em và schema không có lớp người-trẻ-em, cần giữ `person` hay ghi chú theo cách nào để không làm sai nghĩa dữ liệu?
   **Khung ví dụ:** `S08_ir` —  E3 chỉ cho biết box `person` có ở bản mine mà không match peer, không chứng minh tuổi hay lớp thực tế.
   **Tạm gán:** Không thay đổi annotation chỉ dựa trên kết quả XML diff. Kiểm tra lại S08_ir trên CVAT. Nếu đối tượng có hình dạng giống trẻ em, ghi nhận mã khung và báo coach để được hướng dẫn trước khi quyết định gán nhãn. Không tự chuyển thành person hoặc child_seat khi chưa được xác nhận. Nếu xác định rõ là người lớn, gán person với seat theo hướng xe.

2. **Câu hỏi:** Ở `D04`, khi thấy đủ bàn tay để vẽ box nhưng tư thế hoặc che khuất làm không xác định chắc `hand.side`, guideline yêu cầu xử lý thế nào khi schema chỉ có `left`/`right` và không có `unknown`?
   **Khung ví dụ:** `D04` —  E3 ghi hai bản đảo `left`/`right`.
   **Tạm gán:** Giữ hai giá trị hiện có trong bản final và không sửa chỉ từ XML diff; mở ảnh để truy theo tay của chính tài xế và kiểm tra hai box không trùng `side`. Nếu vẫn không xác định được, hỏi coach trước khi thay đổi vì GUIDE chưa nêu cách biểu diễn `side=unknown`.
