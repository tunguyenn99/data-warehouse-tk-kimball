# 💳 Chương 9: Dịch vụ Tài chính (Financial Services)

## 🏦 Banking Case Study

Chương này tập trung vào cách mô hình dữ liệu trong lĩnh vực tài chính, đặc biệt là ngân hàng. Với đặc thù về giao dịch phức tạp, sản phẩm đa dạng, và yêu cầu phân tích theo thời gian thực hoặc thời điểm xác định, thiết kế trong ngành tài chính cần cấu trúc linh hoạt và nhất quán.

---

## 🧪 Dimension Triage

Ngành ngân hàng có số lượng dimension lớn, cần phân loại:

* Dimension cốt lõi: Khách hàng, Tài khoản, Sản phẩm, Chi nhánh
* Dimension tham chiếu: Loại giao dịch, Kênh giao dịch, Trạng thái
* Dimension phụ: Chi tiết nhân viên xử lý, metadata quy trình

📌 Việc phân loại giúp tối ưu thiết kế và dễ mở rộng mô hình.

## 🏠 Household Dimension

Một khách hàng cá nhân có thể là thành viên của nhiều nhóm (hộ gia đình, nhóm tài khoản...):

* Tạo dimension "household" để phân tích theo nhóm
* Mỗi khách hàng gắn với một mã household ID
* Có thể model quan hệ một-nhiều hoặc nhiều-nhiều tuỳ theo hệ thống

## 🔗 Multivalued Dimensions

Khách hàng hoặc tài khoản có thể gắn với nhiều đặc tính:

* Loại hình khách hàng (VIP, ưu tiên, nội bộ...)
* Nhiều sở thích hoặc nhu cầu đầu tư

📌 Cần dùng bridge table để ánh xạ nhiều giá trị cho một thực thể

## 🧮 Minidimensions Revisited

Một số thuộc tính có thay đổi nhanh (nhóm tuổi, mức thu nhập, phân khúc rủi ro...)

* Nên tách thành minidimension để tránh SCD quá lớn
* Fact sẽ tham chiếu đến minidimension để phân tích nhanh

## 📊 Arbitrary Value Banding of Facts

Ví dụ: nhóm số dư tài khoản thành các mức:

* < 1 triệu, 1–5 triệu, > 5 triệu

Thay vì lưu trong fact, nên tạo một dimension "banding" để phân tích linh hoạt hơn, tránh hardcode logic vào report.

## 📅 Point-in-Time Balances

Tài khoản thay đổi liên tục nên cần ghi nhận snapshot tại một thời điểm:

* Số dư tài khoản mỗi ngày / tháng / thời điểm cụ thể
* Grain: \[Tài khoản, Ngày]
* Dùng cho phân tích tài sản, thanh khoản, hoặc phân loại khách hàng

## 🧬 Heterogeneous Product Schemas

Ngân hàng cung cấp nhiều loại sản phẩm:

* Tài khoản tiết kiệm, thẻ tín dụng, vay tiêu dùng, bảo hiểm...

Mỗi sản phẩm có cấu trúc dữ liệu khác nhau
👉 Có 2 hướng xử lý:

* Tạo fact riêng cho từng loại sản phẩm
* Thiết kế schema chuẩn hóa (unified schema) → phức tạp hơn nhưng thuận tiện phân tích chéo

## 🔄 Heterogeneous Products with Transaction Facts

Khi dùng bảng fact giao dịch tổng hợp cho tất cả sản phẩm:

* Thêm dimension "Product Type"
* Cần kiểm tra chặt chẽ các cột fact: có thể null cho một số loại sản phẩm
* Dễ triển khai nhưng phức tạp hóa việc phân tích chi tiết

---

## 📌 Tóm tắt chương

* Tài chính yêu cầu mô hình linh hoạt, phân loại dimension rõ ràng
* Household và multivalued dimension rất quan trọng trong phân tích khách hàng
* Minidimension hỗ trợ hiệu quả cho các thuộc tính thay đổi nhanh
* Dữ liệu snapshot theo thời điểm giúp phân tích số dư và rủi ro
* Cần chọn giữa schema phân tán và schema hợp nhất cho sản phẩm tài chính đa dạng
