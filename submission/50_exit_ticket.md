# Exit ticket

1. Một vật ở vùng seam giữa hai camera thật xuất hiện với hai box khác nhau: đó là lỗi `DUPLICATE` hay cần một quy tắc riêng? Vì sao?
   - Cần một quy tắc riêng cho vùng seam (`SEAM_CROSS_CAMERA`). Bởi vì vật thể thực tế xuất hiện đồng thời trên hai ống kính 물리 (physical camera) khác nhau ở hai góc nhìn riêng biệt; việc gán 2 box độc lập trên mỗi ảnh gốc là đúng về mặt ống kính, nhưng hệ thống xử lý trung tâm cần quy tắc gộp (fusion rule) dựa trên calibration/BEV để tránh coi đó là 2 xe khác nhau mà không phải lỗi gán nhãn đơn thuần.

2. Một vật đi qua nhiều frame trên cùng camera: khi nào giữ cùng track ID, khi nào thêm keyframe hoặc trạng thái Outside? Nêu bằng chứng sẽ cần trước khi nối track qua hai camera.
   - Giữ cùng Track ID khi vật thể di chuyển liên tục và còn nhìn thấy trên khung hình.
   - Thêm trạng thái `Outside` hoặc ngắt track khi vật thể đi hoàn toàn ra khỏi vùng quan sát của camera quá N frame.
   - Bằng chứng cần thiết trước khi nối track qua hai camera: Timestamp đồng bộ chính xác, vận tốc/hướng di chuyển nhất quán, và vị trí chuyển tiếp liên tục trên không gian BEV/tọa độ xe.

3. Nhìn lại cả buổi: một chỗ bạn tin nhãn mình đúng nhưng reference hoặc người soát nghĩ khác (dẫn frame/`object_ref`), bạn đã xử lý thế nào, và nếu làm lại slice này bạn sẽ đổi gì trong cách làm?
   - Ở frame `adasind_128310.jpg`, với box `L5` gán nhãn `Bus` do vật thể có kích thước lớn ở vị trí trung tâm, trong khi Reference gán `Car` (`R4`). Em đã xử lý bằng cách tuân thủ kết quả đối chiếu, ghi nhận dòng chẩn đoán `E1_annotator_error` vào `findings.csv` và tiến hành rework chuyển nhãn thành `Car` để đồng bộ.
   - Nếu làm lại slice này: Em sẽ chú ý soi kỹ hơn các đặc điểm nhận dạng chi tiết của phương tiện thay vì chỉ ước lượng qua kích thước bounding box trên ảnh méo fisheye.