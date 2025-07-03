# 🏥 Chương 13: Y tế (Health Care)

## 🔄 Health Care Value Circle

* Trong lĩnh vực chăm sóc sức khoẻ, vòng đời giá trị bao gồm: tiếp nhận bệnh nhân → chẩn đoán → điều trị → thanh toán → theo dõi hậu kỳ
* Mỗi giai đoạn đều sinh ra dữ liệu quan trọng cần lưu trữ và phân tích

---

## 💳 Health Care Bill

* Mỗi hóa đơn y tế bao gồm nhiều dịch vụ:

  * Khám bệnh, xét nghiệm, phẫu thuật, giường bệnh, thuốc...
* Mỗi dòng hóa đơn nên là một dòng trong fact table:

  * Dimension: bệnh nhân, bác sĩ, loại dịch vụ, ngày
  * Fact: chi phí, thời lượng sử dụng, trạng thái thanh toán

---

## 📅 Roles Played by the Date Dimension

* Dữ liệu y tế nhạy cảm về thời gian:

  * Ngày nhập viện, xuất viện, ngày chẩn đoán, ngày điều trị
* Mỗi vai trò thời gian cần một alias riêng trong date dimension

---

## 🩺 Multivalued Diagnosis Dimension

* Một bệnh nhân có thể có nhiều chẩn đoán (ICD codes)
* Dùng bridge table để ánh xạ nhiều giá trị chẩn đoán cho một sự kiện điều trị

---

## 💰 Extending Billing Fact Table to Show Profitability

* Bổ sung các trường:

  * Chi phí thực tế
  * Doanh thu thu về
  * Biên lợi nhuận (profit margin)
* Cho phép phân tích hiệu quả tài chính theo dịch vụ, bác sĩ, phòng ban...

---

## 🛏️ Dimensions for Billed Hospital Stays

* Một đợt nằm viện có thể bao gồm nhiều dịch vụ
* Các dimension đi kèm:

  * Loại phòng (thường, VIP)
  * Mục đích nằm viện (điều trị, hậu phẫu...)
  * Khoa điều trị, trạng thái bệnh nhân, bảo hiểm

---

## 🧬 Complex Health Care Events

* Một sự kiện y tế có thể kéo dài và gồm nhiều phần:

  * Ví dụ: quá trình điều trị ung thư kéo dài nhiều tháng
* Cần theo dõi qua snapshot hoặc accumulating snapshot

---

## 📋 Medical Records

* Lưu trữ hồ sơ y tế:

  * Kết quả xét nghiệm, đơn thuốc, hình ảnh chẩn đoán
* Có thể cần dùng document storage hoặc blob để lưu dữ liệu phi cấu trúc

---

## 📉 Fact Dimension for Sparse Facts

* Một số bảng fact có rất ít fact (sparse)
* Có thể đưa các thuộc tính phân tích vào chính bảng fact (fact dimension)

---

## 🔁 Going Back in Time

### 🐢 Late-Arriving Fact Rows

* Dữ liệu sự kiện đến trễ so với thời gian thực tế xảy ra
* Cần cơ chế cập nhật hoặc đánh dấu "late arrival"

### 🐌 Late-Arriving Dimension Rows

* Dimension chưa có sẵn khi fact đến
* Tạo bản ghi placeholder rồi cập nhật sau

---

## 📌 Tóm tắt chương

* Hệ thống y tế có dữ liệu đa chiều, đa thời điểm, và thường phức tạp
* Hóa đơn y tế nên được model chi tiết từng dịch vụ
* Diagnosis dùng bridge table để quản lý giá trị đa chẩn đoán
* Có thể mở rộng bảng fact để phân tích lợi nhuận
* Xử lý dữ liệu đến trễ (late-arriving) là điều bắt buộc trong môi trường này
