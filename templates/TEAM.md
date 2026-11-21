# TEAM — Ngày 12

Mã bộ ảnh: **G10** · Hình thức: cá nhân

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Nguyễn Quốc Hưng | 2A202604038 | có | Hoàng Quốc Chung 2A202604039 | 40 |

Ca hai bạn vẫn không thống nhất và đã hỏi coach (ghi tên ảnh + đối tượng):

- D04.png (tài xế quay nghiêng đầu): Điểm mốc mặt face13 ở nửa mặt xa bị góc khuất camera che phủ, một bạn chọn cờ occluded=1 (ước lượng toạ độ theo giải phẫu), một bạn chọn cờ outside=1 (không thấy thì không đoán điểm mốc).

## Cá nhân

### NguyenQuocHung-2A202604038
- Phần mình làm: Hoàn thành độc lập 22 ảnh cabin cốt lõi (16 ảnh SVIRO BMW X5 và 6 ảnh Drive&Act NIR); tự kiểm tra qua các checkpoint bằng `cabin_check.py`; thực hiện chạy diff review chéo (40 điểm khác biệt với bạn b22at045) và hoàn thiện các bản sửa lỗi v2.
- Điều mình học được hôm nay: Nắm vững quy ước hệ toạ độ không gian trong khoang cabin (camera nhìn lùi thì trái ảnh là ghế bên phải xe); xử lý đặc thù ảnh tài xế xoay 90° với trục mắt dọc theo trục y; phân biệt rõ hạn chế của ảnh hồng ngoại so với ảnh màu và luôn tuân thủ nguyên tắc không phỏng đoán nhãn.
