# 🏦 Chương 2 – Bán lẻ (Retail Sales)

## 🔄 Giới thiệu

Chương 2 sử dụng bài toán bán lẻ trong ngành bán lẻ tại các siêu thị/grocery store như một ví dụ điển hình để giải thích nguyên lý thiết kế mô hình dimensional. Việc hiểu được quy trình thiết kế qua bài toán thực tiễn sẽ hiệu quả hơn so với lý thuyết suông.

Dù bạn không làm trong ngành bán lẻ, chương này vẫn mang lại nhiều kỹ thuật áp dụng được cho hầu hết mọi ngành nghề: bảo hiểm, ngân hàng, viễn thông, hàng không,...

---

## 🔹 Các nội dung chính của chương
- Quy trình 4 bước để thiết kế mô hình dữ liệu chiều  
- Bảng fact ở cấp độ giao dịch  
- Fact cộng được và không cộng được  
- Các thuộc tính mẫu của bảng dimension  
- Dimension nguyên nhân (causal), ví dụ như khuyến mãi  
- Dimension suy biến (degenerate), ví dụ số hiệu giao dịch  
- Mở rộng mô hình dimension hiện có  
- Snowflake hóa các thuộc tính dimension  
- Tránh bẫy “quá nhiều dimension”  
- Sử dụng surrogate key  
- Phân tích giỏ hàng (Market Basket Analysis)  

---

## 🧭 1. Quy trình 4 bước thiết kế mô hình dữ liệu chiều

### 🟢 Bước 1: Chọn quy trình nghiệp vụ để mô hình hoá  
Một quy trình là một hoạt động kinh doanh tự nhiên trong tổ chức, thường được hỗ trợ bởi hệ thống thu thập dữ liệu. Cách hiệu quả nhất để xác định quy trình nghiệp vụ là **lắng nghe người dùng** — các chỉ số mà họ mong muốn phân tích chính là kết quả từ các hoạt động kinh doanh đó. Ví dụ về quy trình gồm có: mua nguyên liệu, đơn đặt hàng, giao hàng, lập hóa đơn, kiểm kê, và sổ cái.

Điều quan trọng là **quy trình nghiệp vụ không tương đương với phòng ban** trong tổ chức. Ví dụ, thay vì xây hai mô hình khác nhau cho phòng Kinh doanh và Marketing khi cả hai đều cần dữ liệu về đơn hàng, ta chỉ nên xây một mô hình dimension duy nhất cho **dữ liệu đơn hàng**. Việc tập trung vào quy trình thay vì phòng ban giúp đảm bảo thông tin nhất quán và tiết kiệm chi phí xây dựng kho dữ liệu. Nếu mỗi phòng ban có mô hình riêng, ta sẽ dễ gặp lỗi **trùng lặp dữ liệu** với tên gọi và logic khác nhau.

👉 Xuất bản dữ liệu **một lần duy nhất** là cách tốt nhất để đảm bảo tính nhất quán. Ngoài ra, việc trích xuất – biến đổi – tải (ETL) cũng đơn giản và tiết kiệm tài nguyên lưu trữ hơn.

---

_Các phần tiếp theo sẽ tiếp tục được cập nhật theo từng bước dịch._


### 🟡 Bước 2: Xác định mức độ chi tiết (Grain)

Sau khi đã chọn được quy trình nghiệp vụ, nhóm xây dựng kho dữ liệu cần ra quyết định quan trọng về **độ chi tiết của dữ liệu**. Đây là bước cực kỳ quan trọng:

> **Nên xây dựng mô hình dữ liệu chiều ở mức chi tiết nhỏ nhất (atomic grain) mà quy trình nghiệp vụ thu thập được.**

Dữ liệu ở mức atomic không thể phân rã thêm và thường mang lại **nhiều chiều (dimension)** hơn, đồng thời giúp phân tích linh hoạt hơn. Ví dụ về grain:

- Mỗi dòng hàng trên hóa đơn bán lẻ
- Mỗi dòng trong hoá đơn bệnh viện
- Mỗi thẻ lên máy bay
- Snapshot tồn kho hàng ngày
- Snapshot tài khoản ngân hàng theo tháng

✅ Việc tuyên bố grain giúp định hướng toàn bộ thiết kế. Nếu tuyên bố sai, bạn có thể phải quay lại bước 2 và điều chỉnh.

Trong case bán lẻ, grain chính xác là **mỗi dòng hàng trong giao dịch POS**. Trước đây, người ta thường chọn grain ở mức tổng hợp theo ngày/cửa hàng/sản phẩm, vì hạn chế về phần cứng. Nhưng ngày nay, lưu trữ dữ liệu giao dịch chi tiết trở nên khả thi và rất cần thiết cho các câu hỏi phân tích sâu, ví dụ:

