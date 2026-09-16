# Visibility report

- Thư mục nhãn: `dataset\labels\train`
- 20 ảnh, 27 skeleton, trung bình 15.22 khớp có v > 0 mỗi người
- Tổng: v=2 386 | v=1 25 | v=0 48

| # | Khớp | v=2 | v=1 | v=0 | %v=1 |
| ---: | --- | ---: | ---: | ---: | ---: |
| 0 | nose | 22 | 2 | 3 | 7% |
| 1 | left_eye | 22 | 2 | 3 | 7% |
| 2 | right_eye | 22 | 2 | 3 | 7% |
| 3 | left_ear | 24 | 3 | 0 | 11% |
| 4 | right_ear | 26 | 1 | 0 | 4% |
| 5 | left_shoulder | 27 | 0 | 0 | 0% |
| 6 | right_shoulder | 27 | 0 | 0 | 0% |
| 7 | left_elbow | 26 | 0 | 1 | 0% |
| 8 | right_elbow | 25 | 0 | 2 | 0% |
| 9 | left_wrist | 23 | 3 | 1 | 11% |
| 10 | right_wrist | 21 | 3 | 3 | 11% |
| 11 | left_hip | 25 | 2 | 0 | 7% |
| 12 | right_hip | 26 | 1 | 0 | 4% |
| 13 | left_knee | 17 | 3 | 7 | 11% |
| 14 | right_knee | 19 | 0 | 8 | 0% |
| 15 | left_ankle | 16 | 3 | 8 | 11% |
| 16 | right_ankle | 18 | 0 | 9 | 0% |

## Đọc bảng này thế nào

1. Khớp nào có **%v=1 cao**: khớp hay bị che. Cổ tay và hông thường là hai vị trí cần xem lại guideline trước khi kết luận.
2. Khớp nào có **v=0 cao bất thường**: mọi người đang dùng Outside ở chỗ đáng lẽ là Occluded. Đó là lỗi số 3 của slide 46, và nó xoá thẳng khớp đó khỏi bảng điểm OKS.
3. Khi so hai người: **lệch lớn = bất đồng về guideline**, không phải về bức ảnh. Sửa guideline trước, sửa nhãn sau.
