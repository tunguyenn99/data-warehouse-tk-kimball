# 🛒 Chương 14: Thương mại điện tử (Electronic Commerce)

## 🌐 Web Client-Server Interactions Tutorial

* Trình bày cách thức hoạt động cơ bản giữa trình duyệt người dùng và máy chủ web
* Mỗi lần tải trang, click, tương tác đều được ghi lại và tạo thành **clickstream**
* Mỗi phiên (session) bao gồm chuỗi các sự kiện theo thứ tự thời gian

---

## 🚦 Clickstream không chỉ là một nguồn dữ liệu khác

* Dữ liệu clickstream chứa **hành vi người dùng trực tiếp** trên website
* Không giống transactional data thông thường:

  * Thời gian và chuỗi hành động rất quan trọng
  * Dữ liệu không đồng nhất và có thể không hoàn chỉnh

---

## ⚠️ Thách thức khi xử lý dữ liệu clickstream

* Phiên không xác định rõ (sessionization khó)
* Dữ liệu có thể bị thiếu, rời rạc, thứ tự không đảm bảo
* Không phải sự kiện nào cũng dẫn đến giao dịch
* Thiếu thông tin định danh người dùng (ẩn danh, cookie, đăng nhập không bắt buộc)

---

## 🧩 Các dimension đặc thù trong clickstream

* 🧑 Người dùng / Tài khoản
* 💻 Trình duyệt, thiết bị, hệ điều hành
* 🌍 Địa chỉ IP, vị trí địa lý
* 📆 Ngày, giờ, khung thời gian truy cập
* 🧭 Trang (page), loại nội dung, luồng điều hướng

---

## 🗂️ Clickstream Fact Table: Mô hình toàn phiên

* Mỗi dòng đại diện cho một phiên duy nhất
* Dimension:

  * Người dùng, trình duyệt, quốc gia, ngày...
* Fact:

  * Số trang xem, thời lượng, lượt click, lượt thoát

---

## 🧾 Clickstream Fact Table: Mô hình từng sự kiện

* Mỗi dòng là một sự kiện (mở trang, click, cuộn chuột...)
* Phù hợp cho phân tích hành vi chi tiết, cá nhân hoá
* Cần xác định session ID để nhóm theo người dùng

---

## 📊 Aggregate Clickstream Fact Tables

* Tổng hợp hành vi theo ngày, người dùng, loại nội dung...
* Phục vụ dashboard nhanh, không cần quét raw event

---

## 🏗️ Tích hợp với Enterprise Data Warehouse

* Clickstream được đưa vào data mart riêng → tích hợp qua dimension conformed
* Cho phép phân tích:

  * Truy cập web vs giao dịch mua hàng
  * Phễu chuyển đổi (conversion funnel)
  * Hiệu quả landing page, chiến dịch tiếp thị

---

## 💰 Electronic Commerce Profitability Data Mart

* Kết hợp dữ liệu:

  * Clickstream
  * Đơn hàng, thanh toán, lợi nhuận
* Cho phép phân tích hiệu quả:

  * Chi phí thu hút khách hàng (CAC)
  * Doanh thu theo kênh
  * Tỷ lệ lợi nhuận sau cùng

---

## 📌 Tóm tắt chương

* Clickstream giúp hiểu rõ hành vi khách hàng online
* Có thể model theo phiên hoặc theo từng sự kiện
* Tích hợp clickstream với transactional data để phân tích toàn diện
* Thương mại điện tử cần data mart chuyên biệt để đo hiệu quả, lợi nhuận và hành trình khách hàng