- Bao nhiêu người mua dầu gội khi có khuyến mãi 50%?
- So sánh doanh số bán hàng ngày Chủ Nhật và Thứ Hai
- Có nên tiếp tục bày bán đủ size ngũ cốc?

### 🟠 Bước 3: Chọn các chiều dữ liệu (Dimensions)

Sau khi xác định grain, các chiều chính sẽ xuất hiện rõ ràng: **ngày**, **sản phẩm**, **cửa hàng**, và **khuyến mãi**. Ngoài ra, còn có thể thêm số hiệu giao dịch POS như một chiều suy biến (degenerate dimension).

> Một grain được xác định rõ ràng sẽ kéo theo các chiều chính xác cho bảng fact.

Điều quan trọng là mỗi chiều bổ sung **phải có duy nhất một giá trị cho mỗi dòng fact**. Nếu một chiều mới khiến phát sinh nhiều dòng fact, thì cần xem lại grain.

### 🔴 Bước 4: Xác định các chỉ số định lượng (Facts)

Facts là những gì doanh nghiệp muốn đo lường: **số lượng bán**, **giá**, **doanh thu**, **chi phí**, **lợi nhuận gộp**. Những chỉ số này cần **phù hợp với grain** đã chọn. Ví dụ:

- `sales_quantity`: số lượng bán
- `sales_amount`: doanh thu (số lượng × giá)
- `cost_amount`: giá vốn
- `gross_profit`: doanh thu – giá vốn

> Các chỉ số như `gross_profit` là **cộng được** và nên được lưu trữ sẵn thay vì tính toán động để tránh lỗi người dùng.

Những chỉ số **không cộng được** (non-additive), như `gross_margin = gross_profit / revenue` hay `unit_price`, nên được tính trong báo cáo, chứ không nên cộng thẳng trong bảng fact.

---

_Các phần tiếp theo như chi tiết các bảng dimension, dimension suy biến, xử lý khuyến mãi, phân tích giỏ hàng, v.v. sẽ tiếp tục bên dưới._


---

## 🧱 2. Các bảng Dimension và thuộc tính chi tiết

### 📅 Dimension Ngày (Date Dimension)

Dimension Ngày là dimension phổ biến nhất vì hầu hết mọi data mart đều là chuỗi thời gian. Ta nên tạo trước bảng này, có thể chứa dữ liệu cho 5–10 năm. Một số thuộc tính hữu ích:

- Tên ngày (Thứ Hai, Thứ Ba…)
- Ngày trong tháng, tháng trong năm, quý, năm
- Chỉ báo ngày lễ (Holiday / Non-Holiday)
- Chỉ báo ngày trong tuần (Weekday / Weekend)
- Mùa bán hàng, sự kiện đặc biệt (Noel, Tết…)
- Mốc thời gian tài chính (Fiscal periods)

> SQL không hỗ trợ tốt các truy vấn theo ngày lễ, mùa vụ, v.v. nên ta cần lưu rõ ràng trong bảng dimension.  
> Định dạng `Date Key` nên là số nguyên (integer surrogate key), không phải kiểu `DATE`.

### 🛒 Dimension Sản phẩm (Product Dimension)

Mỗi SKU (Stock Keeping Unit) có nhiều thuộc tính mô tả như:

- Tên sản phẩm, số SKU, mô tả thương hiệu
- Danh mục (Category), phòng ban (Department)
- Loại bao bì, kích thước, trọng lượng, chất béo (fat content), loại thực phẩm ăn kiêng (diet type)

> Một bảng dimension sản phẩm tốt nên có ít nhất 50 thuộc tính mô tả. Drilling-down chỉ là việc **thêm các cột dimension vào báo cáo**.

### 🏬 Dimension Cửa hàng (Store Dimension)

Mô tả từng cửa hàng trong chuỗi bán lẻ, gồm:

- Địa chỉ, mã zip, thành phố, bang
- Khu vực quản lý (district, region)
- Diện tích bán hàng, ngày khai trương, ngày nâng cấp
- Kiểu mặt bằng, dịch vụ đi kèm như xử lý ảnh, dịch vụ tài chính

Có thể tạo các "outrigger" view để kết nối ngày mở cửa với bảng date dimension.

### 🎯 Dimension Khuyến mãi (Promotion Dimension)

Là **dimension nhân quả (causal dimension)**, dùng để đánh giá hiệu quả khuyến mãi:

