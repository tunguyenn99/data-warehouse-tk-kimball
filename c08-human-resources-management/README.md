# 🧑‍💼 Chương 8: Quản lý Nhân sự (Human Resources Management)

## 🧾 Giới thiệu

Chương này trình bày cách mô hình hóa dữ liệu nhân sự trong kho dữ liệu, bao gồm các hoạt động như theo dõi thay đổi nhân sự, khảo sát, ghi nhận thông tin phức tạp (keyword, text), và xử lý các phép lọc logic nâng cao.

---

## ⏳ Time-Stamped Transaction Tracking in a Dimension

Một nhân viên có thể thay đổi nhiều thông tin như:

* Phòng ban, chức vụ
* Lương, trạng thái công việc

👉 Ta sử dụng **SCD Type 2** để lưu các thay đổi theo thời gian:

* Mỗi thay đổi tạo một dòng mới trong dimension
* Có thêm các cột ngày hiệu lực (effective date, end date)

## 📆 Time-Stamped Dimension với Periodic Snapshot Facts

Kết hợp dimension có timestamp (SCD2) với bảng fact snapshot để ghi lại trạng thái nhân viên tại từng thời điểm:

* Ví dụ: số lượng nhân viên, tổng chi phí nhân sự mỗi tháng
* Có thể tính tổng lương, headcount theo phòng ban, theo kỳ

## 🧮 Audit Dimension

Dùng để ghi nhận metadata về quá trình ghi nhận dữ liệu:

* Nguồn dữ liệu
* Thời điểm load
* Người xử lý
* Trạng thái: hợp lệ, ngoại lệ...

📌 Audit dimension giúp truy xuất, kiểm tra và debug pipeline dữ liệu.

## 🧠 Keyword Outrigger Dimension

Một số thuộc tính nhân sự có thể là dạng "nội dung mở", ví dụ:

* Kỹ năng (SQL, Python, Leadership...)
* Sở thích

→ Dùng bảng outrigger dạng từ khóa (nhiều-nhiều):

* 1 nhân viên có thể gắn với nhiều từ khóa
* Hỗ trợ phân tích, tìm kiếm theo tag

## 🔀 AND/OR Dilemma

Khi tìm nhân sự thỏa mãn nhiều điều kiện:

* Có kỹ năng A **và** B (AND)
* Có kỹ năng A **hoặc** B (OR)

📌 Dùng **bridge table** với fact phụ trợ để xử lý phép lọc logic này.

## 🔎 Searching for Substrings

Đối với các dữ liệu dạng mô tả:

* Có thể cần tìm kiếm text không chính xác (fuzzy match)
* Cân nhắc lưu text gốc và thêm bản rút gọn/chuẩn hóa phục vụ tìm kiếm

📌 Một số công cụ tìm kiếm văn bản (ElasticSearch) có thể tích hợp vào pipeline nếu cần.

## 📋 Survey Questionnaire Data

Phân tích dữ liệu khảo sát nhân viên:

* Có thể model mỗi câu hỏi là một dimension
* Hoặc pivot theo câu hỏi và lưu vào fact bảng ngang
* Hỗ trợ phân tích xu hướng hài lòng, nhu cầu đào tạo, phúc lợi...

---

## 📌 Tóm tắt chương

* Dữ liệu nhân sự thường xuyên thay đổi → cần dùng SCD2
* Snapshot fact theo tháng giúp phân tích headcount, chi phí
* Dùng audit dimension để theo dõi và kiểm tra ETL
* Outrigger và bridge table hỗ trợ phân tích thuộc tính phức tạp
* Xử lý logic AND/OR và tìm kiếm văn bản giúp nâng cao tính linh hoạt trong phân tích
