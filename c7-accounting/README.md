# 📘 Chương 7: Kế toán (Accounting)

## 🧾 Accounting Case Study

Chương này mô tả cách mô hình dữ liệu kế toán trong kho dữ liệu, tập trung vào hệ thống sổ cái (General Ledger), quy trình lập ngân sách, báo cáo tài chính và bảng fact hợp nhất. Kế toán yêu cầu độ chính xác cao, logic phức tạp và kiểm soát dữ liệu chặt chẽ hơn các chủ đề khác.

---

## 📚 General Ledger Data

### 🗓️ General Ledger Periodic Snapshot

* Ghi nhận số dư tài khoản định kỳ (hàng tháng, hàng quý...)
* Mỗi dòng fact đại diện cho số dư tại một thời điểm
* Grain: \[Account, Time Period]

**Dimension:**

* Thời gian (tháng, quý)
* Tài khoản (Account)
* Trung tâm chi phí / bộ phận
* Công ty / đơn vị kinh doanh

**Fact:**

* Số dư đầu kỳ, cuối kỳ
* Tổng phát sinh Nợ / Có trong kỳ

### 📒 General Ledger Journal Transactions

* Ghi nhận từng bút toán kế toán (journal entry)
* Grain: \[Journal Entry ID, Account]

**Fact:**

* Ngày ghi nhận
* Số tiền Nợ / Có
* Mô tả bút toán
* Người ghi nhận

📌 Các giao dịch journal có thể dùng để kiểm toán, theo dõi thay đổi chi tiết hơn so với snapshot định kỳ.

---

## 📊 Financial Statements

Từ dữ liệu kế toán, có thể xây dựng:

* Báo cáo kết quả kinh doanh (P\&L)
* Bảng cân đối kế toán (Balance Sheet)
* Lưu chuyển tiền tệ (Cash Flow)

🧱 Các báo cáo này thường dựa trên fact snapshot định kỳ hoặc bảng hợp nhất.

---

## 💰 Budgeting Process

Quy trình lập ngân sách thường tách biệt khỏi dữ liệu thực tế:

* Dữ liệu dự báo (budget plan) theo tháng/quý/năm
* Mỗi dòng fact là một mục tiêu ngân sách theo \[Account, Time Period, Cost Center]

📌 Cần phân biệt rõ fact "thực tế" (actuals) và "ngân sách" (budget) để so sánh chênh lệch.

---

## 🔗 Consolidated Fact Tables

Để phục vụ báo cáo tổng hợp, có thể thiết kế bảng fact hợp nhất:

* Kết hợp dữ liệu actual, budget, forecast
* Thêm dimension "Scenario" để phân biệt loại dữ liệu

Grain: \[Account, Time Period, Scenario]

---

## 🧰 OLAP và Giải pháp Phân tích đóng gói

Kế toán là lĩnh vực phổ biến của OLAP:

* Hỗ trợ pivot table đa chiều theo thời gian, account, trung tâm chi phí...
* Giải pháp phân tích đóng gói thường có sẵn các mô hình báo cáo chuẩn

📌 Tuy nhiên, việc triển khai trong kho dữ liệu vẫn cần kiểm soát dữ liệu, lineage và khả năng truy xuất nguồn gốc (audit trail).

---

## 📌 Tóm tắt chương

* Kế toán yêu cầu các mô hình snapshot định kỳ và journal transaction
* Phân biệt rõ giữa dữ liệu actual, budget và forecast
* Bảng fact hợp nhất hỗ trợ phân tích so sánh theo nhiều kịch bản
* Có thể tích hợp với các công cụ OLAP để hỗ trợ phân tích đa chiều
* Cần đảm bảo tính minh bạch và kiểm toán trong mô hình hóa kế toán