- Các loại giảm giá (discount type), quảng cáo, trưng bày, phiếu giảm giá
- Ngày bắt đầu / kết thúc khuyến mãi
- Chi phí thực hiện

✅ Có thể lưu các biến khuyến mãi trong một bảng tổng hợp hoặc tách ra từng bảng riêng, tùy vào cách tổ chức dữ liệu.

> Luôn cần một dòng "Không có khuyến mãi" để tránh NULL key trong bảng fact.

---

## 🛠️ 3. Các kỹ thuật đặc biệt

### 📉 Bảng fact không số liệu (Factless Fact Table)

Để biết **sản phẩm nào được khuyến mãi nhưng không bán được**, ta cần bảng riêng ghi nhận các SKU nằm trong chương trình khuyến mãi, bất kể có bán hay không.  
Đây là bảng fact không chứa chỉ số (factless fact), chỉ lưu quan hệ giữa `date`, `product`, `store`, `promotion`.

### 🧩 Dimension suy biến (Degenerate Dimension)

Ví dụ như số hóa đơn POS. Dù không có bảng dimension đi kèm, các mã đơn hàng vẫn là khóa chính trong bảng fact. Các dimension như vậy gọi là **degenerate dimensions**.

### 🧬 Mở rộng schema

Khi doanh nghiệp có thêm **chương trình khách hàng thân thiết (frequent shopper)**, ta chỉ cần thêm dimension `shopper` và khóa ngoại tương ứng vào bảng fact.

Tương tự, có thể thêm dimension cho **thời gian trong ngày** hoặc **nhân viên thu ngân (clerk)** nếu thông tin đó có sẵn và có duy nhất một giá trị tại grain của bảng fact.

---

## 🚀 4. Các nguyên tắc nâng cao

### ❄️ Tránh snowflake hoá dimension

Dù việc tách các dimension như department hay category thành bảng riêng giúp tiết kiệm bộ nhớ, nhưng:

- Làm **phức tạp hoá schema**
- Giảm hiệu năng khi join
- Gây khó khăn khi duyệt dữ liệu (browsing)
- Không tận dụng được **bitmap index**

✅ Hạn chế snowflake hóa trừ khi thật cần thiết.

### 🐛 Tránh quá nhiều dimension

Nếu có trên 25 dimension, nên:

- Gộp các dimension có mối quan hệ chặt chẽ (vd: category và department)
- Tránh thêm các dimension trùng lặp theo hierarchy

> Một thiết kế tốt thường có dưới 15 dimension.

### 🔑 Sử dụng surrogate key

Không nên dùng mã nghiệp vụ làm khóa chính trong dimension:

- Dễ bị thay đổi, tái sử dụng, trùng lặp
- Dài dòng, khó join
- Khó xử lý dữ liệu chưa xác định (vd: ngày chưa xảy ra)

> Khóa surrogate nên là integer tự tăng, giúp giảm dung lượng bảng fact và hỗ trợ xử lý Slowly Changing Dimensions.

---

## 🛍️ 5. Phân tích giỏ hàng (Market Basket Analysis)

Schema bán lẻ tuy chi tiết nhưng không dễ để trả lời câu hỏi **sản phẩm nào thường được mua cùng nhau**. Đó là nhiệm vụ của Market Basket Analysis.

Cần xây dựng bảng fact riêng, ghi nhận:

- Cặp sản phẩm A và B
- Số lần mua chung (basket count)
- Tổng số lượng và doanh thu từng sản phẩm trong cặp

Do số lượng kết hợp sản phẩm rất lớn (`N x (N-1)`), nên cần dùng kỹ thuật **pruning top-down**:

1. Bắt đầu từ cấp cao nhất (category)
2. Lọc những cặp có tần suất cao và cân bằng
3. Drill-down dần xuống brand, SKU…

✅ Phân tích này thường được thực hiện trong bước ETL trước khi truy vấn.

---

## 🧾 6. Tổng kết chương

- Tuân theo **quy trình 4 bước** để thiết kế mô hình chiều
- Phải xác định rõ **grain** — càng chi tiết càng linh hoạt
- Bảng dimension nên đầy đủ thuộc tính mô tả
- Tránh **snowflake**, **quá nhiều dimension**, **khóa thông minh**
- Dùng **surrogate key** và có thể mở rộng schema khi cần
- Áp dụng các bảng factless, phân tích giỏ hàng khi cần phân tích nâng cao

Chương tiếp theo sẽ mở rộng trong ngành bán lẻ với một quy trình nghiệp vụ thứ hai, đồng thời đảm bảo **tái sử dụng dimension hiện có và tránh tạo silo dữ liệu.**
