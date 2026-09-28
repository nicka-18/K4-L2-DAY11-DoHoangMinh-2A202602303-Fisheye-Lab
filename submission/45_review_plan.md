# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| `adasind_230910.jpg` | 6 ca (MISSING 4, WRONG_CLASS 1, BOX_GEOMETRY 1) | Frame có tỷ lệ lỗi cao nhất slice (bỏ sót Pedestrian R8, R10, gán nhầm Truck L6) | Báo cáo `compare.md` và ảnh `submission/screenshots/02_wrongclass_truck.png` |
| `adasind_128310.jpg` | 3 ca (SPURIOUS 1, WRONG_CLASS 1, MISSING 1) | Frame gặp lỗi sai phân loại phương tiện chính (L5=Bus vs R4=Car) và thừa polygon ignore_region | Báo cáo `local_quality_conflicts.csv` dòng 0 và ảnh `submission/screenshots/01_spurious_egobody.png` |

Giới hạn của kết luận từ ba frame ADASIND: Mẫu dữ liệu chỉ gồm 3 frame liên tiếp trên 1 camera fisheye đơn, không phản ánh được tổng thể phân bố lỗi trên toàn bộ chuỗi video dài hoặc các góc quay khác của xe.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv` (kể cả tránh đếm nhiều frame liền nhau trong cùng cảnh như nhiều ca độc lập), và vì sao kế hoạch đó chỉ giúp tìm ca cần soi, chưa đo được tỷ lệ lỗi:
- Để kiểm soát độ phủ, 200 frame được chia đều theo 8 ô (4 camera × 2 điều kiện normal/hard). Sử dụng phương pháp lấy mẫu cách quãng (stride) tối thiểu 30-50 frame giữa hai mẫu được chọn trong cùng một cảnh quay để tránh hiện tượng lặp lại thông tin (data redundancy).
- Kế hoạch lấy mẫu tập trung chọn các ca khó (hard cases) nên mẫu bị lệch (biased sample), mục đích là để tìm và phát hiện các góc tối/lỗi biên hệ thống (edge cases) chứ không đại diện cho phân bố ngẫu nhiên của toàn bộ 50.000 frame, do đó không dùng số liệu này để tính tỷ lệ lỗi chung (error rate) của toàn hệ thống production.