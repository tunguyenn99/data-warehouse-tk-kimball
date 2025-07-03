# 🏗️ Chương 16: Xây dựng Kho Dữ liệu (Building the Data Warehouse)

Chương này trình bày chi tiết toàn bộ quy trình xây dựng kho dữ liệu dựa trên phương pháp **Business Dimensional Lifecycle (Vòng đời dữ liệu theo hướng nghiệp vụ)**. Đây là chương có tính tổng hợp và triển khai thực tế cao nhất trong sách. Tác giả hướng dẫn từng bước từ lập kế hoạch, thu thập yêu cầu, thiết kế kiến trúc, mô hình hóa dữ liệu, đến phát triển ETL và triển khai ứng dụng BI.

---

## 🗺️ Business Dimensional Lifecycle Road Map

### 🔍 Các giai đoạn chính:

1. 📋 Lập kế hoạch và quản lý dự án
2. 💬 Thu thập yêu cầu nghiệp vụ
3. 🏗️ Thiết kế kiến trúc kỹ thuật
4. 🧱 Thiết kế và triển khai mô hình dữ liệu
5. 🛠️ Thiết kế & phát triển ETL (Data Staging)
6. 📊 Phát triển ứng dụng phân tích
7. 🚀 Triển khai và bảo trì

Lifecycle này không mang tính tuyến tính mà thường được lặp lại cho từng data mart trong kiến trúc kho dữ liệu doanh nghiệp.

---

## 📋 Project Planning and Management

### ✅ Đánh giá mức độ sẵn sàng (Readiness)

* **Kỹ thuật**: hạ tầng lưu trữ, công cụ ETL, công cụ BI, bảo mật, mạng nội bộ
* **Tổ chức**: văn hoá dữ liệu, sự tham gia của phòng ban nghiệp vụ, chính sách chia sẻ dữ liệu
* **Con người**: sự cam kết của lãnh đạo cấp cao và sự phân công nhân lực đúng vai trò

### 🎯 Phạm vi (Scoping) & Lý do (Justification)

* Xác định rõ **data mart đầu tiên** nên tập trung vào quy trình nghiệp vụ nào (ví dụ: bán hàng, tồn kho...)
* Chỉ ra lợi ích cụ thể: tiết kiệm chi phí, tăng doanh thu, cải thiện dịch vụ khách hàng...
* Tính toán ROI (Return on Investment) sơ bộ

### 👥 Nhân sự (Staffing)

* Nhóm cần có:

  * **Project Manager**: người kết nối và điều phối toàn bộ
  * **Business Analyst**: hiểu rõ nhu cầu nghiệp vụ
  * **Data Modeler**: thiết kế mô hình dimensional
  * **ETL Developer**: xử lý pipeline dữ liệu
  * **BI Developer**: xây dashboard, báo cáo
  * **Database Administrator (DBA)**: tối ưu vận hành

### 🧭 Kế hoạch dự án (Project Plan)

* Thiết kế milestone rõ ràng: kickoff → blueprint → develop → test → deploy
* Có lịch kiểm tra tiến độ định kỳ và quản lý rủi ro (risk mitigation plan)

---

## 📌 Business Requirements Definition

### 🧰 Chuẩn bị trước khi thu thập (Preplanning)

* Lập danh sách stakeholder ở cả khối nghiệp vụ và kỹ thuật
* Lên lịch phỏng vấn, gửi trước mẫu câu hỏi và mong đợi đầu ra

### 🎤 Thu thập yêu cầu (Collecting)

* Phỏng vấn từng vai trò: nhân viên bán hàng, quản lý, kế toán...
* Tài liệu cần thu thập:

  * Mẫu báo cáo hiện tại
  * KPI đang được theo dõi
  * Câu hỏi nghiệp vụ thường xuyên
  * Loại phân tích cần thiết (slice by time, region, product...)

### 📝 Hậu kỳ (Postcollection)

* Tạo tài liệu BRD (Business Requirement Document)
* Review và xác nhận với stakeholder để tránh hiểu sai yêu cầu

---

## 🖥️ Lifecycle Technology Track

### 🏗️ Thiết kế kiến trúc kỹ thuật (Technical Architecture Design)

#### 🧭 Quy trình 8 bước:

1. Xác định nhu cầu phân tích và truy vấn
2. Đánh giá và mô tả rõ ràng nguồn dữ liệu hiện có (source systems)
3. Thiết kế zone lưu trữ: staging → core → presentation
4. Lên kiến trúc pipeline ETL/ELT rõ ràng
5. Xác định cách trình bày dữ liệu: OLAP, semantic layer, BI tools
6. Chọn phần mềm: DBMS, ETL Tool, BI Tool, Metadata Tool
7. Định nghĩa bảo mật: người dùng, phân quyền, truy cập theo vai trò
8. Đảm bảo khả năng backup, khôi phục và giám sát hệ thống

### 🧩 Lựa chọn & cài đặt sản phẩm

* Cân nhắc chi phí, khả năng mở rộng, cộng đồng hỗ trợ, tích hợp với hệ thống hiện tại
* Nên prototype trước với tập dữ liệu thật để kiểm chứng hiệu năng

---

## 🧱 Lifecycle Data Track

### 🧰 Mô hình hóa dữ liệu (Dimensional Modeling)

* Xác định grain đầu tiên
* Thiết kế star schema với fact chính và các dimension:

  * Conformed dimension để dùng lại giữa các data mart
  * Dùng SCD type 2 cho dimension thay đổi theo thời gian

### 💾 Thiết kế vật lý (Physical Design)

* Partition table theo thời gian hoặc ID
* Tối ưu chỉ mục, foreign key, view materialization nếu cần

### 🧮 Chiến lược tổng hợp dữ liệu (Aggregation Strategy)

* Tạo bảng summary ở cấp tuần/tháng để tăng tốc truy vấn
* Cần đảm bảo logic tính toán nhất quán với bảng gốc

### 📇 Chiến lược chỉ mục ban đầu (Indexing)

* Dùng index phù hợp theo loại truy vấn: full scan, range, filter theo cột phân loại
* Cân nhắc chi phí ghi (write cost) khi thêm index

---

## 🔄 Data Staging Design and Development

### 🧱 Staging bảng dimension

* Xử lý null, chuẩn hoá text, map giá trị theo danh mục
* Tạo surrogate key, xác định versioning nếu SCD

### 📦 Staging bảng fact

* Kiểm tra khóa ngoại (foreign key validation)
* Xử lý late-arriving data, gộp dữ liệu nhiều hệ thống
* Batch hoặc streaming tùy vào yêu cầu cập nhật

---

## 📊 Lifecycle Analytic Applications Track

### 📐 Thiết kế ứng dụng phân tích

* Xác định nhu cầu visual: báo cáo cứng, dashboard động, self-service BI
* Mẫu dashboard phổ biến:

  * Bán hàng theo thời gian
  * So sánh vùng địa lý
  * Theo dõi KPI hiệu suất

### 👨‍💻 Phát triển ứng dụng phân tích

* Xây dựng semantic layer để user dễ kéo thả
* Tối ưu performance: pre-aggregation, caching, filter pushdown

### 🚀 Triển khai (Deployment)

* Giao diện dễ dùng, có hướng dẫn sử dụng
* Tích hợp đăng nhập SSO nếu dùng nội bộ doanh nghiệp
* Hỗ trợ nâng cấp, rollback nếu cần

### ♻️ Bảo trì và mở rộng (Maintenance and Growth)

* Có quy trình tiếp nhận yêu cầu mới
* Cập nhật metadata catalog, lineage
* Theo dõi performance truy vấn và tối ưu định kỳ

---

## ❌ Sai lầm phổ biến cần tránh

* Không định nghĩa rõ grain → sai kết quả tổng hợp
* Thiết kế snapshot nhưng lại update như transaction
* Thiếu hoặc trùng lặp dimension (không chuẩn hoá)
* Thiếu kiểm tra chất lượng dữ liệu (data quality check)
* Thiếu test kế hoạch ETL hoặc xử lý lỗi không đầy đủ

---

## 📌 Tổng kết chương

* Chương 16 là "bản kế hoạch hành động" tổng thể để triển khai kho dữ liệu thành công
* Từ quản trị dự án đến kiến trúc kỹ thuật, mô hình hóa và ứng dụng – tất cả cần được kết nối liền mạch
* Mô hình vòng đời Dimensional Lifecycle giúp doanh nghiệp triển khai nhanh, đúng hướng, và có thể mở rộng lâu dài