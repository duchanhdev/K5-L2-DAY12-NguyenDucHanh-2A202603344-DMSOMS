# Danh sách lớp v0 — NguyenDucHanh · G12

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | eye_state | open / closed / unknown | Biết mắt đang mở hay mí đã khép trên khung này, để theo dõi buồn ngủ. `closed` chỉ khi thấy mí khép, không suy từ khung bên cạnh | Có, trừ khi đốm phản xạ, kính râm hoặc tay che vùng mắt |
| 2 | gaze_zone | road / mirror_* / cluster / center / lap / other | Biết tài xế đang nhìn đường, gương, đồng hồ, màn hình giữa hay xuống đùi, để phát hiện mất tập trung | Một phần. NIR thấy hướng đầu và mắt, không thấy màu đèn báo trên đồng hồ |
| 3 | glasses | none / clear / sun / unknown | Biết vùng mắt có bị kính che không, để model không học nhầm người đang đeo kính thành không đeo kính | Có hình dáng gọng. Trên NIR kính râm có thể trông trong suốt, không chắc thì `unknown` |
| 4 | phone | held / mounted / lap | Biết điện thoại đang ở tay, trên giá hay trên đùi, để cảnh báo dùng điện thoại khi lái | Có nếu thấy cạnh, góc hoặc màn hình. Vật tối áp tai mà không thấy hình điện thoại thì không vẽ |
| 5 | hand.on_wheel | yes / no / unknown | Biết tay có đang chạm vô lăng không. Trên xe tự lái thử nghiệm, `no` là trạng thái bình thường nếu tay không chạm vô lăng | Có theo vị trí tay và vành vô lăng, không cần màu da |
| 6 | face13 | 13 điểm mép mắt, mũi, miệng, cờ occluded / outside | Ước lượng tư thế đầu và độ mở mắt. Điểm bị che phải có cờ, không đặt điểm cho đủ | Có khi mặt rộng ít nhất 60 px. Mặt nhỏ hơn thì chỉ giữ box `face` |
| 7 | person.seatbelt | worn_correct / worn_incorrect / not_worn / unknown | Biết dây có đi đúng từ vai xuống hông đối diện hay không, để nhắc thắt dây | Dải dây thấy được bằng độ sáng. Tối hoặc bị che thì `unknown`, không đoán |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | person.seat | driver / front_passenger / rear_left / rear_middle / rear_right | Biết ghế nào có người, để đếm người và nhắc thắt dây đúng ghế. Ghế gọi theo xe, không theo bên trái ảnh | Có theo hình người. Ảnh IR-sim của SVIRO không có màu áo |
| 2 | person.seatbelt | not_worn / unknown (trên SVIRO không có worn_*) | Nhắc người chưa thắt dây. Bộ SVIRO không có ai thắt dây, nên không dùng bộ này để dạy `worn_correct` | Dây có thể chìm trên áo tối. Không thấy thì `unknown` trên từng ảnh, không copy từ ảnh RGB cùng cảnh |
| 3 | child_seat | seat + occupied = no / unknown / yes | Biết ghế trẻ em trống, không thấy rõ lòng ghế, hoặc có trẻ đang ngồi, để nhắc quên trẻ và xử lý túi khí. `yes` khi có hình trẻ em, và thêm box `person` cùng ghế vì trẻ em vẫn là người. `no` khi ghế trống, `unknown` khi không thấy lòng ghế | Có hình ghế. Trên IR-sim không có màu, phân biệt trẻ em với đồ vật bằng hình dạng |
| 4 | infant_seat | seat + facing = rear / front | Biết nôi em bé quay đầu ra sau hay ra trước, để xử lý túi khí ghế đó | Có hình nôi. Hướng nhìn dễ lệch trên IR-sim vì không có màu; gán theo từng ảnh |
| 5 | object | seat + type = bag / box / cup / other | Biết đồ để trên ghế nào, để nhắc đồ quên và không đếm đồ thành người | Có hình dạng. Mất màu nên túi, hộp, cốc không chắc thì `other` |
| 6 | frame_meta | modality, light, camera_blocked | Biết khung đang là RGB hay IR và camera có bị che không, để model không dùng thuộc tính chỉ có ở ảnh màu | `modality` gán theo tên file. Ảnh dựng SVIRO thì `light=unknown` |

## 2 câu hỏi leo thang

1. Câu hỏi: Trẻ em trong ghế trẻ em có cần box `face` như người lớn không?
   Khung ví dụ: G12 S01, S03, S07. Các ghế `occupied=yes` đã có `child_seat` và `person`, chưa có box `face`.
   Bạn tạm gán thế nào và vì sao: Coach xác nhận trẻ em vẫn là người nên giữ box `person`. Box `face` cho các ghế này chưa vẽ. Tạm chưa thêm cho đến khi hỏi rõ, vì guideline gốc chỉ yêu cầu box `face` cho người lớn.
2. Câu hỏi: Khi RGB và IR-sim cùng cảnh cho hai giá trị khác nhau của cùng một thuộc tính, lấy ảnh nào?
   Khung ví dụ: G12 S02, `infant_seat` ghế `rear_right`: RGB ghi `facing=rear`, IR-sim ghi `facing=front`.
   Bạn tạm gán thế nào và vì sao: Giữ mỗi ảnh một giá trị theo đúng ảnh đó, không copy từ ảnh kia. IR-sim không phải NIR thật và không có màu, nên không lấy hướng ghế của RGB để điền cho IR.
