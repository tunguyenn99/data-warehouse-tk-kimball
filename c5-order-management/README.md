# 📦 Chương 5: Quản lý Đơn hàng (Order Management)

## 🔰 Giới thiệu về Quản lý Đơn hàng

Chương này mô hình hóa toàn bộ quy trình quản lý đơn hàng – từ lúc khách hàng đặt hàng đến khi đơn được hoàn tất và thanh toán. Quản lý đơn hàng là một chuỗi các sự kiện phức tạp liên quan đến nhiều trạng thái, nhiều điểm tiếp xúc dữ liệu và cần mô hình hóa cẩn thận để phân tích.

---

## 🧾 Order Transactions

Mỗi đơn hàng bao gồm:

* Header (thông tin chung)
* Line items (các dòng sản phẩm cụ thể)

Một đơn hàng có thể:

* Được chỉnh sửa nhiều lần
* Giao thành nhiều đợt
* Thanh toán bằng nhiều hình thức

\=> Cần mô hình hóa kỹ transaction grain và xử lý sự thay đổi theo thời gian.

### 🧱 Fact Normalization

Tách bảng fact theo chủ đề:

* Order Header Fact (một dòng mỗi đơn hàng)
* Order Line Fact (một dòng mỗi sản phẩm trong đơn)

### 🎭 Dimension Role-Playing

Dùng lại dimension ngày nhiều lần trong cùng một fact:

* Ngày đặt hàng
* Ngày giao hàng dự kiến
* Ngày giao hàng thực tế

### 🧩 Product Dimension mở rộng

* Bao gồm cấu trúc sản phẩm đầy đủ: nhóm, dòng, phiên bản, size, SKU
* Thêm thông tin định giá, trạng thái hoạt động

### 🏠 Customer Ship-To Dimension

Tách riêng địa chỉ giao hàng (ship-to) với khách hàng (bill-to) vì một khách hàng có thể có nhiều địa chỉ nhận hàng.

### 🤝 Deal Dimension

Lưu thông tin chương trình khuyến mãi, chính sách giảm giá hoặc thỏa thuận đặc biệt đi kèm đơn hàng.

### 🧾 Degenerate Dimension

Order Number thường là một dạng **degenerate dimension**: tồn tại trong fact table nhưng không cần bảng riêng.

### 🧺 Junk Dimensions

Gom các cờ logic (flag) không liên quan trực tiếp đến một dimension nào, như:

* Cờ ưu tiên
* Đơn hàng khẩn cấp
* Giao hàng miễn phí

### 💱 Nhiều đơn vị tiền tệ

* Lưu cả tiền bản địa và quy đổi (standard currency)
* Dùng thêm dimension “currency” và tỷ giá thời điểm đặt hàng

---

## 🧮 Sự khác biệt về granularity

### 🧾 Header và Line Item Facts

* Header: thông tin tổng hợp đơn hàng
* Line Item: chi tiết từng sản phẩm

### 📄 Invoice Transactions

* Có thể xuất hóa đơn nhiều lần từ một đơn hàng
* Mỗi hóa đơn có thể bao gồm nhiều đơn hàng → cần fact riêng hoặc liên kết nhiều-nhiều

### 💰 Profit and Loss Facts

* Ghi nhận chi phí và lợi nhuận từng đơn hàng hoặc từng dòng sản phẩm
* Kết hợp nhiều bảng fact với grain khác nhau

### 🔎 Customer Satisfaction Facts

* Ghi nhận feedback, survey, complaint liên quan đến đơn hàng
* Có thể gắn vào Order ID hoặc Customer ID

---

## 🔄 Accumulating Snapshot cho Pipeline Đơn hàng

Sử dụng mô hình **Accumulating Snapshot Fact** để mô tả vòng đời đơn hàng:

* Đặt hàng
* Giao hàng
* Thanh toán
* Hóa đơn

📌 Mỗi dòng trong fact đại diện cho một đơn hàng, được cập nhật theo thời gian với các mốc thời gian được điền dần.

### ⌛ Lag Calculations

* Dễ dàng tính độ trễ giữa các mốc: đặt → giao, giao → thanh toán...

### 📏 Multiple Units of Measure

* Ghi nhận cả đơn vị cơ bản (số lượng) và phụ (trọng lượng, thể tích...)

---

## 🔮 Beyond the Rear-View Mirror

Chương này không chỉ mô hình hóa quá khứ, mà còn hỗ trợ dự báo:

* Số đơn đang chờ xử lý
* Dự đoán tỷ lệ giao đúng hạn
* Hiệu suất xử lý đơn theo từng bước

---

## ⚖️ So sánh các loại Fact Table

| Loại                  | Mục đích chính               | Ví dụ Grain             |
| --------------------- | ---------------------------- | ----------------------- |
| Transaction           | Ghi nhận mỗi hành vi/sự kiện | Mỗi đơn hoặc dòng       |
| Periodic Snapshot     | Tình trạng định kỳ           | Tồn kho theo ngày       |
| Accumulating Snapshot | Diễn tiến vòng đời           | Đơn hàng theo thời gian |

---

## ⚙️ Thiết kế Real-Time Partition

### 🧩 Yêu cầu

* Cho phép xử lý giao dịch đang diễn ra
* Kết hợp dữ liệu realtime và batch

### 🧾 Transaction Grain Realtime Partition

* Mỗi dòng là một hành động mới nhất
* Dùng cho hệ thống cập nhật liên tục

### 🗓️ Periodic Snapshot Realtime

* Ghi nhận trạng thái đơn hàng mới nhất theo giờ/ngày

### 🔄 Accumulating Snapshot Realtime

* Cập nhật các mốc tiến độ khi đơn thay đổi trạng thái

---

## 📌 Tổng kết chương

* Mô hình quản lý đơn hàng rất linh hoạt, cần xử lý nhiều loại grain và thời gian
* Áp dụng degenerate, junk, role-playing dimension hiệu quả
* Kết hợp các loại fact để phân tích hiệu suất đơn hàng và lợi nhuận
* Sử dụng accumulating snapshot để theo dõi vòng đời
* Thiết kế real-time partition để hỗ trợ phân tích thời gian thực