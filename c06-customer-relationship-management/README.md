# 📇 Chương 6: Quản lý Mối quan hệ Khách hàng (Customer Relationship Management)

## 🌐 CRM Overview

Quản lý quan hệ khách hàng (CRM) là phương pháp tiếp cận toàn diện giúp tổ chức xây dựng mối quan hệ bền vững với khách hàng thông qua việc ghi nhận, phân tích và tối ưu hóa các tương tác. Trong kho dữ liệu, CRM đóng vai trò trung tâm để phân tích hành vi, hiệu suất và giá trị lâu dài của khách hàng.

## ⚙️ Operational và Analytical CRM

* **Operational CRM**: Hệ thống nghiệp vụ dùng để quản lý các tương tác hàng ngày như bán hàng, dịch vụ khách hàng, marketing tự động.
* **Analytical CRM**: Phân tích các dữ liệu từ operational CRM để đưa ra quyết định kinh doanh, đánh giá hiệu quả chiến dịch, hành vi tiêu dùng, v.v.

Cả hai cần được tích hợp vào kho dữ liệu để đảm bảo cái nhìn toàn diện về khách hàng.

## 📦 Packaged CRM

Các giải pháp CRM đóng gói như Salesforce, Microsoft Dynamics, SAP CRM... cung cấp các schema có sẵn. Tuy nhiên, các hệ thống này thường phức tạp, có nhiều lớp quan hệ. Trong data warehouse, cần "flatten" chúng thành dimension và fact để dễ phân tích.

## 👤 Customer Dimension

Là trung tâm của CRM. Cấu trúc bao gồm:

* Customer ID (surrogate key)
* Tên, giới tính, ngày sinh
* Thông tin liên hệ: email, điện thoại
* Thông tin tài khoản: ngày tạo, trạng thái, nhóm khách hàng
* Phân loại: B2C, B2B, VIP, Casual...

### ✂️ Name and Address Parsing

* Cần chuẩn hóa tên, địa chỉ thành các thành phần riêng (họ, tên, đường, phường, quận...)
* Hỗ trợ tìm kiếm, phân vùng, và làm sạch dữ liệu

### 🏷️ Other Common Customer Attributes

* Kênh đăng ký (web, app, call center)
* Ngôn ngữ ưa thích
* Loại tài khoản
* Trạng thái thành viên (active, inactive, dormant)

## 🧩 Dimension Outriggers

Với các thuộc tính ít thay đổi nhưng cần mô tả riêng như:

* Nhóm nhân khẩu học
* Hạng khách hàng
* Mức độ tín nhiệm

→ có thể tạo bảng dimension phụ (outrigger) thay vì nhồi hết vào bảng customer.

## 🔁 Large Changing Customer Dimensions

Khách hàng có thể thay đổi địa chỉ, email, trạng thái, nhóm... rất thường xuyên:

* Sử dụng **Slowly Changing Dimension Type 2 (SCD Type 2)** để lưu lịch sử
* Với khối lượng lớn, cần kiểm soát update performance và index tốt

### 🔍 Type 2 Implications

* Một khách hàng có thể có nhiều dòng
* Phải dùng surrogate key để join với fact
* Phải xác định rõ dòng "active"

## 👥 Customer Behavior Study Groups

Tạo các nhóm phân tích hành vi như:

* Nhóm khách có nguy cơ rời bỏ (churn)
* Nhóm khách VIP
* Nhóm phản hồi tích cực với khuyến mãi

Những nhóm này có thể lưu ở bảng dimension phân loại hoặc bảng fact hành vi tùy mục đích.

## 🏢 Commercial Customer Hierarchies

Với khách hàng doanh nghiệp:

* Một công ty có thể có nhiều chi nhánh
* Mỗi chi nhánh có nhiều điểm giao dịch

→ Mô hình hóa quan hệ phân cấp bằng **bridge table** hoặc **recursive hierarchy**.

## 🔗 Kết hợp nhiều nguồn dữ liệu khách hàng

Khách hàng có thể tồn tại trong nhiều hệ thống (CRM, Loyalty, E-commerce...)

* Cần chuẩn hóa và hợp nhất thông tin theo business key hoặc email/số điện thoại
* Có thể dùng **mapping table** để theo dõi ID tương ứng giữa các hệ thống

## 🔄 Phân tích dữ liệu khách hàng từ nhiều quy trình

Customer dimension thường là conformed dimension:

* Kết nối với fact bán hàng, chăm sóc khách hàng, phản hồi, loyalty
* Giúp "drill across" giữa các data mart

📌 Nên duy trì customer dimension với surrogate key chung và logic SCD nhất quán.

## 📌 Tóm tắt chương

* CRM bao gồm cả nghiệp vụ và phân tích
* Customer dimension là trung tâm phân tích khách hàng
* Áp dụng SCD Type 2 cho thuộc tính thay đổi
* Dùng dimension phụ (outrigger) cho nhóm thuộc tính phụ
* Kết hợp nhiều nguồn dữ liệu bằng chuẩn hóa và mapping
* Hỗ trợ phân tích hành vi, phân khúc, và cấu trúc khách hàng doanh nghiệp
