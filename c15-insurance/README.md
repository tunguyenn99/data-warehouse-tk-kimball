# 🛡️ Chương 15: Bảo hiểm (Insurance)

## 📘 Insurance Case Study

* Giới thiệu một tổ chức bảo hiểm cung cấp nhiều loại sản phẩm như: bảo hiểm nhân thọ, xe, nhà, sức khỏe
* Dữ liệu liên quan đến hợp đồng (policy), yêu cầu bồi thường (claim), và sự kiện rủi ro (accident)

---

## 🔗 Insurance Value Chain

* Chuỗi giá trị ngành bảo hiểm bao gồm:

  * Phân phối sản phẩm bảo hiểm
  * Quản lý hợp đồng
  * Nhận yêu cầu và xử lý bồi thường
  * Quản lý rủi ro và tái bảo hiểm

---

## 🚌 Draft Insurance Bus Matrix

* Xác định các process (policy, claim, risk...) và dimension chung
* Dimension chuẩn hoá để dùng lại trong các data mart khác nhau: khách hàng, sản phẩm, đại lý, thời gian, vị trí

---

## 📄 Policy Transactions

* Ghi nhận các giao dịch hợp đồng: mở mới, gia hạn, thay đổi điều khoản, huỷ
* Mỗi dòng fact đại diện một giao dịch hợp đồng cụ thể

---

## 🧱 Dimension Details and Techniques

* Chi tiết dimension:

  * Khách hàng, sản phẩm, kênh bán hàng, đại lý, địa lý
* Dùng kỹ thuật SCD để theo dõi thay đổi thông tin khách hàng
* Dùng bridge hoặc multivalued dimension cho người thụ hưởng, điều khoản mở rộng

---

## 📆 Alternative or Complementary Policy Accumulating Snapshot

* Mô hình accumulating snapshot theo dõi toàn bộ vòng đời hợp đồng:

  * Mở hợp đồng, kích hoạt, gia hạn, huỷ bỏ
* Giúp đo thời gian xử lý và hiệu suất quy trình

## 📅 Policy Periodic Snapshot

* Ghi nhận trạng thái hợp đồng theo định kỳ (hàng tháng/quý)
* Có thể lưu:

  * Tình trạng hiệu lực, số tiền bảo hiểm, phí đóng...

---

## 🔄 Conformed Dimensions & Facts

* Dùng dimension và fact đồng nhất giữa policy và claim:

  * Khách hàng, sản phẩm, thời gian
* Cho phép phân tích hợp nhất giữa hai quy trình chính

---

## 🧩 Heterogeneous Products & Multivalued Dimensions (again)

* Sản phẩm bảo hiểm đa dạng, cấu trúc khác nhau
* Một hợp đồng có thể chứa nhiều loại bảo hiểm → multivalued dimension

---

## 🏗️ More Case Background & Updated Bus Matrix

* Bổ sung use case xử lý bồi thường (claims)
* Mở rộng bus matrix để bao phủ toàn bộ chuỗi giá trị

---

## 💥 Claims Transactions

* Ghi nhận yêu cầu bồi thường: ngày xảy ra sự kiện, báo cáo, xử lý, thanh toán
* Mỗi dòng fact = một sự kiện yêu cầu bồi thường

## 📈 Claims Accumulating Snapshot

* Theo dõi toàn bộ quá trình xử lý yêu cầu bồi thường:

  * Báo cáo, kiểm tra, định giá tổn thất, phê duyệt, chi trả

## 🧾 Policy/Claims Consolidated Snapshot

* Kết hợp trạng thái hợp đồng và tình trạng bồi thường trong 1 bảng snapshot duy nhất
* Hỗ trợ phân tích toàn diện khách hàng và rủi ro

## 🚫 Factless Accident Events

* Lưu sự kiện tai nạn/rủi ro mà chưa có yêu cầu bồi thường cụ thể
* Dùng factless fact table để theo dõi các sự kiện chưa rõ kết quả

---

## ❌ Common Dimensional Modeling Mistakes to Avoid

* Sai sót thường gặp:

  * Trộn lẫn grain
  * Không tách rõ transaction và snapshot
  * Thiếu dimension chuẩn hoá (conformed)
  * Không xử lý SCD đúng cách

---

## 📌 Tóm tắt chương

* Ngành bảo hiểm cần nhiều loại bảng fact: transaction, snapshot, accumulating
* Dữ liệu phân mảnh và đa hình: sản phẩm, điều khoản, người thụ hưởng
* Dùng dimension và fact đồng nhất để tích hợp data mart
* Tránh lỗi thiết kế như mix grain, thiếu chuẩn hoá, hoặc lặp dimension không cần thiết
