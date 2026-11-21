# TEAM — Ngày 12

**Mã bộ ảnh:** G07  
**Hình thức:** Cá nhân

## 1. Thông tin và kết quả review

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Lê Vĩnh Khải | 2A202603322 | Có, 22/22 | Nguyễn Đình Phú | 5/81 |

## 2. Kết quả review chéo (E3)

Đã thực hiện `cabin_check diff` trên 22 ảnh và phát hiện 81 điểm khác biệt giữa hai bản annotation.

Đã xử lý 5 trường hợp tiêu biểu trong `disagreement_log.csv`:

| Khung ảnh | Đối tượng / thuộc tính | Verdict | Quyết định |
|---|---|---|---|
| D01.png | `face.eye_left` | `mine` | Giữ nhãn `open` |
| D02.png | `person` bounding box | `mine` | Giữ bounding box hiện tại |
| D02.png | `hand.on_wheel` | `mine` | Giữ nhãn `yes` |
| D04.png | `hand.side` | `mine` | Giữ nhãn tay trái/phải hiện tại |
| S08_ir.png | `person` bounding box | `mine` | Giữ annotation hiện tại |

Kết quả: Cả 5 trường hợp đã được ghi nhận với `verdict=mine` trong file E3. Không phát sinh thay đổi annotation từ 5 kết luận này.

**Trao đổi với coach:** đã trao đổi với coach và có quyết định giống tôi.
## 3. Cá nhân

### LeVinhKhai-2A202603322

**Phần mình làm:**

- Hoàn thành annotation 22/22 ảnh G07, bao gồm 16 ảnh OMS và 6 ảnh DMS.
- Export dữ liệu theo định dạng CVAT for images 1.1 và chạy các checkpoint A, B, Final.
- Kết quả kiểm tra cuối: 0 ERROR, 0 WARN.
- So sánh với annotation của Nguyễn Đình Phú và xử lý 5/81 dòng khác biệt theo guideline Cabin v1.0.
- Hoàn thiện nhật ký quan sát IR và danh sách lớp DMS/OMS.

**Điều mình học được hôm nay:**

Cần xác định vị trí ghế theo hướng của xe, phân biệt trái/phải theo người trong ảnh và sử dụng `unknown` khi không đủ bằng chứng thị giác. Ngoài ra, kết quả checker đạt 0 lỗi chỉ chứng minh annotation tuân thủ các quy tắc có thể kiểm tra tự động, không đồng nghĩa mọi nhãn đều chính xác. Việc review chéo giúp phát hiện những điểm khác biệt cần đối chiếu với guideline.