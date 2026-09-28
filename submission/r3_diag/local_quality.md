# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `609fad2cf88ada46a7236c90c56c0b64f98d19c5e5df0edb136884c544522fc6`; slice `B3-mid`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_128310.jpg, adasind_140160.jpg, adasind_230910.jpg. Frame thiếu trong export: không.
TP=15; FP=3; FN=5; số lần đối chiếu=21; mean IoU của TP=0.848.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.714 | 0.937 | 0.810 |
| precision | 0.833 | 0.772 | 0.000 |
| recall | 0.750 | 0.688 | 0.000 |
| jaccard | 0.652 | 0.643 | 0.000 |
| dice | 0.789 | 0.712 | 0.000 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 2 | 0 | 0 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 |
| Bus | 0 | 1 | 0 | 0.952 | 0.000 | 0.000 | 0.000 | 0.000 |
| Car | 2 | 0 | 2 | 0.905 | 1.000 | 0.500 | 0.500 | 0.667 |
| Pedestrian | 5 | 1 | 3 | 0.810 | 0.833 | 0.625 | 0.556 | 0.714 |
| ThreeWheeler | 2 | 0 | 0 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 |
| Truck | 4 | 1 | 0 | 0.952 | 0.800 | 1.000 | 0.800 | 0.889 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_128310.jpg | 4 | 1 | 1 | 0.800 | 0.800 | 0.800 |
| adasind_140160.jpg | 3 | 0 | 0 | 1.000 | 1.000 | 1.000 |
| adasind_230910.jpg | 8 | 2 | 4 | 0.615 | 0.800 | 0.667 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Bus | Car | Pedestrian | ThreeWheeler | Truck | <missing> |
|---|---:|---:|---:|---:|---:|---:|---:|
| Bike | 2 | 0 | 0 | 0 | 0 | 0 | 0 |
| Bus | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| Car | 0 | 1 | 2 | 0 | 0 | 1 | 0 |
| Pedestrian | 0 | 0 | 0 | 5 | 0 | 0 | 3 |
| ThreeWheeler | 0 | 0 | 0 | 0 | 2 | 0 | 0 |
| Truck | 0 | 0 | 0 | 0 | 0 | 4 | 0 |
| <extra> | 0 | 0 | 0 | 1 | 0 | 0 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.
