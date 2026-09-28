# Quan sát vạch ô đỗ

- Hai vạch `parking_line` đã vẽ (mô tả vị trí trong ảnh): Đã vẽ các vạch sơn vàng/trắng phân chia ô đỗ nằm ở khu vực tiền cảnh (góc dưới bên phải/trái) và trung cảnh bãi đỗ xe (chạy dọc các dãy ô đỗ từ trái sang phải).
- Một vạch/dấu sơn hoặc biên **không** vẽ, và vì sao: Không vẽ đường vạch ngang mờ kẻ ngang bãi đỗ ở khu vực trung cảnh (dải vạch kẻ chỉ dẫn lối đi) và dải biên hàng rào/vỉa hè phía xa, vì đây không phải vạch sơn phân chia ranh giới giữa hai ô đỗ xe riêng biệt (`parking_line`).
- Polygon `free_space` dừng ở đâu; có phần bị che nào không: Polygon bao trùm toàn bộ dải mặt đường nhựa trống nhìn thấy được; đường viền xanh lá dừng lại và né quanh chân chiếc xe tải màu đỏ phía xa, bờ rào/hàng cây phía sau và các mép ngoài cùng của khung hình.
- Ca chưa chắc cần hỏi người soát (nếu không có, ghi “không có”): Ca các vạch sơn vàng ở dãy ô đỗ phía xa bị mờ/ngắn do góc chụp hẹp và dải vạch kẻ ngang chỉ hướng ở khu vực trung cảnh bãi đỗ.