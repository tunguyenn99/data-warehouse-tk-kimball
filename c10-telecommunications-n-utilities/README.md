# 📡 Chương 10: Viễn thông và Tiện ích (Telecommunications and Utilities)

## 📞 1. Case Study: Ngành Viễn thông

Chương này tập trung vào thiết kế data warehouse trong ngành viễn thông và tiện ích – nơi dữ liệu giao dịch rất lớn, phức tạp và cần độ chính xác cao. Các loại dịch vụ bao gồm cuộc gọi, tin nhắn, dữ liệu, điện lực, nước, truyền hình cáp...

---

## 🧠 2. Các nguyên tắc thiết kế cần lưu ý

### 🔬 2.1. Granularity
- Xác định đúng cấp độ grain: từng sự kiện (cuộc gọi, giao dịch), hoặc cấp tài khoản.
- Mô hình có thể cần grain kép: grain event và grain tổng hợp theo khách hàng.

### 📅 2.2. Date Dimension
- Phân tích dữ liệu theo ngày, giờ, phút, giây, thậm chí tới mili-giây.
- Có thể mở rộng thêm hierarchy như buổi sáng, ca làm việc, khung giờ cao điểm.

### 🧾 2.3. Degenerate Dimensions
- Các ID giao dịch như Call ID, Transaction ID không cần bảng dimension.
- Được lưu trực tiếp trong bảng fact dưới dạng degenerate dimension.

### 🔤 2.4. Dimension Decodes and Descriptions
- Dữ liệu thường mã hoá → cần tạo bảng decode cho trạng thái dịch vụ, thiết bị, lỗi...

### 🔑 2.5. Surrogate Keys
- Khuyến nghị sử dụng surrogate key thay vì business key để xử lý SCD và dữ liệu thiếu nhất quán.

### ⚖️ 2.6. Too Many (or Too Few) Dimensions
- Tránh lạm dụng dimension → khiến model cồng kềnh.
- Đồng thời đảm bảo không thiếu các dimension phân tích quan trọng như gói cước, vị trí, khách hàng...

---

## 📝 3. Bài tập thiết kế (Draft Design Discussion)

- Thiết kế data mart mẫu cho giao dịch gọi điện
- Gồm fact table chi tiết cuộc gọi & các dimension như:
  - 📱 Khách hàng
  - 🕒 Thời gian
  - 📍 Vị trí
  - 📡 Thiết bị
  - 📦 Gói dịch vụ
  - 🔁 Trạng thái cuộc gọi (roaming, thất bại, quốc tế...)

---

## 🌍 4. Dimension Vị trí địa lý

### 🗺️ 4.1. Location Outrigger
- Sử dụng outrigger để tách chi tiết địa lý: phường/xã, quận/huyện, tỉnh/thành phố...

### 🧭 4.2. GIS Integration
- Tích hợp hệ thống thông tin địa lý (GIS) để:
  - Vẽ bản đồ nhiệt
  - Phân tích lưu lượng theo khu vực
  - Định vị thiết bị và trạm phát sóng

---

## 📌 5. Tổng kết chương

- ✅ Ngành viễn thông cần mô hình hoá granular (event-level) và chuẩn hóa
- ✅ Degenerate dimension hữu dụng với mã giao dịch
- ✅ Date dimension cần độ phân giải cao
- ✅ Outrigger & GIS giúp tăng cường phân tích không gian
- ✅ Tối ưu số lượng dimension giúp cải thiện hiệu suất và tính mở rộng
