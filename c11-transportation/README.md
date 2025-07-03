# ✈️ Chương 11: Vận tải (Transportation)

## 🧳 Airline Frequent Flyer Case Study

Chương này trình bày mô hình hóa dữ liệu trong ngành vận tải, đặc biệt là hàng không. Dữ liệu liên quan đến hành trình, chuyến bay, dịch vụ khách hàng thân thiết (frequent flyer), vận chuyển hàng hóa, và các đặc điểm thời gian phức tạp.

---

## 📊 Multiple Fact Table Granularities

* Hệ thống có thể cần nhiều grain:

  * Mỗi lần đặt vé
  * Mỗi phân đoạn chuyến bay (flight segment)
  * Mỗi hành trình đầy đủ (trip)
* Mỗi bảng fact sẽ có mục tiêu và ứng dụng riêng:

  * Phân tích hiệu suất hành trình
  * Theo dõi lộ trình hành khách
  * Tối ưu hoá logistics hoặc tiếp thị

---

## 🔗 Linking Segments into Trips

* Một chuyến đi (trip) có thể bao gồm nhiều đoạn bay (segment):

  * Ví dụ: HAN → SIN → LAX
* Cần bảng bridge hoặc định danh chung để liên kết các segment thành 1 trip
* Phân tích theo trip giúp đo:

  * Tổng thời gian hành trình
  * Tổng chi tiêu
  * Số điểm tích lũy, v.v.

---

## 🔁 Extensions to Other Industries

### 🚚 Cargo Shipper

* Ghi nhận các lần vận chuyển hàng:

  * Ngày gửi, ngày đến, trạng thái
  * Khối lượng, loại hàng, phương thức vận chuyển

### 🧳 Travel Services

* Quản lý các dịch vụ du lịch:

  * Tour, đặt phòng khách sạn, thuê xe, vé vào cổng...
  * Mỗi dịch vụ là một phân đoạn (segment) của hành trình

---

## 🧱 Combining Small Dimensions into a Superdimension

* Với các dimension nhỏ, ít thay đổi (loại vé, loại hành khách, hình thức thanh toán...)
* Có thể gộp vào một superdimension (dimension tổng hợp) để đơn giản hóa schema

---

## 🛫 Class of Service

* Hạng vé: economy, business, first class...
* Có thể model là một dimension riêng để phân tích:

  * Chi tiêu theo hạng vé
  * Hiệu suất bán vé theo phân khúc

---

## 🌐 Origin and Destination

* Cần model rõ ràng các điểm xuất phát và đến:

  * Có thể là một dimension (sân bay)
  * Hoặc tạo dimension riêng cho origin và destination nếu cần join linh hoạt

---

## 🗓️ More Date and Time Considerations

### 🗓️ Country-Specific Calendars

* Một số quốc gia dùng lịch riêng (âm lịch, lịch tài khóa...)
* Cần chuẩn hóa hoặc thêm các trường quy chiếu

### 🕒 Time of Day as a Dimension or Fact

* Phân tích hoạt động theo giờ trong ngày:

  * Lưu như một dimension (giờ, ca làm việc...)
  * Hoặc là field trong bảng fact (timestamp, time bucket)

### 🌍 Date and Time in Multiple Time Zones

* Đặc biệt quan trọng với hàng không:

  * Bay qua múi giờ khác
  * Cần lưu giờ địa phương + giờ UTC
  * Hoặc thêm dimension "time zone"

---

## 📌 Tóm tắt chương

* Hành trình vận tải phức tạp → cần nhiều grain fact table
* Liên kết các phân đoạn thành hành trình để phân tích end-to-end
* Áp dụng cho nhiều ngành: hàng không, logistics, du lịch
* Dùng superdimension để gom các dimension nhỏ
* Xử lý ngày giờ: múi giờ, lịch đặc biệt, giờ trong ngày
* Tối ưu mô hình để hỗ trợ phân tích khách hàng, hiệu suất chuyến bay và chi tiêu
