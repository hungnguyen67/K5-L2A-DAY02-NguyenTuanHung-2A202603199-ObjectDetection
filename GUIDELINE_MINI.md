# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp     | Định nghĩa của bạn                                  | Ví dụ/điểm phân biệt                                                          |
| ------- | --------------------------------------------------- | ----------------------------------------------------------------------------- |
| `car`   | Xe con, sedan, SUV, taxi và xe bán tải.             | Xe bán tải xếp vào `car`, không xếp vào `truck`.                              |
| `truck` | Xe tải chở hàng và xe đầu kéo.                      | Phân biệt với xe bán tải/cabin nhỏ thuộc `car`.                               |
| `bus`   | Xe buýt và minibus chở khách.                       | Van chở người vẫn thuộc `van`, không tự xếp thành `bus`.                      |
| `van`   | Xe van hoặc minivan dùng để chở hàng hay chở người. | Phân biệt van/minivan với xe buýt lớn (`bus`) và xe con thông thường (`car`). |

## Quy tắc chung

- Box bám sát vật thể nghĩa là: ôm sát phần thân xe nhìn thấy được, không lấy thêm mặt đường, nền hoặc xe bên cạnh.
- Vật thể bị che khuất: vẫn gán một box riêng quanh phần xe nhìn thấy được nếu đủ thông tin để nhận diện lớp; không gộp nhiều xe vào một box.
- Vật thể bị cắt bởi rìa ảnh: vẽ box đến đúng rìa ảnh, chỉ bao phần nằm trong ảnh và không đoán phần ở ngoài khung.
- Vật thể rất nhỏ/mơ hồ: nếu phần nhìn thấy quá nhỏ để xác định chắc lớp thì không tự đoán; ghi ảnh/tình huống và hỏi giảng viên. Không gán người đi bộ, xe đạp, xe máy, biển báo hoặc đèn giao thông.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh         | Tình huống                                                                        | Quyết định cuối                                                                                                  | Lý do theo schema                                                                      |
| ----------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| `drive_052` | Xe buýt nhìn gần chính diện, nằm giữa nhiều xe con và một phần cảnh bị che khuất. | Gán `bus` cho xe buýt; các xe khác nhận box riêng nếu nhận diện được.                                            | Phân lớp theo loại xe và gán từng xe một box; không gộp xe gần nhau.                   |
| `drive_053` | Xe buýt lớn bị cắt ở mép dưới ảnh; nhiều xe nhỏ hơn ở phía trên và hai bên.       | Gán `bus` cho phần xe buýt nhìn thấy, box dừng ở mép ảnh; gán riêng từng xe khác đủ nhận diện.                   | Không ước lượng phần nằm ngoài ảnh; xe bị cắt khung vẫn được gán theo phần nhìn thấy.  |
| `drive_059` | Một số xe ở xa, nhỏ và chen sát nhau nên hình dạng/lớp khó xác định chắc.         | Chỉ gán riêng xe có thể nhận diện đủ chắc; với vật thể không xác định được lớp, không tự đoán và hỏi giảng viên. | Áp dụng quy tắc vật thể nhỏ/mơ hồ; không suy lớp chỉ từ vị trí hoặc dự đoán của model. |
