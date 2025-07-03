# 📘 Chapter 1: Tổng quan về Mô hình hướng chiều (Dimensional Modeling Primer)

## 🎯 Mục tiêu chương
Chương này đặt nền móng cho toàn bộ cuốn sách bằng cách:
- Trình bày mục tiêu kinh doanh của một Data Warehouse
- Giải thích mô hình hướng chiều (Dimensional Modeling)
- Mô tả các thành phần chính trong hệ thống Data Warehouse
- Giới thiệu các khái niệm cơ bản: bảng fact, dimension, Star Schema
- Nêu rõ các hiểu lầm và sai lầm phổ biến khi triển khai Data Warehouse

---

## 🌍 Hai thế giới thông tin
Thông tin trong tổ chức tồn tại dưới hai dạng:
- **Hệ thống giao dịch (operational systems)**: nơi dữ liệu được đưa vào
- **Data Warehouse**: nơi dữ liệu được truy xuất phục vụ phân tích

| Operational World | Analytical World (Data Warehouse) |
|-------------------|-----------------------------------|
| Xử lý từng bản ghi | Truy vấn hàng triệu bản ghi |
| Tác nghiệp (OLTP) | Phân tích (OLAP) |
| Quy trình lặp đi lặp lại | Câu hỏi thay đổi liên tục |

---

## 📰 Ẩn dụ: Người làm dữ liệu là Tổng biên tập
Người quản lý Data Warehouse giống như tổng biên tập của một tạp chí:
- Hiểu độc giả (người dùng business)
- Chọn lọc nội dung phù hợp (dữ liệu cần phân tích)
- Duy trì chất lượng, nhất quán và dễ sử dụng
- Liên tục cập nhật và phục vụ nhu cầu người đọc

---

## 🏗 Các thành phần chính của Data Warehouse

<img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhdU4Qa5hgiLCmJnBZc4PLlFQrqPOb02Vg_DuDcSJp1Bw5h-3GS9H3DlW9LjMp8uupraFDNRyblSjHAB8TwjtNrLdd6NOwHKqKHCQcOHj1cRjtVyZ8-1SAUKz88M4dhNYZsOahzEVqt3o4/s1600/Operational++Source+Systems.jpg" width=600>

| Thành phần             | Mô tả ngắn |
|------------------------|-----------|
| Operational Systems    | Nguồn dữ liệu gốc |
| Data Staging Area      | ETL, xử lý, làm sạch |
| Presentation Area      | Dữ liệu đã sẵn sàng truy vấn |
| Data Access Tools      | Dashboard, ad-hoc query, BI... |

> **Note**: Presentation area bắt buộc phải dùng dimensional model.

---

## 📊 Bảng Fact và Bảng Dim

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240730100256/imgonline-com-ua-resize-7FChpPp58PUg2cZf.jpg" width=600>

### 🧱 Bảng Fact 

- Lưu trữ các đo lường định lượng như doanh số, số lượng.
- Có nhiều dòng nhưng ít cột (sâu và hẹp).
- Có khóa chính là tổ hợp các khóa ngoại từ các bảng dimension.
- Chỉ lưu những giao dịch thực sự xảy ra (không chèn dòng 0).
- Ba loại grain phổ biến:
  - **Transaction grain**
  - **Periodic snapshot**
  - **Accumulating snapshot**

---

### 🧱 Bảng Dimension

- Mô tả bối cảnh cho dữ liệu fact: sản phẩm, khách hàng, thời gian…
- Có nhiều cột mô tả (rộng), ít dòng (nhỏ hơn 1 triệu bản ghi).
- Là nơi dùng để filter, group, gắn nhãn báo cáo.
- Thuộc tính nên là chuỗi có ý nghĩa (tránh viết tắt, mã hóa).

---

## 🌟 Mô hình Star Schema

<img src="https://learn.microsoft.com/en-us/power-bi/guidance/media/star-schema/star-schema-example-1.svg" width=600>

- Bảng fact ở trung tâm, được bao quanh bởi các bảng dimension.
- Cấu trúc đơn giản, dễ hiểu, hiệu suất cao, dễ mở rộng.
- Hỗ trợ truy vấn ad hoc linh hoạt từ mọi chiều.

---

## 🧩 Mối Quan Hệ Giữa ERD và Dimensional Model

