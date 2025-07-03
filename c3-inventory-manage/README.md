# 📦 Chương 3: Quản lý Tồn kho (Inventory)

## 🔗 Giới thiệu và Chuỗi giá trị (Value Chain)

Trong Chương 2, chúng ta đã xây dựng mô hình dữ liệu dạng dimensional cho các giao dịch bán hàng tại một chuỗi siêu thị lớn. Trong chương này, chúng ta vẫn ở trong ngành bán lẻ nhưng tiến thêm một bước trong chuỗi giá trị để giải quyết bài toán tồn kho. Những thiết kế được trình bày không chỉ áp dụng trong ngành bán lẻ mà còn phù hợp với nhiều hệ thống quản lý tồn kho trong các ngành khác.

Quan trọng hơn, chương này giới thiệu chi tiết về **kiến trúc bus của kho dữ liệu (data warehouse bus architecture)** – một yếu tố thiết yếu để xây dựng kho dữ liệu tích hợp từ các quy trình kinh doanh phân tán. Chúng ta sẽ tìm hiểu cách sử dụng các **dimension và fact đồng nhất (conformed)** nhằm đảm bảo sự liên kết giữa các mô hình dimensional trong kho dữ liệu.

### 📚 Nội dung chính trong chương:

* 🧩 Ý nghĩa của chuỗi giá trị (value chain)
* 📊 Mô hình snapshot định kỳ cho tồn kho, mô hình giao dịch và mô hình snapshot tích lũy
* ➕ Các loại fact bán phần cộng (semi-additive facts)
* 📈 Fact nâng cao trong tồn kho
* 🚌 Kiến trúc bus và ma trận bus
* 🧱 Dimension và fact đồng nhất

### 🏭 Chuỗi giá trị trong tổ chức

Hầu hết các tổ chức có một chuỗi giá trị bao gồm các quy trình kinh doanh cốt lõi. Ví dụ, với một nhà bán lẻ:

* 📝 Công ty phát hành đơn đặt hàng cho nhà sản xuất
* 🚚 Sản phẩm được giao đến kho và lưu trữ trong tồn kho
* 🏬 Từ kho, sản phẩm được chuyển đến từng cửa hàng
* 🛒 Tại cửa hàng, sản phẩm tiếp tục được giữ trong tồn kho cho đến khi khách hàng mua

Ở mỗi bước, hệ thống nghiệp vụ sẽ tạo ra các giao dịch hoặc snapshot, từ đó sinh ra những chỉ số đo lường hiệu suất. Mỗi quy trình sinh ra các chỉ số riêng biệt với các cấp độ thời gian, độ chi tiết và chiều dữ liệu khác nhau, do đó thường cần các bảng fact riêng biệt. Việc lập bản đồ toàn bộ chuỗi giá trị giúp định hình tổng thể kiến trúc kho dữ liệu doanh nghiệp.

## 🧮 Các mô hình tồn kho

### 🗓️ Mô hình snapshot định kỳ (Inventory Periodic Snapshot)

Đây là mô hình phổ biến nhất để theo dõi tồn kho. Mỗi ngày, hệ thống sẽ ghi lại số lượng tồn của mỗi sản phẩm tại mỗi địa điểm. Dữ liệu được lưu vào bảng fact snapshot với các chiều như `date`, `product`, `location`.

Ưu điểm:

* Cho phép phân tích nhanh tồn kho tại bất kỳ thời điểm nào.
* Có thể tính trung bình tồn kho theo tuần/tháng.

Nhược điểm:

* Lượng dữ liệu rất lớn do phải ghi toàn bộ mỗi ngày.

### ➕ Semi-additive facts (Fact bán phần cộng)

Các fact như `quantity_on_hand` không thể cộng dồn theo thời gian như doanh thu. Tuy nhiên, chúng có thể cộng theo product hoặc location.

Ví dụ xử lý:

* Tính tồn kho trung bình theo ngày bằng cách tính tổng và chia cho số ngày (không dùng AVG SQL trực tiếp).

