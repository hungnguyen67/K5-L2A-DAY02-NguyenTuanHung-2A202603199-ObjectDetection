# Báo cáo cá nhân — Ngày 2 Object Detection

Đổi tên file theo `MSSV_HoTen.md`, ví dụ `20241234_NguyenVanAn.md`. Điền kết quả thật, xóa dòng hướng dẫn khi nộp. Xem [quy định nộp](../../SUBMISSION.md).

## 1. Thông tin học viên

- Họ tên: Nguyễn Tuấn Hung
- MSSV: 2A202603199
- Email: hungnn91296@gmail.com
- Lớp: L2A
- Link repo bài làm: https://github.com/hungnguyen67/K5-L2A-DAY02-NguyenTuanHung-2A202603199-ObjectDetection.git
- Link Colab đã chạy: https://drive.google.com/file/d/1FsmLIQKM8Jz6ZzC5pN9UV_Ev9_2KPHLC/view?usp=sharing

## 2. Schema và mini guideline

Dẫn tới [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md). Tóm tắt ba ca mơ hồ đã quyết định, cách áp dụng schema và phần cần giảng viên làm rõ.

- Schema: `car=0`, `truck=1`, `bus=2`, `van=3`. Quy tắc box: mỗi xe một box quanh phần nhìn thấy; xe bị che/cắt khung vẫn gán nếu đủ căn cứ nhận diện.
- `GUIDELINE_MINI.md` ghi ba tình huống từ ảnh train `drive_002`, `drive_041`, `drive_024`, lần lượt minh họa xe bị che khuất, xe buýt bị cắt khung và xe nhỏ/chen sát khó xác định lớp; không dùng ảnh eval làm ca train.
- Cần hỏi giảng viên: cách xử lý các trường hợp không đủ thông tin để phân biệt chắc `car`/`van`/`bus` theo schema.

## 3. Annotation và self-QC

- Số file nhãn train: 50 file `.txt` trong `dataset/labels/train/`.
- Kết quả checker và lỗi đã xử lý: `python tools/check_yolo_labels.py` đạt `50/50`; checker không báo lỗi cấu trúc. Chưa có nhật ký lỗi nội dung/việc sửa.
- Danh sách ít nhất 10 ảnh đã rà bằng mắt: Chưa có danh sách xác nhận 10 ảnh train được rà. Các ảnh eval `drive_051.jpg`–`drive_060.jpg` có prediction trong artifacts, nhưng không tính là bằng chứng self-QC 10 ảnh train.
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa: Chưa có ghi chép xác thực.
- Commit khóa nhãn ban đầu: `f748cf01f42f3a13e7c96c1ed490e029a0747dac` (`Add training dataset labels`).

## 4. Gold QC và rework

| Chỉ số              | Trước sửa |               Sau sửa nếu có |
| ------------------- | --------: | ---------------------------: |
| TP                  |       309 | Chưa có kết quả đánh giá lại |
| FP                  |       227 | Chưa có kết quả đánh giá lại |
| FN                  |       344 | Chưa có kết quả đánh giá lại |
| Precision           |    0.5765 | Chưa có kết quả đánh giá lại |
| Recall              |    0.4732 | Chưa có kết quả đánh giá lại |
| F1                  |    0.5198 | Chưa có kết quả đánh giá lại |
| mean_iou_of_matches |    0.8718 | Chưa có kết quả đánh giá lại |
| passed              |     false | Chưa có kết quả đánh giá lại |

Dẫn tới `outputs/annotation_evaluation.json` trong repo. Nếu rework, ghi ảnh, lỗi đã kiểm, quyết định sửa/giữ và lý do. Không suy nguyên nhân chỉ từ FP/FN. Không có rework thì ghi rõ.

Lần đánh giá đang lưu trong JSON có `F1=0.5198` (chưa đạt ngưỡng `0.80`) và `mean_iou_of_matches=0.8718` (đạt ngưỡng `0.70`). Chưa có dữ liệu chứng minh đã rework hoặc chạy evaluator lại.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch: Cấu hình lưu trong `args.yaml` ghi `device=cpu`, model `yolo26n.pt`; đường dẫn `/content/Day2-Lab/` cho thấy chạy trong môi trường Colab. Phiên bản Ultralytics và Torch chưa có trong artifacts.
- Các tham số thay đổi so với notebook nếu có và lý do: Chưa có ghi chép xác nhận tham số nào được thay đổi; `args.yaml` ghi 50 epochs, `imgsz=640`, batch `-1` (tự động), `device=cpu`.
- Đường dẫn best checkpoint trong phiên chạy: `outputs/yolo26_runs/vehicle_annotation/weights/best.pt` trong Colab (bản `.pt` không đưa vào repo).

| Chỉ số validation epoch 50 trong `results.csv` | Giá trị |
| ---------------------------------------------- | ------: |
| Precision                                      | 0.26802 |
| Recall                                         | 0.42145 |
| mAP50                                          | 0.25219 |
| mAP50–95                                       | 0.17417 |

Đặt cả 2 folder `assets/eval_predictions/` và `assets/yolo26_runs/` (giải nén từ `day2_colab_outputs.zip`) cạnh báo cáo và dẫn link tương đối. Không chỉ ghi số; chỉ ra ít nhất một ảnh và vật thể cụ thể.

