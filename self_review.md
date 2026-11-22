# Tự đánh giá — NguyenDucHanh · G12

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S01_rgb | child_seat + person rear_left | ok | `occupied=yes` và có box `person` cùng ghế. Coach: trẻ em vẫn là người | có |
| S03_rgb | infant_seat rear_left và object rear_middle | wrong_class | Bên phải ảnh là nôi em bé, giữa là hộp carton. Đã đổi thành infant_seat và thêm object trong export_final_v2 | có |
| S02_ir | infant_seat rear_right | ok | `facing=rear` trên cả IR-sim và RGB | có |
| D03 | face13 | ok | Đã có 13 điểm. Mắt trái y=455, mắt phải y=384 | có |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Người trên ảnh OMS (kể cả trẻ em đã có box `person`) chưa có box `face`.

Vì sao mình mắc: Tập trung vào ghế và `occupied`, bỏ bước box mặt của OMS.

Lần sau tránh bằng cách: Sau mỗi box `person`, vẽ box `face` nếu thấy mặt. `face13` chỉ vẽ trên ảnh D, và chỉ khi mặt rộng ít nhất 60 px.

## 3. Ghi chú về disagreement_log

Đỗ Thị Kim Oanh đúng ở box `face` người lớn trên S01, S07, S08 (GUIDE 4.1, mặt thấy rõ), ở `infant_seat` và hộp carton trên S03 (GUIDE 4.8), và ở `seatbelt=worn_correct` trên D02, D06 (GUIDE 4.7, dải dây thấy rõ). Mình không lấy `hand` và `face13` trên ảnh S vì GUIDE 4.2 và 4.6 chỉ dùng hai lớp đó cho ảnh D.
