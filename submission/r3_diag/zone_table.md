# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 8 | 3 | 2 | 3 | 3 | WRONG_CLASS (1) |
| mid | 9 | 2 | 1 | 4 | 3 | WRONG_CLASS (1) |
| edge | 3 | 0 | 0 | 1 | 2 | ATTRIBUTE (1) |

## Nhận xét

- Zone nào người (L) và model (M) gãy nhiều nhất, dẫn số ở bảng trên:
  - Với người (L): Gãy nhiều nhất ở zone `center` (3 missing, 2 spurious) và zone `mid` (2 missing, 1 spurious) do bỏ sót các vật thể xa/nhỏ (Pedestrian R8, R10) và vẽ thừa polygon ignore_region.
  - Với model (M): Gãy nhiều nhất ở zone `mid` (4 missing, 3 thừa) và zone `center` (3 missing, 3 thừa) do Model AI dự đoán sai/nhiễu nhiều vật thể (FP) và bỏ sót các vật thể trong vùng bóng râm.

- Giả thuyết vì sao (méo fisheye, box lỏng, thiếu `ego_body`, ...) và giới hạn của slice ba frame:
  - Do góc nhìn ống kính fisheye biến dạng mạnh ở vùng mid/edge làm hình ảnh xe bị dẹt ngang dẫn tới annotator gán nhầm class (Car thành Truck/Bus), đồng thời thói quen vẽ mặc định polygon `ignore_region` (ego_body) khi không có thân xe xuất hiện làm tăng lỗi spurious.
  - Giới hạn: Slice 3 frame chỉ đại diện cho một bối cảnh quay duy nhất (ADASIND B3-mid), chưa đủ số lượng mẫu thống kê để đánh giá độ bao phủ toàn diện cho toàn bộ mô hình AI trên các điều kiện thời tiết/ban đêm khác nhau.