Các chỉ số trong bảng là validation ở epoch 50 theo `results.csv`, không phải bộ metrics xác nhận của `best.pt`. Notebook gọi `best_model.val(...)` cho run `vehicle_eval` và ghi bốn metrics vào `outputs/model_eval_metrics.json`, nhưng JSON đó không có trong artifacts hiện tại. Biểu đồ PR của `vehicle_eval` ghi mAP50 `0.276`; không thể suy chính xác precision, recall và mAP50–95 từ biểu đồ này. Ảnh dự đoán eval nằm trong `assets/eval_predictions/visuals/drive_051.jpg` đến `drive_060.jpg`; ví dụ `drive_053.jpg` có xe buýt lớn và nhiều xe con trong cùng khung hình.

Trả lời bốn câu hỏi cuối notebook:

1. Lớp nào recall thấp nhất? Ảnh nào minh họa?
2. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box?
3. Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ nhận xét?
4. Vì sao không dùng 10 ảnh eval để train? Vai trò validation của chúng trong notebook là gì?

- **Trả lời 1:** `bus` là lớp yếu nhất: biểu đồ Recall–Confidence đính kèm cho thấy recall của `bus` giảm về `0` ở confidence khoảng `0.10`; biểu đồ PR cũng có AP `0.018`, thấp nhất trong các lớp. `drive_053.jpg` minh họa cảnh có xe buýt lớn cùng nhiều xe khác; ảnh này minh họa bối cảnh, không phải số đo recall riêng của ảnh.
- **Trả lời 2:** Kiểm tra độ khít/vị trí bốn cạnh bounding box so với phần thân xe nhìn thấy; box lệch hoặc quá rộng/hẹp dễ đạt IoU ở ngưỡng thấp nhưng trượt ở các ngưỡng IoU cao.
- **Trả lời 3:** Cần kiểm tra nhầm lẫn `bus` với `car` và việc áp dụng ranh giới lớp trong guideline. Ma trận nhầm lẫn chuẩn hóa đính kèm cho thấy với nhãn thật `bus`, tỷ lệ dự đoán `car` là `0.50` và dự đoán nền là `0.50`; AP `bus` là `0.018`. Đây là lỗi mô hình, chưa đủ để kết luận guideline hoặc nhãn người gán là nguyên nhân; cần đối chiếu ảnh và nhãn cụ thể.
- **Trả lời 4:** Không dùng `eval` để train vì notebook dùng split này làm validation để đánh giá/chọn best checkpoint và quy định yêu cầu giữ nguyên split. Vì đã tham gia validation/chọn checkpoint, 10 ảnh này không còn là test set độc lập.

## 6. Khó khăn và cách xử lý

| Bước/thời điểm  | Lỗi quan sát                                                                    | Cách đã thử                                                              | Kết quả/còn thiếu                                                     |
| --------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------ | --------------------------------------------------------------------- |
| Annotation QC   | F1 trong kết quả hiện lưu dưới ngưỡng yêu cầu (`0.5198 < 0.80`).                | Chạy evaluator; kết quả được lưu ở `outputs/annotation_evaluation.json`. | Chưa có ghi chép rework hoặc kết quả chạy lại.                        |
| Colab/artifacts | CSV của quá trình train và biểu đồ PR thuộc run `vehicle_eval` có mAP50 khác nhau (`0.25219` và `0.276`). | Ghi rõ nguồn: CSV là validation epoch 50; biểu đồ là run đánh giá riêng. | `model_eval_metrics.json` không có trong artifacts hiện tại nên chưa xác nhận đủ bốn metrics của run `vehicle_eval`. |

## 7. Tự đánh giá theo rubric

Đối chiếu [RUBRIC.md](../../RUBRIC.md): phần nào đã có kết quả, phần nào còn thiếu hoặc chưa kiểm được. Không tự nhận hoàn thành bước chưa chạy.

- Có 50 file nhãn và checker cấu trúc đạt.
- Gold QC hiện chưa đạt ngưỡng F1; chưa có bằng chứng rework hoàn tất.
- Mini guideline có ba tình huống từ ảnh eval; nếu rubric yêu cầu case trong quá trình gán nhãn train thì cần thay bằng các tình huống train đã tự xử lý. Danh sách rà mắt 10 ảnh train chưa được ghi nhận.
- Có artifacts train/eval và link Colab; cần bổ sung phiên bản thư viện và xác minh metrics best checkpoint từ JSON của đúng lần chạy.
- Cần tự nộp link repo trên LMS và xác nhận quyền xem Colab.

## 8. Công cụ AI và tài liệu tham khảo

Ghi công cụ đã dùng, dùng ở bước nào và phần đã tự kiểm tra; không dùng thì ghi rõ. Liệt kê nguồn ngoài repo được sử dụng. Không ghi mật khẩu/token hoặc đính kèm gold train.

- Công cụ AI: Copilot hỗ trợ đọc hướng dẫn/artifacts và điền bản nháp các câu trả lời dựa trên số liệu trong repo và biểu đồ người học cung cấp. Các quan sát annotation và quyết định rework cần do người học tự kiểm tra, xác nhận.
- Tài liệu: `GUIDE.md`, `RUBRIC.md`, `SUBMISSION.md`, `RULES.md`, notebook và artifacts trong repository; không khai báo nguồn ngoài repo.