<img src="https://i.ytimg.com/vi/w1ROt4qnsac/sddefault.jpg" width=600>

Trong thực tế, nhiều hệ thống có sẵn sơ đồ ERD (Entity Relationship Diagram) phức tạp với hàng trăm bảng. Tuy nhiên, để phục vụ truy vấn phân tích, ERD **không phải** là cách tổ chức hiệu quả. Thay vào đó, chúng ta cần **chuyển hóa** sang mô hình dimensional:

- 🔍 **Tách biệt theo quy trình kinh doanh**: ERD thường mô tả toàn bộ hệ thống, nhưng DW cần chia nhỏ theo từng **business process** (đơn hàng, khiếu nại, thanh toán...) → mỗi quy trình này trở thành một **data mart** độc lập nhưng liên thông.

- 📊 **Fact Table = nơi lưu dữ liệu đo lường**: Mọi mối quan hệ nhiều-nhiều có số liệu như doanh thu, số lượt, thời gian xử lý... đều nên quy về **Fact Table**.

- 🏷️ **Dimension Table = nơi lưu ngữ cảnh phân tích**: Các bảng còn lại (sản phẩm, khách hàng, địa lý, thời gian...) được gom lại và thiết kế lại để tạo thành các **Dimension Table** chứa thuộc tính mô tả (rộng, dễ hiểu, có phân cấp).

💡 Một ERD lớn → **phân rã logic theo process → chuyển hóa thành nhiều Star Schema đơn giản**, dễ dùng, dễ scale, dễ bảo trì.

---

## ⚖️ So sánh: Dimensional Model vs Normalized Model (ERD)

| Khía cạnh     | Dimensional Model              | Normalized Model (ERD)         |
|---------------|--------------------------------|--------------------------------|
| 🎯 Mục đích     | Phân tích, báo cáo              | Giao dịch (OLTP)               |
| 🔍 Truy vấn     | Dễ viết, nhanh, trực quan       | JOIN phức tạp, khó mở rộng     |
| 🧠 Tư duy thiết kế | Theo quy trình nghiệp vụ         | Theo cấu trúc dữ liệu thực thể |
| ⭐ Cấu trúc     | Star Schema (Fact + Dimensions)| Sơ đồ mạng nhện (nhiều quan hệ)|
| 📍 Áp dụng      | Presentation Layer (DW)         | Staging Layer / Hệ thống OLTP  |

> ✅ Dimensional model không thay thế ERD — mà là **chuyển hoá phù hợp theo mục tiêu sử dụng**. Khi cần phân tích và hỗ trợ ra quyết định, ta luôn cần mô hình dimensional đơn giản và trực quan hơn cho người dùng cuối.

---

## 🧠 Các ngộ nhận phổ biến

1. **Chỉ dùng cho dữ liệu tổng hợp** → sai, nên dùng dữ liệu chi tiết.
2. **Chỉ cho phòng ban nhỏ** → sai, nên tổ chức theo business process.
3. **Không mở rộng được** → sai, thực tế rất scale tốt.
4. **Không linh hoạt** → sai, dễ thêm chi tiết, chiều, đo lường mới.
5. **Không tích hợp được** → sai, nếu có bus architecture và conformed dimensions.

---

## 💥 10 sai lầm cần tránh

1. Quá tập trung vào công nghệ, quên mất mục tiêu kinh doanh.
2. Không có người bảo trợ từ lãnh đạo doanh nghiệp.
3. Dự án quá lớn, không có vòng lặp nhỏ và khả thi.
4. Tập trung backend, không xây dựng frontend usable.
5. Thiết kế dữ liệu trình bày quá phức tạp.
6. Bỏ qua trải nghiệm người dùng khi truy vấn.
7. Không xây dựng conformed dimension chung.
8. Chỉ load dữ liệu tổng hợp.
9. Cho rằng dữ liệu, yêu cầu và công nghệ là bất biến.
10. Không đạt được sự chấp nhận của người dùng.

---

## ✅ Kết luận

- Dimensional Modeling = đơn giản + mạnh mẽ + mở rộng dễ dàng
- Là nền tảng chuẩn cho **presentation area**
- Hạn chế dùng normalized trong tầng truy vấn
- Đảm bảo trải nghiệm tốt cho người dùng cuối

> “The data warehouse is only as good as its dimensions.” – Ralph Kimball