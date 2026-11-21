# Danh sách lớp v0 — Nguyễn Quốc Hưng · G10

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | eye_state (eye_left, eye_right) | open / closed / unknown | Phát hiện tài xế buồn ngủ, ngủ gật (drowsiness detection) hoặc vi ngủ (microsleep) qua chỉ số PERCLOS để phát chuông cảnh báo. | Có, đồng tử và viền mắt phản xạ rõ dưới ánh sáng hồng ngoại gần 940nm; trừ khi bị lóa phản xạ LED trên kính hoặc kính râm tối. |
| 2 | gaze_zone | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Phát hiện mất tập trung (distraction detection) khi tài xế rời mắt khỏi đường lái (road) quá 2-3 giây (ví dụ nhìn xuống đùi, màn hình trung tâm). | Có, kết hợp hướng đầu (head pose 3D) và vị trí con ngươi; mắt nhìn lệch vẫn nhận dạng tốt trên IR. |
| 3 | glasses | none / clear / sun / unknown | Báo cho hệ thống biết tài xế có đeo kính hay không để tự động điều chỉnh thuật toán ước lượng mắt/hướng nhìn phù hợp. | Có, phân biệt gọng kính và bề mặt phản xạ; kính cận nhìn xuyên qua được, kính râm có thể trong suốt một phần trên phổ IR. |
| 4 | hand_on_wheel | yes / no / unknown | Nhận biết trạng thái Hands-on / Hands-off khi xe kích hoạt lái tự động Level 2/2+ để nhắc tài xế giữ tay trên vô lăng (Takeover Request). | Có, thấy rõ bàn tay và điểm tiếp xúc với vành vô lăng kể cả trong khoang lái tối hoàn toàn. |
| 5 | phone_state | held / mounted / lap | Phát hiện hành vi sử dụng điện thoại khi đang điều khiển phương tiện (nhắn tin, gọi điện cầm tay) gây nguy hiểm nghiêm trọng. | Có, phát hiện thân máy dạng chữ nhật phẳng hoặc độ phản xạ/phát sáng của màn hình điện thoại. |
| 6 | face13 | 13 mốc giải phẫu (mắt, mũi, miệng) kèm cờ occluded/outside | Cung cấp toạ độ chuẩn xác để tính góc nghiêng/quay đầu (Pitch, Yaw, Roll), đo tỷ lệ mở mắt EAR và mở miệng MAR (phát hiện ngáp). | Có, các mốc tương phản tốt với đèn NIR; điểm bị che khuất bởi vật thể hoặc tóc được đánh dấu occluded. |
| 7 | seatbelt (driver) | worn_correct / worn_incorrect / not_worn / unknown | Kiểm tra thắt dây an toàn tài xế, nhắc nhở trước khi khởi hành và điều chỉnh thuật toán kích nổ túi khí khi xảy ra va chạm. | Thấy được dải dây chéo vắt qua ngực/vai; nếu áo đen tiệp màu dây thì cần tăng độ tương phản để quan sát. |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | person_seat (vị trí người) | rear_left / rear_middle / rear_right / front_passenger | Xác định vị trí có hành khách ngồi để bật nhắc nhở thắt dây an toàn cho đúng ghế và điều hướng cửa gió điều hòa (Smart HVAC). | Có, thân hình người phản xạ ánh sáng hồng ngoại rõ rệt cả ngày lẫn ban đêm. |
| 2 | child_seat | child_seat (occupied: no / unknown) | Xác định có ghế trẻ em cố định trên xe; tối ưu hóa cảnh báo va chạm và an toàn cho ghế sau. | Có, cấu trúc khung cứng và đai cố định của ghế trẻ em hiển thị rõ hình khối trên ảnh IR. |
| 3 | infant_seat | infant_seat (facing: rear / front) | Tính năng cực kỳ quan trọng chống bỏ quên trẻ em trong xe (Child Presence Detection - Euro NCAP); vô hiệu hóa túi khí ghế trước nếu nôi quay lưng (rear-facing). | Có, nhận biết rõ hình dáng lòng nôi, quai xách và chiều quay của nôi em bé. |
| 4 | object | type: bag / box / cup / other | Phân biệt đồ vật đặt trên ghế với người ngồi thật để tránh báo động giả thắt dây an toàn; nhắc nhở quên hành lý khi rời xe. | Có, nhìn rõ đường bao hình học và góc cạnh của đồ vật, nhưng khó phân biệt chất liệu/màu sắc so với RGB. |
| 5 | frame_meta (camera_blocked) | yes / no | Giám sát trạng thái hoạt động của camera cabin (health monitoring); phát hiện ống kính bị hành khách che áo, mũ hoặc bị bám bẩn. | Có, khung hình sẽ bị mờ đục hoặc tối đen hoàn toàn nếu ống kính bị che chắn. |
| 6 | seatbelt (rear seats) | worn_correct / worn_incorrect / not_worn / unknown | Giám sát hành khách phía sau có tuân thủ an toàn hay không, cảnh báo tài xế nếu trẻ em hoặc hành khách bất ngờ tháo dây an toàn khi xe đang chạy. | Có thể nhìn thấy dải dây chéo; trên ảnh IR-sim nếu áo tiệp màu thì tương phản kém hơn ảnh màu RGB. |

## 2 câu hỏi leo thang

Câu hỏi bạn muốn hỏi người viết guideline (hoặc khách hàng) vì guideline v1.0 chưa trả lời. Mỗi câu kèm **tên khung** làm ví dụ.

1. **Câu hỏi:** Khi một đồ vật lớn (như balo hoặc thùng đồ) đặt chiếm trọn cả diện tích của một ghế ngồi nhưng không có dây đai chằng giữ, hệ thống có yêu cầu phân định chi tiết loại đồ vật (`bag` hay `box`) hay chỉ cần gắn nhãn chung là `object` để kích hoạt chức năng cảnh báo vật thể nặng trên ghế?
   - **Khung ví dụ:** `S04_rgb` / `S04_ir` (bộ G10, có túi/hộp đặt tại ghế giữa `rear_middle`).
   - **Bạn tạm gán thế nào và vì sao:** Tạm thời vẽ box `object` ôm sát đồ vật, gán thuộc tính `seat = rear_middle` và `type = bag` theo hình dạng quan sát được, vì theo Guideline Cabin v1.0 mọi đồ vật mang theo đặt trên ghế đều phải được vẽ box và định danh loại hình học để phục vụ phát hiện vật cản.

2. **Câu hỏi:** Trên ảnh hồng ngoại DMS, khi tài xế quay đầu góc quá lớn (> 60°) khiến nửa mặt xa hoàn toàn bị khuất sau sống mũi (không thể nhìn thấy mắt và khóe miệng xa), guideline nên quy định đánh dấu điểm mốc mặt `face13` là `outside` (bỏ qua toạ độ) hay bắt buộc nội suy cấu trúc giải phẫu và đánh dấu `occluded`?
   - **Khung ví dụ:** `D04.png` (bộ G10, tài xế quay nghiêng đầu thao tác).
   - **Bạn tạm gán thế nào và vì sao:** Tạm thời đánh dấu các điểm mốc bị khuất hoàn toàn là `outside = 1` và không ước lượng toạ độ phỏng đoán; chỉ những điểm mốc nào bị tóc hoặc gọng kính che một phần nhưng vẫn xác định chắc chắn được vị trí thì mới đặt điểm và bật cờ `occluded = 1`, tuân thủ đúng nguyên tắc số 1 của guideline: "Không thấy thì unknown / không đoán".
