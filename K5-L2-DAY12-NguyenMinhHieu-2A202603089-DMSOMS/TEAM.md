# TEAM — Ngày 12

Mã bộ ảnh: **G07** · Hình thức: cá nhân

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Nguyen Minh Hieu | 2A202603089 | có | Nguyen Trong Binh - 2A202603099 | 5 |

Ca hai bạn vẫn không thống nhất và đã hỏi coach (ghi tên ảnh + đối tượng):

- Không có

## Cá nhân

### NguyenMinhHieu-2A202603089
- Phần mình làm: Tự gán nhãn đủ 22 ảnh cốt lõi (S01–S08 RGB/IR và D01–D06) trên CVAT, chạy `cabin_check.py` ở các checkpoint và đối chiếu chéo với `peer_export_final.zip`.
- Điều mình học được hôm nay: Phân biệt quy tắc gọi tên ghế theo xe (trái ảnh = `rear_right`), nguyên tắc không suy đoán (`unknown` khi bị che/phản xạ trên IR), và cách dùng keypoint `face13` kèm cờ `occluded`/`outside`.
