# Đề xuất gold set theo camera — tình huống giả lập

**Đầu bài:** 50.000 frame từ bốn camera SVM, ngân sách chọn 200 frame để review/gold. Đây là tình huống trên slide, **không phải** 50.000 frame có trong repo. Phân bổ đúng 200 ở `45_sampling_plan.csv` cho bốn camera, mỗi camera có normal và hard slice. “Gold set” ở đây là **kế hoạch tạo** reference sau kiểm chứng, không phải teaching reference ADASIND hoặc nhãn bạn vừa vẽ.

| camera_id | Hard case cần chọn | Vì sao dễ sai | Annotation space / calibration cần giữ | Cách review trước khi gọi là gold |
|---|---|---|---|---|
| front | Xe cắt ngang mép kính, chói sáng | Méo biến dạng fisheye góc rộng | Tọa độ ảnh gốc + thông số camera matrix | 2 QA độc lập duyệt mù + Lead xác nhận |
| rear | Xe bám đuôi sát, lóa đèn đêm | Nhầm lẫn vật thể do lóa sáng | Tọa độ ảnh gốc + vùng che thân xe | So sánh chéo với mô hình AI + kiểm tra viền |
| left | Vật thể di chuyển qua đường seam góc trái | Vật thể xuất hiện ở điểm nối 2 camera | Calibration méo viền + nối khung hình | Review đồng thời 2 góc quay trước/trái |
| right | Người đi bộ / Xe hai bánh sát điểm mù | Nhỏ, mờ và truncated bởi viền kính | Tọa độ mặt phẳng BEV + ảnh gốc | Đối chiếu polygon ignore_region và thuộc tính |

- Khi nào cần refresh gold set (đổi camera, calibration hoặc rule): Cần refresh khi thay đổi cấu hình phần cứng góc quay camera, cập nhật lại thông số hiệu chuẩn (intrinsic/extrinsic calibration), hoặc khi có sự điều chỉnh trong quy tắc gán nhãn (guideline v1.1.0).
- Một ca seam/cross-camera cần policy và evidence trước khi ghép hai box: Cần quy tắc đồng bộ thời gian (timestamp matching) và kiểm tra hình học 3D/BEV để xác định 2 box ở 2 camera có cùng thuộc 1 vật thể thực tế hay không trước khi ghép/merge track ID.
- Vì sao peer agreement hoặc quality report trên ảnh một camera chưa chứng minh gold set đúng for cả bốn camera: Vì ảnh đơn camera chưa thể hiện được vùng mù, lỗi méo ghép góc seam, và độ lệch góc nhìn giữa các camera trên cùng hệ thống 360 SVM.