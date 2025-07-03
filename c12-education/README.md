# 🎓 Chương 12: Giáo dục (Education)

## 🏫 University Case Study

Chương này trình bày cách thiết kế kho dữ liệu trong môi trường giáo dục, đặc biệt tại các trường đại học. Dữ liệu tập trung vào quy trình tuyển sinh, ghi danh, sử dụng cơ sở vật chất, và theo dõi sự tham gia của sinh viên.

---

## 📈 Accumulating Snapshot for Admissions Tracking

* Theo dõi quy trình nộp hồ sơ, xét tuyển và nhập học
* Mỗi hồ sơ là một dòng trong bảng fact
* Dùng mô hình **accumulating snapshot** để cập nhật tiến trình:

  * Ngày nộp hồ sơ
  * Ngày phỏng vấn
  * Ngày được nhận
  * Ngày nhập học thực tế
* Có thể đo:

  * Tỷ lệ chuyển đổi hồ sơ
  * Thời gian trung bình giữa các bước

---

## ❌ Factless Fact Tables

* Một số sự kiện không có số liệu định lượng (số học)
* Ví dụ:

  * Sinh viên đăng ký khoá học (nhưng chưa học)
  * Ghi nhận việc tham gia buổi định hướng
* Mô hình bằng bảng fact không chứa field số liệu
* Hữu ích để kiểm tra sự kiện có/không xảy ra

---

## 📝 Student Registration Events

* Ghi nhận đăng ký môn học mỗi học kỳ:

  * Sinh viên, môn học, giảng viên, thời gian
* Dimension:

  * Sinh viên, lớp học, học kỳ, chương trình đào tạo
* Fact:

  * Trạng thái: đăng ký, rút môn, huỷ đăng ký
  * Số tín chỉ, học phí liên quan

---

## 🏢 Facilities Utilization Coverage

* Phân tích việc sử dụng cơ sở vật chất:

  * Phòng học, phòng lab, sân thể thao...
* Theo dõi lịch sử đặt lịch, sử dụng thực tế
* So sánh giữa năng lực (capacity) và thực tế sử dụng
* Mục tiêu:

  * Tối ưu hoá tài nguyên
  * Phát hiện thiếu hụt, lãng phí

---

## 👥 Student Attendance Events

* Theo dõi điểm danh lớp học, hội thảo, sự kiện
* Mỗi dòng fact = một lần điểm danh:

  * Ai? Khi nào? Ở đâu? Buổi học nào?
* Hỗ trợ phân tích:

  * Mức độ chuyên cần
  * Hiệu quả đào tạo
  * Dự đoán nguy cơ bỏ học

---

## 📌 Other Areas of Analytic Interest

* 📚 Theo dõi kết quả học tập (GPA, điểm môn)
* 🎯 Phân tích hiệu quả chương trình đào tạo
* 💰 Phân tích học bổng, học phí, tài chính sinh viên
* 👨‍🏫 Hiệu suất giảng viên, tỷ lệ hoàn thành môn học

---

## 📌 Tóm tắt chương

* Mô hình accumulating snapshot phù hợp theo dõi quá trình tuyển sinh
* Factless fact table hữu ích cho sự kiện không có dữ liệu định lượng
* Ghi nhận đăng ký môn, sử dụng cơ sở vật chất, và điểm danh là các use case phổ biến
* Phân tích dữ liệu giáo dục đa chiều: học tập, hành vi, tài chính, cơ sở vật chất
