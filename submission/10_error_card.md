# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B3 | BOX_GEOMETRY | 1 |
| center | B3 | MISSING | 5 |
| center | B3 | SPURIOUS | 5 |
| center | B3 | WRONG_CLASS | 1 |
| edge | B3 | ATTRIBUTE | 1 |
| edge | B3 | MISSING | 1 |
| edge | B3 | SPURIOUS | 2 |
| mid | B3 | MISSING | 5 |
| mid | B3 | SPURIOUS | 3 |
| mid | B3 | WRONG_CLASS | 1 |
| mid | C0 | ATTRIBUTE | 1 |
| unknown | B3 | SPURIOUS | 3 |
| unknown | C0 | IGNORE_SCOPE | 1 |
| unknown | C0 | MISSING | 1 |

## Top defects
- SPURIOUS: 13 (ví dụ frame adasind_128310.jpg)
- MISSING: 12 (ví dụ frame adasind_019560.jpg)
- ATTRIBUTE: 2 (ví dụ frame adasind_019560.jpg)

## Phân tích của bạn

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy:
  - Lỗi `SPURIOUS` nổi bật nhất do annotator tiện tay vẽ polygon `ignore_region` với `reason: ego_body` trên cả 3 frame (`adasind_128310.jpg`, `adasind_140160.jpg`, `adasind_230910.jpg`) thuộc Slice B3-mid dù ảnh không nhìn thấy thân xe (`E1_annotator_error`), vi phạm R06.
  - Lỗi `MISSING` và `WRONG_CLASS` tập trung ở vùng center và mid trên frame `adasind_230910.jpg` (bỏ sót `Pedestrian R8`, `R10` và gán nhầm `Truck L6` cho `Car R7`) do vật thể ở xa bị thu nhỏ, méo hình học fisheye dẫn đến annotator quan sát sót và nhầm phân loại (`E1_annotator_error`).
- Cách sửa và ai nhận việc (`owner`):
  - `annotator`: Thực hiện xóa polygon `ignore_region` thừa trên cả 3 frame, sửa nhãn `Truck` (L6) thành `Car`, bổ sung 2 Bbox `Pedestrian` bị sót trên frame `adasind_230910.jpg`, và sửa nhãn `Bus` (L5) thành `Car` trên frame `adasind_128310.jpg`.
  - `qa`: Kiểm tra đối chiếu lại hình học Bbox sau khi sửa qua giao diện `qa_overlay.html`.
- Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule):
  - Ảnh minh họa: `submission/screenshots/01_spurious_egobody.png` (thừa ego_body) và `submission/screenshots/02_wrongclass_truck.png` (gán nhầm Truck).
  - Dòng findings: `r2_qa,B3-mid,adasind_128310.jpg,IGNORE_REGION 7,L_only,SPURIOUS` và `r1_craft,B3-mid,adasind_230910.jpg,L6+R7,LRM,WRONG_CLASS`.
  - Quy tắc chiếu theo: `R06_IGNORE_REGION` và `R01_BOX_BOUNDS`.