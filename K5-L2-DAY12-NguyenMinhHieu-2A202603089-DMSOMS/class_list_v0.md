# Danh sách lớp v0 — Nguyen Minh Hieu · G07

## DMS (7 lớp / thuộc tính)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person.seatbelt` | `worn_correct` / `worn_incorrect` / `not_worn` / `unknown` | Cảnh báo tài xế chưa thắt dây an toàn hoặc thắt sai quy cách (dưới nách, sau lưng) | Có, trừ khi áo tối màu/bị che khuất (khi đó ghi `unknown`) |
| 2 | `face.eye_left` / `face.eye_right` | `open` / `closed` / `unknown` | Phát hiện buồn ngủ, nhắm mắt kéo dài để cảnh báo kịp thời | Có, trừ khi bị đốm phản xạ LED trên kính hoặc kính râm tối |
| 3 | `face.glasses` | `none` / `clear` / `sun` / `unknown` | Giúp model xử lý chính xác vùng mắt (kính râm/phản xạ dễ che mắt) | Có thể thấy gọng/tròng, nhưng trên NIR kính râm có thể trông trong suốt |
| 4 | `face.gaze_zone` | `road` / `mirror_l` / `mirror_r` / `mirror_c` / `cluster` / `center` / `lap` / `other` | Phát hiện mất tập trung (nhìn lệch khỏi đường quá lâu) | Có (theo hướng đầu và tròng mắt) |
| 5 | `face13` (13 điểm mặt) | 13 keypoint kèm cờ `occluded` / `outside` | Ước lượng tư thế đầu (head pose: yaw/pitch/roll) và độ mở mắt | Có, nếu mặt đủ lớn (>= 60 px) và không bị che |
| 6 | `hand.on_wheel` | `yes` / `no` / `unknown` | Kiểm tra tài xế có giữ tay trên vô lăng hay đang buông tay/làm việc riêng | Có (dựa theo hình dạng bàn tay và vị trí vô lăng) |
| 7 | `phone` | `held` / `mounted` / `lap` | Phát hiện hành vi cầm/sử dụng điện thoại gây mất tập trung khi lái xe | Có (nhận diện qua hình dạng cạnh, góc, màn hình điện thoại) |

## OMS (6 lớp / thuộc tính)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person` (`seat`, `seatbelt`) | `front_passenger` / `rear_left` / `rear_middle` / `rear_right`; `not_worn` / `unknown` | Xác định số lượng, vị trí hành khách ngồi trên xe để điều chỉnh túi khí và nhắc thắt dây an toàn | Có (dựa vào hình dạng cơ thể, đầu người) |
| 2 | `face` (OMS) | Bounding box mặt hành khách | Định vị vùng đầu hành khách, hỗ trợ phân biệt người thật với đồ vật/ghế trống | Có |
| 3 | `child_seat` | `seat`; `occupied`: `no` / `unknown` | Nhận diện ghế trẻ em đang lắp trên xe để nhắc kiểm tra/cảnh báo bỏ quên trẻ | Có (nhận diện qua hình dạng khung ghế trẻ em) |
| 4 | `infant_seat` | `seat`; `facing`: `rear` / `front` | Nhận diện nôi em bé và hướng lắp (quay sau/trước) để cảnh báo tắt túi khí nếu lắp sai/ngược | Có (nhận diện qua hình dạng nôi xách) |
| 5 | `object` | `seat`; `type`: `bag` / `box` / `cup` / `other` | Phân biệt đồ vật đặt trên ghế với người/trẻ em, tránh báo nhầm thắt dây an toàn hoặc bỏ quên trẻ | Có (theo hình dạng, nhưng dễ nhầm nếu vật tối màu/lẫn nền) |
| 6 | `frame_meta` | `modality` (`rgb`/`ir`), `light` (`day`/`night`/`unknown`), `camera_blocked` (`yes`/`no`) | Cảnh báo camera bị che khuất và phân luồng xử lý theo loại ảnh RGB/IR | Có (đánh giá mức độ che khuất trực tiếp trên khung hình) |

## 2 câu hỏi leo thang

1. Câu hỏi: Khi một mắt của tài xế bị phản xạ ánh sáng nhẹ trên tròng kính nhưng vẫn hơi thấy bóng mí mắt, ngưỡng nào thì bắt buộc ghi `unknown` thay vì `closed`/`open`?
   Khung ví dụ: `D04.png`
   Bạn tạm gán thế nào và vì sao: Tạm gán `unknown` cho `eye_right` theo quy tắc 4.4-1 ("không thấy rõ thì `unknown`", không suy đoán từ mắt còn lại).
2. Câu hỏi: Với nôi em bé (`infant_seat`) nhìn từ góc chéo trên ảnh IR mô phỏng, tiêu chí hình học cụ thể nào để phân biệt `facing = rear` và `facing = front` khi tay xách/mái che bị khuất một phần?
   Khung ví dụ: `S04_ir.png`
   Bạn tạm gán thế nào và vì sao: Tạm gán `rear` dựa theo hướng tựa lưng/mái che quan sát được, nhưng cần đối chiếu thêm với guideline chi tiết.
