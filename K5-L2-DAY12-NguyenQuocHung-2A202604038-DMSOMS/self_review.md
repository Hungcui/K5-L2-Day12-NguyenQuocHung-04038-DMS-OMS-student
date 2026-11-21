# Tự đánh giá — Nguyễn Quốc Hưng · G10

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S01_rgb | person | ok | Ghế bên trái ảnh đã gán đúng rear_right theo xe, seatbelt để not_worn | Đã kiểm tra |
| S04_ir | object | guess | Ban đầu đoán type=box theo thói quen, sau nhìn kỹ lại phom dáng bo tròn sửa thành bag | Đã sửa |
| D01 | face | lr_flip | Ảnh xoay 90°, lúc đầu nhầm mắt trái/phải theo trục x, đã sửa lại mắt trái có y lớn hơn | Đã sửa |
| D03 | face13 | flag | Điểm khóe mắt bị bóng tối che khuất nhẹ ban đầu quên bật occluded, đã bổ sung cờ occluded=1 | Đã sửa |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Nhầm lẫn quy ước trái/phải trên ảnh tài xế `D##` do ảnh bị xoay 90 độ so với camera chuẩn.

Vì sao mình mắc: Do thói quen nhìn mắt trái/phải theo màn hình (trục x) như ảnh chụp chân dung thông thường, trong khi ảnh bị xoay 90° nên trục nối hai mắt của tài xế chạy dọc theo trục y (mắt trái có y lớn hơn mắt phải).

Lần sau tránh bằng cách: Luôn tự hình dung tư thế ngồi của người lái xe hoặc xoay nhẹ góc nhìn theo hướng đầu tài xế trước khi chấm điểm `face13` và thuộc tính `eye_left`/`eye_right`; kiểm tra bằng quy tắc: toạ độ y của mắt trái luôn lớn hơn mắt phải.

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai. Mình học được gì từ dòng đó:
- Tại khung hình có kính râm, bạn mình chọn `glasses = sun` kèm `eye_left = unknown` vì tròng kính bị lóa hồng ngoại không nhìn rõ mí mắt, trong khi mình chọn `clear` do thấy hơi mờ mờ viền mắt bên trong. Mình học được bài học đắt giá về quy tắc "không thấy thì unknown, không phỏng đoán": khi phổ hồng ngoại làm tròng kính trong suốt giả tạo nhưng bị lóa đèn LED che mất khe mắt thật, việc ghi `unknown` là bắt buộc để tránh dạy sai dữ liệu cho model.
