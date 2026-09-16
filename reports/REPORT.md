# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: Bùi Duy Quảng   Nhóm: ______   Ngày: 16/09/2026

## 1. Nhãn của tôi

<!-- Lấy số từ reports/visibility_report.md hoặc outputs/visibility_report.json sau Chặng 4.
Số ảnh phải là 20; số skeleton là tổng số người trong 20 ảnh. Thời gian trung bình = tổng
thời gian gán / 20. -->

| Chỉ số | Giá trị |
| --- | ---: |
| Số ảnh đã gán | 20 |
| Số skeleton | 29 |
| v=2 / v=1 / v=0 | 415/31/47|
| Thời gian trung bình mỗi ảnh | 5 phút |

Ba khớp có `%v=1` cao nhất (chép từ `reports/visibility_report.md`):

1. right_wrist 14%
2. left_wrist 14%
3. left_knee 10%

Chúng có đúng là những khớp bạn thấy khó gán nhất không? Nếu không, giải thích.

Không, các khớp này ở vị trí hay bị che khuất bởi quần áo, xe cộ, đồ ăn

## 2. Chấm với gold

<!-- Lấy hai cột từ outputs/eval_vs_gold.json: một lần ngay khi protected release mở và một
lần sau rework. Đếm số phần tử trong từng danh sách lỗi, không tự làm tròn. -->

| Chỉ số | Trước rework | Sau rework |
| --- | ---: | ---: |
| OKS trung bình | ko lưu | 0.929 |
| OKS@0.50 | ko lưu | 1.000 |
| OKS@0.75 | ko lưu | 1.000 |
| Lỗi `dao_trai_phai` | ko lưu | 1 |
| Lỗi `nham_nguoi` | | 0 |
| Lỗi `xoa_khop_bi_che` | | 0 |

**Tôi đã sửa gì giữa hai lần chạy** (ghi cụ thể: ảnh nào, người thứ mấy, khớp nào):

- Thêm 2 người ở ảnh thứ 13
- Thêm vị trí các khớp bị đánh nhầm v=0, sửa thành v=1 ở ảnh 9

**Lỗi đảo trái/phải của tôi xảy ra ở ảnh nào?** Ảnh đó dễ hay khó? Nếu là ảnh dễ,
bạn nghĩ vì sao mình vẫn sai?

Lỗi đảo trái phải xảy ra ở ảnh 13, không phải sai mà do người này có xoay vai khiến vị trí 2 vai bị đảo

## 3. Kiểm chéo

Bạn cùng nhóm: ______

Khớp lệch `%v=1` nhiều nhất giữa hai bảng đếm:

| Khớp | Bạn | Họ | Lệch | Nguyên nhân (guideline hay gán sai?) |
| --- | ---: | ---: | ---: | --- |
| | | | | |
| | | | | |

Luật mới đã bổ sung vào `GUIDELINE_MINI.md` sau khi thống nhất:

## 4. Model

| Chỉ số | yolo26n-pose gốc | Sau fine-tune | Chênh |
| --- | ---: | ---: | ---: |
| pose_mAP50 | 0.8450 |  0.8450 | +0.0000 |
| pose_mAP50-95 | 0.6853 | 0.6908 | +0.0055 |
| pose_precision | 0.9734 | 0.9792 | +0.0058 |
| pose_recall | 0.8462 |  0.8462 | +0.0000 |
| box_mAP50-95 | 0.8119 | 0.8041 | -0.0078 |

### Trả lời năm câu hỏi ở cuối notebook

> Mỗi câu cần trỏ tới ảnh/chỉ số cụ thể. Một con số thấp không tự chứng minh nhãn sai;
> kiểm lại bằng bằng chứng thị giác và kết quả gold.

1. `pose_mAP50-95` thay đổi bao nhiêu? Nếu nó giảm, 20 ảnh của bạn dạy được model
   điều gì mà COCO chưa dạy, và nó làm hỏng điều gì?

    pose_mAP50-95 tăng từ 0.6853 lên 0.6908. 20 ảnh có thêm 1 số trường hợp đặc biệt, con người quay lưng lại, và một vài tính huống che khuất giống ảnh huấn luyện. Tuy nhiên do dữ liệu khá nhỏ nên chưa thể kết luận model tiến bộ ở mọi trường hợp.

2. `box_mAP` và `pose_mAP` chênh nhau bao nhiêu? Model tìm *người* dễ hơn hay tìm
   *khớp* dễ hơn? Vì sao?
   Sau finetune, box_mAP50-95 = 0.8041, còn pose_mAP50-95 = 0.6908, chênh nhau 0.1133 điểm. Model tìm người dễ hơn tìm đúng vị trí các khớp, vì bounding box chỉ cần bao quanh toàn thân, trong khi pose phải đặt chính xác 17 keypoint.

3. Một ảnh test model đoán sai - gọi tên lỗi theo bốn loại của slide 43
   (lệch nhẹ / đảo trái/phải / nhầm người / trượt hẳn): Ở train_13.jpg, người số 1, lỗi thuộc loại đảo trái/phải. Khi đối chiếu ảnh, các điểm hai bên cơ thể bị gán ngược do người này xoay vai, làm hướng trái/phải khó xác định. Đây không phải lỗi nhầm người hay trượt hẳn, vì skeleton vẫn nằm đúng trên cơ thể.

4. Ảnh nào có OKS thấp nhất giữa nhãn của bạn và model? Ai đúng, và bạn dựa vào đâu?
    Ảnh train 15 có OKS model với nhãn của tôi thấp nhất là 0.658. Nhãn của tôi đúng hơn, vì 2 người trong ảnh đứng tư thế xoay người khiến các khớp khó phát hiện.

5. Ảnh bạn gán tệ nhất có *cũng* là ảnh model đoán tệ nhất không? Nếu có, điều đó
   nói gì về bức ảnh đó?
   Có. Ảnh tôi gán tệ nhất là c train_15.jpg. Điều đó cho thấy ảnh có tư thế xoay vai và nhiều người đứng gần nhau khiến việc xác định trái/phải khó cả với người gán nhãn lẫn model.

## 5. Một rule evidence bạn đã dùng

Chọn một keypoint trong ảnh core mà bạn phải quyết định giữa `v=1` và `v=0`. Nêu ảnh, người,
khớp, bằng chứng nhìn thấy và lý do chọn trạng thái đó trong 3-5 câu.

train_06 người thứ nhất, keypoint mắt và mũi, ở đây tôi đánh v=0 vì hai phần này bị cả mũ bảo hiểm che hết, không thể định dạng vị trí của mắt và mũi.
