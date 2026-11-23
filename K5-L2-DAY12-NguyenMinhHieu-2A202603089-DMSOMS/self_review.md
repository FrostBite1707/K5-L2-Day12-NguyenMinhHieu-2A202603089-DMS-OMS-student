# Tự đánh giá — Nguyen Minh Hieu · G07

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S01_rgb.png | `frame_meta` | `wrong_class` | Gắn nhầm `modality = ir` thay vì `rgb` (phát hiện khi diff với peer) | Đã sửa (`export_final_v2.zip`) |
| S04_rgb.png | `infant_seat` | `ok` | Đã đối chiếu hướng `facing` theo hình dạng khung nôi | Đã kiểm tra |
| D01.png | `face13` | `flag` | Đủ 13 điểm, các điểm `right_eye_*` bật cờ `occluded` do phản xạ kính | Đã ghi giải thích trong `check_final_v2.txt` |
| D04.png | `face` | `ok` | `eye_left = closed`, `eye_right = unknown` đúng quy tắc không đoán | Đã kiểm tra |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Nhầm lẫn khi gán thuộc tính `modality` ở `frame_meta` (như `S01_rgb.png` bị ghi `ir`) và chưa nhất quán ở cờ `occluded`/`outside` của `face13`.

Vì sao mình mắc: Thao tác nhanh khi chuyển khung hình giữa `_ir` và `_rgb` nên quên đổi lại `modality`, và chưa kiểm tra kỹ sự đồng bộ giữa cờ `occluded` trên `face13` với trạng thái `eye_right`.

Lần sau tránh bằng cách: Kiểm tra theo đúng thứ tự mục 4.3 (`frame_meta` đầu tiên, kiểm tra tên file `_rgb`/`_ir`) và chạy `cabin_check.py` + `diff` sớm.

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai. Mình học được gì từ dòng đó: Ở `S01_rgb.png`, bạn mình gán đúng `frame_meta.modality = rgb` trong khi mình để nhầm `ir`. Mình học được cần kiểm tra kỹ metadata của từng khung hình theo tên file trước khi chuyển sang vẽ box.
