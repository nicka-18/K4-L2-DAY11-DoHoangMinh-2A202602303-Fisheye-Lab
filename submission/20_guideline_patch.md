# Guideline patch

- **Rule mới đề xuất:** Bổ sung quy tắc làm rõ ranh giới phân biệt giữa `Car` và `Truck`/`Bus` trên ống kính fisheye méo viền, đồng thời nghiêm cấm tự động vẽ polygon `ego_body` khi mặt ca-pô/thân xe không xuất hiện rõ ràng trên khung hình.
- **Áp dụng cho:** Tất cả class phương tiện giao thông (`Car`, `Truck`, `Bus`) và polygon `ignore_region` (`ego_body`).
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** Luật hiện tại R06 chưa ghi rõ điều kiện cứng để nhận biết sự hiện diện của thân xe ego trên các góc quay fisheye khác nhau, dẫn đến thói quen gán mặc định polygon ego_body của annotator; R01 chưa cung cấp tỉ lệ biến dạng tiêu chuẩn cho xe tải/xe buýt khi nằm ở mép kính.
- **`rules_version` mới:** v1.1.0
- **Hiệu lực từ:** Vòng Rework (P5) và các đợt gán nhãn tiếp theo.