### 📈 Mô hình snapshot nâng cao (Enhanced Inventory Snapshot)

Bổ sung thêm các chỉ số tài chính vào snapshot:

* `quantity_sold`
* `value_at_cost`
* `value_at_selling_price`

Từ đó tính được:

* **Turns** = `quantity_sold` / `average_quantity_on_hand`
* **Days’ Supply** = `quantity_on_hand` / (`quantity_sold` / số ngày)
* **GMROI** = (Doanh thu - Giá vốn) / Tồn kho trung bình

### 🔄 Mô hình giao dịch tồn kho (Inventory Transaction)

Ghi nhận từng thao tác thay đổi tồn kho:

* Nhập hàng, kiểm định, đóng gói, xuất kho, trả hàng, v.v.

Bảng fact bao gồm:

* Ngày, loại giao dịch, sản phẩm, kho, số lượng ảnh hưởng

Ưu điểm:

* Phân tích chi tiết theo từng hành động kho.
  Nhược điểm:
* Không thuận tiện để biết tồn kho tại một thời điểm.

### 📦 Mô hình snapshot tích lũy (Inventory Accumulating Snapshot)

Theo dõi toàn bộ vòng đời của một shipment từ lúc nhận đến khi xuất kho. Mỗi dòng trong fact table đại diện cho một shipment, được cập nhật theo thời gian khi shipment tiến triển qua các bước:

* Received → Inspected → Put Away → Picked → Shipped

Thích hợp cho các quy trình logistics có giai đoạn rõ ràng.

## 🚌 Kiến trúc Bus trong Kho Dữ liệu

### 🧠 Tầm quan trọng của kiến trúc Bus

Thay vì xây dựng một kho dữ liệu khổng lồ ngay từ đầu, hay tạo ra nhiều mart rời rạc không kết nối, giải pháp lý tưởng là kiến trúc **Data Warehouse Bus**:

* Chuẩn hóa các dimension dùng chung
* Cho phép mở rộng kho dữ liệu dễ dàng, triển khai theo từng nhóm quy trình kinh doanh

### 📐 Ma trận Bus (Bus Matrix)

Là bảng 2 chiều thể hiện:

* Các quy trình nghiệp vụ (Retail Sales, Inventory, Procurement...)
* Các dimension dùng chung (Date, Product, Store, Vendor...)

Ma trận giúp xác định đâu là dimension cần chia sẻ, từ đó giữ cấu trúc dữ liệu nhất quán.

## 🧱 Dimension và Fact Đồng Nhất (Conformed)

### 🧱 Dimension Đồng Nhất

Một dimension được coi là conformed nếu nó:

* Có định nghĩa, cấu trúc, nội dung giống nhau giữa các fact
* Cho phép dùng chung để phân tích giữa các data mart khác nhau

Có thể ở dạng:

* Gốc (granular)
* Tập con (subset) hoặc rút gọn chiều

### 🧾 Fact Đồng Nhất

Fact conformed đảm bảo:

* Định nghĩa, đơn vị đo lường và cách tính thống nhất
* Có thể dùng so sánh và kết hợp dữ liệu giữa các bảng fact khác nhau

Ví dụ:

* `total_sales_amount` ở các bảng phải cùng tính trên đơn giá \* số lượng, không được khác nhau giữa các mart.

## 📌 Tóm tắt chương

* ✅ Đã trình bày 3 mô hình tồn kho: snapshot định kỳ, giao dịch, tích lũy
* 🕒 Snapshot định kỳ phù hợp cho tồn kho dài hạn và liên tục
* 🔁 Snapshot tích lũy phù hợp với quy trình tồn kho có vòng đời
* 🧾 Giao dịch cung cấp chi tiết nhưng không phù hợp để phân tích tổng hợp
* 🏗️ Đặt nền móng cho kiến trúc bus và việc chia sẻ dimension giữa các data mart
* 💡 Nhấn mạnh tầm quan trọng của dimension và fact đồng nhất để tích hợp toàn bộ kho dữ liệu
