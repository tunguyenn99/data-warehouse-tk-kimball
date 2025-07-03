# 📑 Chương 4: Mua hàng (Procurement) – The Data Warehouse Toolkit 🇻🇳

## 📦 Procurement Case Study

Trong chương này, chúng ta tiếp tục chuỗi giá trị từ bán hàng và tồn kho đến hoạt động mua hàng (procurement). Quy trình này liên quan đến việc mua sản phẩm từ các nhà cung cấp để lấp đầy hàng hóa trong kho và đảm bảo chuỗi cung ứng luôn hoạt động trơn tru.

Ví dụ, một nhà bán lẻ có thể thực hiện đơn đặt hàng từ nhiều nhà cung cấp, nhận hàng tại kho trung tâm, và sau đó phân phối về các cửa hàng chi nhánh.

Chúng ta sẽ xây dựng các bảng fact để lưu trữ chi tiết giao dịch mua hàng, cùng với các dimension liên quan như sản phẩm, nhà cung cấp, địa điểm, thời gian, trạng thái đơn hàng, v.v.

## 🔄 Procurement Transactions

Một bảng fact giao dịch mua hàng sẽ ghi lại từng hành động liên quan đến đơn đặt hàng: tạo đơn, xác nhận, giao hàng, nhận hàng, trả hàng, v.v. Mỗi dòng trong bảng thể hiện một giao dịch cụ thể với các chiều đi kèm:

* Thời gian giao dịch
* Mã đơn hàng
* Sản phẩm
* Vendor
* Trạng thái đơn hàng
* Địa điểm kho
* Nhân viên thực hiện

Các chỉ số fact có thể bao gồm:

* Số lượng đặt hàng
* Số lượng đã giao
* Giá trị giao dịch (giá trị hàng hóa)

## ⚖️ Multiple vs. Single Transaction Fact Tables

Có hai cách để thiết kế bảng fact cho đơn hàng:

1. **Multiple-transaction table**: Mỗi dòng là một giao dịch cụ thể (ví dụ: tạo đơn, nhận hàng, trả hàng). Tốt để truy vết lịch sử chi tiết, nhưng dữ liệu phân mảnh.

2. **Single-transaction table**: Mỗi dòng là toàn bộ đơn hàng, cập nhật dần theo các mốc sự kiện (giao hàng, nhận, hoàn tất). Tốt cho báo cáo tổng hợp, nhưng khó ghi nhận chi tiết.

Lý tưởng nhất là kết hợp cả hai mô hình để phục vụ cho cả phân tích chi tiết và tổng quan.

## 📸 Complementary Procurement Snapshot

Bên cạnh bảng fact giao dịch, chúng ta có thể tạo snapshot định kỳ (ví dụ hàng ngày) để ghi nhận trạng thái của các đơn đặt hàng:

* Đơn nào đang chờ giao
* Đơn nào đã giao một phần
* Đơn nào bị trả lại hoặc huỷ

Snapshot giúp đo lường hiệu suất thực hiện đơn hàng, tỷ lệ giao đúng hẹn, thời gian chờ trung bình,...

## 🐢 Slowly Changing Dimensions (SCD)

Trong thế giới thực, thông tin trong dimension sẽ thay đổi theo thời gian. Chúng ta cần kỹ thuật **Slowly Changing Dimensions** để quản lý các thay đổi này.

### 🧊 Type 1 – Overwrite the Value

Loại đơn giản nhất: khi dimension thay đổi, ta ghi đè giá trị cũ bằng giá trị mới. Không giữ lịch sử. Phù hợp khi sai sót dữ liệu cần sửa.

### 📘 Type 2 – Add a Dimension Row

Tạo một dòng mới cho mỗi lần dimension thay đổi. Ví dụ: nếu vendor đổi địa chỉ, một dòng mới với địa chỉ mới sẽ được thêm vào dimension.

* Cần có surrogate key để phân biệt dòng
* Bảng fact liên kết tới đúng dòng dimension theo thời điểm

### 🗃️ Type 3 – Add a Dimension Column

Lưu cả giá trị hiện tại và giá trị trước đó trong cùng một dòng. Phù hợp khi chỉ cần lưu một lần thay đổi gần nhất.

## 🧬 Hybrid SCD & Predictable Changes

### 🧬 Hybrid Techniques

Kết hợp nhiều kỹ thuật SCD trong cùng một dimension:

* Type 1 cho cột A (ghi đè)
* Type 2 cho cột B (lưu lịch sử)
* Type 3 cho cột C (trước và sau thay đổi)

### 🔁 Predictable Changes with Overlays

Với các thay đổi có thể dự đoán trước (ví dụ: thay đổi mức chiết khấu theo quý), ta có thể tạo sẵn nhiều dòng dimension tương ứng, và ánh xạ theo thời gian có hiệu lực.

### 🎲 Unpredictable Changes

Với thay đổi bất ngờ, chỉ nên giữ một phiên bản hiện tại. Có thể tạo bảng lookup phụ hoặc sử dụng version flag.

## ⚡️ More Rapidly Changing Dimensions

Một số chiều như trạng thái tài khoản, địa chỉ giao hàng, giá thị trường… thay đổi quá thường xuyên.

Chiến lược:

* Không đưa vào dimension mà để trong bảng fact
* Hoặc lưu ở bảng phụ, chỉ liên kết khi cần thiết để giảm tải dữ liệu chính

## 📌 Summary

* Thiết kế bảng fact mua hàng giúp theo dõi hiệu quả chuỗi cung ứng
* Kết hợp giao dịch và snapshot để phân tích toàn diện
* Làm chủ kỹ thuật SCD (Type 1/2/3 + hybrid)
* Cân nhắc khi xử lý dimension thay đổi nhanh (rapid change)
* Mô hình hóa linh hoạt giúp kho dữ liệu thích nghi tốt với thực tế
