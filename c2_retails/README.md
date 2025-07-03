# 🏦 Chapter 2: Doanh thu Bán lẻ (Retail Sales)

## 🔄 Giới thiệu

Chương 2 sử dụng bài toán bán lẻ trong ngành bán lẻ tại các siêu thị/grocery store như một ví dụ điển hình để giải thích nguyên lý thiết kế mô hình dimensional. Việc hiểu được quy trình thiết kế qua bài toán thực tiễn sẽ hiệu quả hơn so với lý thuyết trẫn trùng.

Dù bạn không làm trong ngành bán lẻ, chương này vẫn mang lại nhiều kỹ thuật áp dụng được cho hầu hết mọi ngành nghề: bảo hiểm, ngân hàng, viễn thông, hàng không,...

---

## ✅ Bốn bước thiết kế Dimensional Model

1. **Chọn business process** để model: trong trường hợp này là POS Retail Sales (ghi nhận giao dịch tại quầy thu ngân)
2. **Xác định grain (cấp độ chi tiết)**: mỗi dòng trong fact table tương ứng với 1 sản phẩm được quét trong giao dịch POS
3. **Chọn Dimensions**: các thuộc tính mô tả giao dịch, vd: Date, Product, Store, Promotion, POS Ticket Number
4. **Xác định Facts**: Sales Quantity, Sales Amount, Cost, Gross Profit, ... (phải tôn trọng grain đã tuyên bố)

---

## 📊 Thiết kế Data Model cho POS Retail Sales

* Grain: 1 giao dịch line-item (mỗi sản phẩm được bán)
* Dimensions:

  * `Date Dimension`: chứa các thông tin về ngày như dạng chữ, weekday/weekend, tháng, năm, kỳ nghỉ...
  * `Product Dimension`: danh sách sản phẩm/SKU, gồm hierarchy Brand - Category - Department và các thuộc tính khác như Package, Fat Content...
  * `Store Dimension`: thông tin siêu thị (Store Name, City, Zip Code, District, Region, ...)
  * `Promotion Dimension`: mô tả các chương trình khuyến mãi (được coi là causal dimension)
  * `POS Transaction Number`: được lưu trong fact table như degenerate dimension
* Facts:

  * `Sales Quantity`
  * `Sales Dollar Amount`
  * `Cost Dollar Amount`
  * `Gross Profit Amount` (nên tính sẵn để tránh user tính sai)
  * Non-additive: `Unit Price`, `Gross Margin` (cần tính từ sum truớc khi chia)

---

## 🌐 Mở rộng schema với các dimension khác

Khi doanh nghiệp triển khai thêm các chương trình khách hàng thân thiết, ta có thể mở rộng schema bằng việc thêm:

* `Frequent Shopper Dimension`
* `Clerk Dimension` (nhân viên thu ngân)
* `Time of Day Dimension`

Vì grain vẫn là transaction line-item, việc bổ sung không ảnh hưởng đến schema cũ.

---

## 📲 Promotion Coverage Factless Fact Table

Câu hỏi: **"Sản phẩm nào được khuyến mãi nhưng không bán được?"**

* Sales Fact Table chỉ ghi những sản phẩm đã được bán
* Tạo Promotion Coverage Fact Table: ghi lại mỗi combination (Date, Product, Store, Promotion) dù số bán = 0
* Thực hiện set difference với Sales Fact để biết những gì KHôNG bán dù có khuyến mãi

---

## 📊 Market Basket Analysis

Phân tích những sản phẩm hay đi cùng giỏ hàng.

* Tạo fact table khác với grain = 1 cặp sản phẩm cùng xuất hiện trong giao dịch
* Sử dụng kỹ thuật Progressive Pruning (top-down theo hierarchy)
* Lưu ý các sản phẩm bán cùng phải đạt đặc điểm:

  * basket count cao
  * đồng đều về doanh thu/số lượng

---

## 🔹 Lời khuyên thiết kế

* **Tránh snowflaking** dimension (normalize lại dimension) vì:

  * Phức tạp, khó sử dụng, giảm performance
  * Tiết kiệm dung lượng không đáng kể
* **Tránh "too many dimensions"**: đây thường là dấu hiệu hierarchy bị bỏ rời hoặc bị tách ra quá nhiều
* **Sử dụng Surrogate Key**: integer key thay vì mã tự nhiên

  * Hạn chế tác động khi hệ thống nguồn thay đổi (mã thay đổi, reuse,...)
  * Tối ưu dụng lượng và performance
  * Cho phép xử lý Slowly Changing Dimensions (SCD)

---

## ✏️ Tổng kết

* Thiết kế dimensional theo 4 bước cố định.
* Sử dụng dữ liệu chi tiết nhất (atomic grain) để phục vụ truy vấn linh hoạt
* Dimension tables cần được làm phong phù với nhiều descriptive attributes
* Tránh normalize dimension và tránh quá nhiều dimension
* Triển khai Surrogate Key ngay từ đầu

Chương sau sẽ tiếp tục với ngành bán lẻ nhưng chọn business process khác để mở rộng và tái sử dụng dimension tối ưu.