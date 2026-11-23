# TEAM — Ngày 12

Mã bộ ảnh: **G12** · Hình thức: nhóm

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Nguyễn Đức Hạnh | 2A202603344 | có, export 22 ảnh | Đỗ Thị Kim Oanh (2A202604034) | 93 |
| Đỗ Thị Kim Oanh | 2A202604034 | có, cùng 22 ảnh | Nguyễn Đức Hạnh | 93 |

Ca hai bạn vẫn không thống nhất và đã hỏi coach (ghi tên ảnh + đối tượng):

- Đã xem lại trên ảnh. Oanh đúng ở box `face` S01/S07/S08, `infant_seat` và hộp trên S03, `seatbelt` D02 và D06. Mình đúng ở ghế theo xe, không vẽ `hand`/`face13` trên ảnh S, và `light=unknown` trên ảnh dựng.
- Chưa xác định (4 dòng): miệng và hai môi trên D06 bị chai che. Cả hai cùng sai nên giữ nguyên, cần hỏi coach.
- Đã sửa trên CVAT theo phán quyết, export `export_final_v2.zip`, `cabin_check` ra 0 lỗi.

## Cá nhân

Mỗi người một mục, 1–2 dòng mỗi ý.

### NguyenDucHanh-2A202603344
- Phần mình làm (ngoài 22 ảnh của mình, ví dụ ai review ai, ai tổng hợp ca hỏi coach): Tự gán 22 ảnh. Diff với Đỗ Thị Kim Oanh, điền 93 dòng `disagreement_log.csv`. Sửa 22 dòng bị người review đúng và 4 dòng chưa xác định giữ nguyên, export `export_final_v2.zip`.
- Điều mình học được hôm nay: Ghế OMS gọi theo xe. Trẻ em trong ghế trẻ em vẫn là người: `child_seat` với `occupied=yes` và thêm box `person` cùng ghế. Ảnh D xoay khoảng 90°, mắt trái của tài xế có y lớn hơn mắt phải.

### DoThiKimOanh-2A202604034
- Phần mình làm: Tự gán 22 ảnh. Diff với Nguyễn Đức Hạnh, điền 93 dòng `disagreement_log.csv`.
- Điều mình học được hôm nay: OMS cần box `face` cho người lớn, nhưng `hand` và `face13` chỉ dùng cho ảnh D. Ảnh SVIRO là ảnh dựng nên `light=unknown`.
