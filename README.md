# 📘 Kimball Data Warehouse – Từ điển Thuật ngữ

**Tổng hợp các thuật ngữ quan trọng trong sách _The Data Warehouse Toolkit (2nd Edition)_ của Ralph Kimball** – tài liệu nền tảng về kho dữ liệu và mô hình hóa dữ liệu hướng phân tích (Dimensional Modeling).

---

## 📚 Giới thiệu

Khi đọc sách *The Data Warehouse Toolkit*, bạn sẽ gặp hàng trăm thuật ngữ chuyên ngành liên quan đến:

- Mô hình dữ liệu dạng sao (Star Schema), tuyết hoa (Snowflake Schema)
- Bảng Fact, bảng Dimension, khóa Surrogate
- Quản lý thay đổi chậm (Slowly Changing Dimension – SCD)
- OLAP, ETL, Bus Architecture, Data Mart…
- Và rất nhiều khái niệm khác trong lĩnh vực BI/Data Warehouse

📖 Để giúp việc đọc sách dễ dàng hơn, mình đã dịch toàn bộ phần *Glossary* trong sách, chia theo từng nhóm A–Z. Mỗi thuật ngữ đều có giải thích ngắn gọn, chính xác, dễ hiểu – bám sát ngữ cảnh sách Kimball.

---

## 💡 Cách sử dụng

- Dùng `Ctrl + F` để tra cứu nhanh khi đọc sách
- Có thể tích hợp vào Obsidian, VSCode hoặc bất kỳ trình đọc Markdown nào
- Sử dụng như tài liệu tham khảo khi làm việc với BI, Data Warehouse, SQL, Power BI, Snowflake, BigQuery, v.v.

---

### 📘 Glossary Kimball - Thuật ngữ A–B

| Thuật ngữ | Giải thích |
|----------|------------|
| **24/7 Operational availability** | Hoạt động liên tục 24 giờ mỗi ngày, 7 ngày mỗi tuần. |
| **3NF (Third Normal Form)** | Dạng chuẩn thứ ba trong mô hình hóa dữ liệu quan hệ. |
| **Accumulating snapshot fact table** | Bảng fact tích lũy – lưu nhiều mốc thời gian của một quy trình ngắn hạn. Dữ liệu cập nhật khi có tiến triển mới. |
| **Activity-based costs** | Chi phí được xác định dựa trên hoạt động thực tế thay vì chuẩn cố định. |
| **Additive (facts)** | Các giá trị có thể cộng dồn theo tất cả chiều (dimensions). |
| **Ad hoc queries** | Truy vấn tự do do người dùng đặt ra bất ngờ. |
| **Aggregate navigator** | Lớp phần mềm chuyển đổi truy vấn SQL sang dùng dữ liệu tổng hợp có sẵn. |
| **Aggregates** | Dữ liệu tổng hợp – thường là tổng, trung bình, hoặc đếm. |
| **Algorithm** | Thuật toán – công thức xử lý dữ liệu. |
| **Alias (SQL)** | Tên tạm trong SQL, thường viết ngắn cho bảng hoặc cột. |
| **Allocated inventory** | Hàng tồn đã được phân bổ để giao nhưng chưa thực sự chuyển đi. |
| **Allocations** | Phân bổ chi phí hoặc dữ liệu cho nhiều đối tượng khác nhau. |
| **Allowance** | Khoản giảm giá từ giá niêm yết – thường do khuyến mãi. |
| **Analytic application** | Ứng dụng phân tích được thiết kế sẵn cho người dùng cuối. |
| **Analytic processing** | Xử lý dữ liệu phục vụ phân tích, so với xử lý vận hành. |
| **ANSI** | Viện tiêu chuẩn quốc gia Mỹ – phát triển tiêu chuẩn như SQL. |
| **Answer set** | Tập kết quả trả về từ truy vấn SQL. |
| **Application constraint (SQL)** | Điều kiện lọc dữ liệu trong WHERE, áp dụng cho cột dimension. |
| **Architected data marts** | Các data mart được thiết kế theo cấu trúc có chuẩn hóa. |
| **ASCII** | Bộ mã ký tự tiêu chuẩn của Mỹ – chỉ hỗ trợ 127 ký tự. |
| **Asset** | Tài sản thuộc quyền sở hữu hoặc được người khác nợ. |
| **Associative table / Bridge table** | Bảng trung gian thể hiện quan hệ nhiều-nhiều. |
| **Atomic data** | Dữ liệu nguyên tử – mức chi tiết thấp nhất. |
| **Attribute** | Thuộc tính – là cột trong bảng dimension. |
| **Audit dimension** | Dimension đặc biệt ghi metadata về dòng dữ liệu trong fact. |
| **Authentication** | Quá trình xác định danh tính người dùng (VD: mật khẩu, vân tay...). |
| **Average order backlog** | Thời gian trung bình đơn hàng bị chậm trễ xử lý. |
| **B-tree index** | Cấu trúc chỉ mục tốt cho dữ liệu có độ phân biệt cao. |
| **Baseline sales** | Doanh số giả định nếu không có chương trình khuyến mãi. |
| **Behavior score** | Điểm hành vi – phản ánh hành vi mua hàng hoặc tín dụng của khách. |
| **Behavior study group** | Nhóm người dùng được chọn để phân tích hành vi, không thể lọc bằng các ràng buộc đơn giản. |
| **BI (Business Intelligence)** | Trí tuệ doanh nghiệp – khai thác dữ liệu để hỗ trợ quyết định. |
| **Bitmap index** | Chỉ mục bitmap – dùng cho cột có ít giá trị khác nhau (low cardinality). |
| **Brick and mortar** | Doanh nghiệp truyền thống có cửa hàng thực tế. |
| **Browse query** | Truy vấn liệt kê giá trị có thể chọn – thường là `SELECT DISTINCT`. |
| **Browser** | Trình duyệt web – hiển thị nội dung từ máy chủ web. |
| **Bus** | Cấu trúc giao tiếp chuẩn để các data mart liên kết hiệu quả. |
| **Business dimensional lifecycle** | Chu trình phát triển kho dữ liệu theo Kimball. |
| **Business intelligence (BI)** | Tập hợp công cụ, quy trình để phân tích và hỗ trợ ra quyết định. |
| **Business measure** | Chỉ số hoạt động kinh doanh – được lưu trong bảng fact. |
| **Business process** | Quy trình nghiệp vụ chính như bán hàng, đặt hàng... – là nền tảng thiết kế data mart. |
| **Byte (B)** | Đơn vị lưu trữ gồm 8 bit. |
| **Cache** | Vùng lưu trữ tạm để tăng tốc truy xuất dữ liệu. |
| **Cannibalization** | Một sản phẩm mới làm giảm doanh số sản phẩm cũ. |
| **Cardinality** | Độ phân biệt – số lượng giá trị duy nhất trong một cột. |
| **Cartesian product** | Tổ hợp tất cả các giá trị có thể của nhiều tập dữ liệu. |
| **Causal factor / dimension** | Nhân tố/nguyên nhân gây ảnh hưởng – thường là quảng cáo, giảm giá... |
| **Centipede fact table** | Bảng fact có quá nhiều dimension, gây phức tạp – thường do thiết kế sai. |
    

---

### 📘 Glossary Kimball - Thuật ngữ C–D

| Thuật ngữ | Giải thích |
|----------|------------|
| **Chart of accounts** | Danh sách tài khoản sử dụng trong sổ cái kế toán. |
| **Churn** | Tỷ lệ khách hàng rời bỏ trong một dịch vụ thuê bao. |
| **CIO (Chief Information Officer)** | Giám đốc thông tin – người phụ trách công nghệ và hệ thống dữ liệu trong tổ chức. |
| **Click and mortar** | Doanh nghiệp kết hợp giữa cửa hàng truyền thống và kênh bán hàng trực tuyến. |
| **Clickstream** | Dòng hành vi người dùng trên web – thể hiện chuỗi hành động như nhấp chuột, xem trang. |
| **Consolidated data mart** | Data mart tổng hợp từ nhiều quy trình nghiệp vụ. |
| **Constraint (SQL)** | Điều kiện lọc dữ liệu – có thể là join constraint hoặc application constraint. |
| **Cookie** | Tệp văn bản nhỏ được web server lưu trên máy người dùng để lưu trạng thái truy cập. |
| **Copybook** | File định nghĩa cấu trúc dữ liệu truyền thống trong COBOL. |
| **Core table** | Bảng chính dùng chung trong hệ thống có nhiều loại sản phẩm dị biệt. |
| **Coverage table** | Bảng fact không chứa số liệu, thể hiện vùng phủ khuyến mãi theo sản phẩm/cửa hàng. |
| **CRM (Customer Relationship Management)** | Quản trị quan hệ khách hàng – quy trình xây dựng và duy trì mối quan hệ với khách. |
| **Cross-selling** | Bán chéo – giới thiệu sản phẩm khác cho khách hàng hiện tại. |
| **Cube** | Cấu trúc dữ liệu đa chiều trong OLAP, ban đầu gồm 3 chiều cơ bản: sản phẩm, thời gian, khu vực. |
| **Custom line-of-business table** | Bảng dành riêng cho một dòng sản phẩm có cấu trúc đặc thù. |
| **Customer master file** | File chính lưu thông tin khách hàng, thường do hệ thống vận hành duy trì. |
| **Customer matching** | Quá trình xác định cùng một khách hàng xuất hiện ở nhiều hệ thống khác nhau. |
| **Cyclic redundancy checksum (CRC)** | Giải thuật kiểm tra sự thay đổi dữ liệu bằng cách so sánh mã tổng CRC. |
| **Data access tool** | Công cụ truy cập dữ liệu – dùng để thực hiện truy vấn và phân tích dữ liệu từ kho dữ liệu. |
| **Data cube** | Khái niệm tương đương với cube – đại diện cho dữ liệu đa chiều. |
| **Data extract** | Quá trình trích xuất dữ liệu từ hệ thống nguồn sang kho dữ liệu. |
| **Data quality assurance** | Kiểm soát chất lượng dữ liệu – đảm bảo dữ liệu chính xác, đầy đủ và có thể sử dụng được. |
| **Data staging tool** | Công cụ hỗ trợ quy trình ETL trong giai đoạn xử lý trung gian (staging area). |
| **Data stovepipe** | Hệ thống dữ liệu cô lập – không chia sẻ dữ liệu với hệ thống khác. |
| **Data warehouse** | Kho dữ liệu – nơi lưu trữ dữ liệu được tổ chức để phục vụ phân tích. |
| **Data warehouse bus architecture** | Kiến trúc kho dữ liệu dựa trên các dimension và fact chuẩn hóa (conformed). |
| **Database management system (DBMS)** | Hệ quản trị cơ sở dữ liệu – phần mềm dùng để lưu trữ và truy xuất dữ liệu. |
| **Days’ supply (inventory)** | Số ngày lượng tồn kho hiện tại có thể đáp ứng dựa trên tốc độ bán hiện tại. |
| **DBA (Database Administrator)** | Quản trị viên cơ sở dữ liệu – người vận hành và tối ưu hệ thống dữ liệu. |
| **Decision support system (DSS)** | Hệ thống hỗ trợ ra quyết định – tiền thân của khái niệm kho dữ liệu. |
| **Decode** | Diễn giải giá trị mã – ví dụ, 0 = 'Chưa xác thực', 1 = 'Đã xác thực'. |
| **Degenerate dimension** | Dimension không có thuộc tính, thường là mã giao dịch, mã hóa đơn... |
| **Demand side** | Chuỗi quy trình bắt đầu từ hàng tồn đến khi bán được cho khách – đối lập với supply side. |
| **Denormalize** | Phi chuẩn hóa – chấp nhận dữ liệu dư thừa để đơn giản hóa truy vấn và tăng hiệu năng. |
| **Depletions** | Hàng hóa được xuất kho – thường dùng trong bối cảnh đáp ứng đơn đặt hàng. |
| **Dimension** | Bảng thông tin mô tả, dùng để phân tích và phân nhóm số liệu trong fact table. |
| **Dimension table** | Bảng chứa dữ liệu mô tả dùng trong mô hình dimensional – có khóa chính đơn và các thuộc tính. |
| **Dimensional model** | Mô hình dữ liệu thiết kế theo hướng phân tích – gồm fact table và các dimension. |
| **Directory server** | Máy chủ lưu thông tin người dùng và tài nguyên trong mạng, hỗ trợ tra cứu qua LDAP. |
| **Discrete attribute** | Thuộc tính rời rạc – có tập giá trị cố định, ví dụ: màu sắc, kích cỡ. |
| **Drill up** | Tóm gọn dữ liệu bằng cách gỡ bỏ hoặc thay thế một chiều chi tiết bằng chiều tổng quát hơn. |
| **DSS (Decision Support System)** | Viết tắt của hệ thống hỗ trợ ra quyết định. |

---

### 📘 Glossary Kimball - Thuật ngữ E–G

| Thuật ngữ | Giải thích |
|----------|------------|
| **Earned income** | Thu nhập đã kiếm được – chỉ ghi nhận khi dịch vụ đã được thực hiện, dù đã được thanh toán trước. |
| **End-aisle displays** | Kệ trưng bày cuối dãy – hình thức khuyến mãi trong siêu thị. |
| **Enterprise application integration (EAI)** | Tích hợp ứng dụng doanh nghiệp – đồng bộ các hệ thống vận hành khác nhau trong tổ chức. |
| **Enterprise data warehouse (EDW)** | Kho dữ liệu toàn doanh nghiệp – tập hợp toàn bộ staging và presentation layer. |
| **Enterprise resource planning (ERP)** | Hệ thống hoạch định nguồn lực – tích hợp nhiều chức năng như tài chính, nhân sự, sản xuất... |
| **Entity-relationship diagram (ERD)** | Sơ đồ thực thể – mô tả mối quan hệ giữa các bảng trong cơ sở dữ liệu. |
| **Equal access** | Khả năng truy vấn dữ liệu từ bất kỳ tiêu chí nào – nguyên lý gốc của CSDL quan hệ. |
| **ETL (Extract–Transform–Load)** | Quy trình trích xuất – biến đổi – tải dữ liệu từ hệ thống nguồn vào kho dữ liệu. |
| **Event** | Sự kiện – hành động hoặc trạng thái được ghi nhận, ví dụ: tai nạn, đơn hàng, giao dịch. |
| **Event-tracking table** | Bảng fact (thường là factless) ghi nhận các sự kiện – ví dụ: hành vi người dùng, tương tác web. |
| **Extended ASCII** | Mở rộng bộ mã ASCII để hỗ trợ ký tự có dấu, ký tự đặc biệt – gồm 256 ký tự. |
| **Extended cost** | Giá trị chi phí mở rộng – bằng đơn giá nhân với số lượng. |
| **Extensible Markup Language (XML)** | Ngôn ngữ đánh dấu mở rộng – dùng để trao đổi dữ liệu có cấu trúc. |
| **Extract–Transform–Load (ETL)** | Tên đầy đủ của quy trình ETL. |
| **Fact** | Dữ liệu định lượng mô tả hiệu suất kinh doanh – thường là số liệu có thể cộng dồn. |
| **Fact dimension** | Dimension đặc biệt mô tả các loại chỉ số trong bảng fact rất thưa và không đồng nhất. |
| **Fact table** | Bảng trung tâm trong mô hình sao – lưu các chỉ số định lượng, khóa ngoại liên kết đến dimension. |
| **Factless fact table** | Bảng fact không có chỉ số – ghi nhận sự kiện hoặc vùng phủ. |
| **File Transfer Protocol (FTP)** | Giao thức truyền tệp – dùng để di chuyển file giữa các hệ thống. |
| **Filter on fact rows** | Bộ lọc áp dụng trên giá trị của các cột fact – ví dụ: chỉ chọn giao dịch > 1 triệu. |
| **First-level data mart** | Data mart lấy dữ liệu trực tiếp từ một hệ thống nguồn chính. |
| **Fixed depth hierarchy** | Cấu trúc phân cấp có số tầng xác định trước – ví dụ: Quốc gia > Vùng > Tỉnh. |
| **Foreign key (FK)** | Khóa ngoại – tham chiếu đến khóa chính trong bảng khác. |
| **Framework** | Khung kiến trúc tổng thể – ví dụ: data warehouse bus architecture. |
| **FROM clause (SQL)** | Phần trong câu lệnh SQL xác định bảng dữ liệu được sử dụng. |
| **General ledger (G/L)** | Sổ cái – ghi chép toàn bộ tài sản, nợ, doanh thu, chi phí. |
| **Geographic information system (GIS)** | Hệ thống thông tin địa lý – kết hợp bản đồ với cơ sở dữ liệu. |
| **Gigabyte (GB)** | Một tỉ byte dữ liệu – đơn vị đo lường dung lượng lưu trữ. |
| **GMROI** | Tỷ suất lợi nhuận gộp trên tồn kho – GMROI = số vòng quay * tỷ lệ lợi nhuận gộp. |
| **Grain** | Mức độ chi tiết của dữ liệu trong một dòng của bảng fact. |
| **Granularity** | Độ chi tiết của dữ liệu – càng nhỏ thì càng chi tiết. |
| **Greenwich Mean Time (GMT)** | Giờ gốc quốc tế – múi giờ 0, dùng để đồng bộ thời gian toàn cầu. |
| **Gross margin percent** | Tỷ lệ lợi nhuận gộp – lợi nhuận gộp chia cho doanh thu. |
| **Gross profit** | Lợi nhuận gộp – doanh thu trừ đi giá vốn. |
| **Gross revenue** | Doanh thu gộp – tổng tiền khách hàng trả trước khi trừ chiết khấu. |
| **GROUP BY clause (SQL)** | Câu lệnh SQL dùng để nhóm dữ liệu theo một hoặc nhiều cột. |
| **GUI (Graphic User Interface)** | Giao diện đồ họa người dùng – có nút, biểu tượng, cửa sổ trực quan. |

---

### 📘 Glossary Kimball - Thuật ngữ H–L

| Thuật ngữ | Giải thích |
|----------|------------|
| **Helper table / Bridge table** | Bảng trung gian – thể hiện quan hệ nhiều-nhiều giữa fact và dimension. |
| **Heterogeneous products** | Sản phẩm dị biệt – có đặc điểm, chỉ số không đồng nhất giữa các dòng sản phẩm. |
| **Hierarchy** | Phân cấp – cấu trúc thể hiện quan hệ cha – con giữa các cấp độ dữ liệu. |
| **Householding** | Gộp nhiều cá nhân/tài khoản vào cùng một hộ gia đình cho mục đích phân tích. |
| **HTML (HyperText Markup Language)** | Ngôn ngữ đánh dấu siêu văn bản – định dạng nội dung web. |
| **HTTP (HyperText Transfer Protocol)** | Giao thức truyền tải nội dung web giữa trình duyệt và máy chủ. |
| **Impact report** | Báo cáo dùng bridge table mà không áp dụng trọng số – thể hiện toàn bộ các dòng liên quan. |
| **Implementation bus matrix** | Ma trận bus triển khai – liệt kê các bảng fact, độ chi tiết và chỉ số tương ứng theo từng quy trình. |
| **Index** | Cấu trúc tăng tốc truy vấn bằng cách sắp xếp dữ liệu theo khóa – gồm B-tree, Bitmap... |
| **Internet** | Mạng toàn cầu kết nối các thiết bị và dịch vụ qua giao thức IP. |
| **ISP (Internet Service Provider)** | Nhà cung cấp dịch vụ internet. |
| **IP address** | Địa chỉ định danh thiết bị trong mạng – ví dụ: 192.168.1.1 |
| **Join constraint (SQL)** | Điều kiện trong câu lệnh SQL thể hiện mối liên kết giữa các bảng. |
| **JPEG (Joint Photographic Experts Group)** | Định dạng nén ảnh – hỗ trợ hình ảnh phức tạp như ảnh chụp. |
| **Julian day number** | Cách biểu diễn ngày tháng bằng số nguyên – số ngày kể từ một thời điểm gốc. |
| **Junk dimension** | Dimension chứa nhiều cờ (flag) hoặc mã nhỏ – gom lại để tránh làm rối bảng fact. |
| **LDAP (Lightweight Directory Access Protocol)** | Giao thức truy cập thông tin người dùng và tài nguyên mạng. |
| **Liability** | Khoản nợ – nghĩa vụ tài chính mà doanh nghiệp phải trả. |
| **Lift (of a promotion)** | Mức tăng doanh số so với mức cơ sở (baseline) nhờ khuyến mãi. |
| **Line item** | Dòng chi tiết trong chứng từ như hóa đơn – thể hiện từng sản phẩm cụ thể. |
| **Logical design** | Thiết kế logic – mô tả mối quan hệ giữa các bảng và thuộc tính, chưa đi vào vật lý. |
| **Loss party (insurance)** | Các bên liên quan đến một vụ tổn thất bảo hiểm – ví dụ: người bị thương, luật sư... |
| **Low-cardinality attribute** | Thuộc tính có ít giá trị phân biệt – ví dụ: giới tính, trạng thái hoạt động. |

---

### 📘 Glossary Kimball - Thuật ngữ M–P

| Thuật ngữ | Giải thích |
|----------|------------|
| **Many-to-many relationship** | Quan hệ nhiều-nhiều – một bản ghi ở bảng A có thể liên kết với nhiều bản ghi ở bảng B và ngược lại. |
| **Many-valued dimensions** | Dimension có thể có nhiều giá trị cho một bản ghi fact – xử lý qua bridge table. |
| **Market basket analysis** | Phân tích giỏ hàng – xác định các sản phẩm thường được mua cùng nhau. |
| **Market growth** | Tăng trưởng thị trường – doanh số tăng thật sự chứ không chỉ do chuyển dịch giữa sản phẩm. |
| **MBA (Master of Business Administration)** | Thạc sĩ Quản trị Kinh doanh – chuyên ngành quản trị doanh nghiệp. |
| **Merchandise hierarchy** | Phân cấp sản phẩm – ví dụ: Loại > Nhóm > Danh mục > SKU. |
| **Meta data** | Siêu dữ liệu – dữ liệu mô tả dữ liệu, như cấu trúc, nguồn gốc, chất lượng. |
| **Migration** | Di chuyển dữ liệu giữa các hệ thống hoặc định dạng khác nhau. |
| **Minidimension** | Dimension nhỏ được tách ra từ dimension chính để giảm độ lớn và theo dõi thay đổi. |
| **Mirrored database** | Cơ sở dữ liệu được nhân bản – thường để dự phòng và tăng hiệu năng đọc. |
| **Modeling application** | Ứng dụng phân tích nâng cao – ví dụ: dự báo, phân cụm, tính điểm khách hàng. |
| **Most recent indicator** | Cờ đánh dấu bản ghi dimension hiện hành trong dạng thay đổi chậm Type 2. |
| **Multidimensional database** | Cơ sở dữ liệu đa chiều – lưu dữ liệu theo dạng khối (cube). |
| **MOLAP (Multidimensional OLAP)** | OLAP dùng cơ sở dữ liệu đa chiều – hiệu năng tốt nhưng ít linh hoạt. |
| **Multipass SQL** | Truy vấn SQL nhiều lần – hợp nhất kết quả từ các bảng fact qua dimension chuẩn hóa. |
| **Multitable join query** | Truy vấn kết hợp nhiều bảng – phổ biến trong môi trường kho dữ liệu. |
| **Multivalued dimension** | Tương đương many-valued dimension – xử lý bằng bảng bridge. |
| **Natural key** | Khóa tự nhiên – khóa được hệ thống vận hành sử dụng, mang ý nghĩa thật. |
| **Nonadditive fact** | Fact không thể cộng dồn – ví dụ: tỷ lệ, số dư cuối kỳ. |
| **Normalize** | Chuẩn hóa dữ liệu – tách thành nhiều bảng nhỏ để tránh dư thừa và bất nhất. |
| **Null** | Giá trị rỗng – không tồn tại hoặc chưa được xác định. |
| **ODS (Operational Data Store)** | Kho dữ liệu tác nghiệp – dùng để truy vấn báo cáo thời gian thực. |
| **Off-invoice allowance** | Khoản giảm trừ khỏi hóa đơn – thường là khuyến mãi hay hỗ trợ thương mại. |
| **One-to-many relationship** | Một-nhiều – một bản ghi bảng A liên kết với nhiều bản ghi bảng B. |
| **OLAP (Online Analytical Processing)** | Hệ thống xử lý phân tích dữ liệu – hỗ trợ phân tích đa chiều. |
| **OLTP (Online Transaction Processing)** | Hệ thống xử lý giao dịch – ưu tiên tốc độ ghi, độ chính xác cao. |
| **Operational system of record** | Hệ thống vận hành chính – nơi phát sinh dữ liệu thực tế. |
| **ORDER BY clause (SQL)** | Câu lệnh SQL sắp xếp kết quả theo thứ tự tăng/giảm. |
| **Outrigger table** | Bảng dimension phụ được nối từ dimension chính (snowflake). |
| **P&L (Profit and Loss)** | Báo cáo lãi lỗ – thể hiện doanh thu, chi phí và lợi nhuận. |
| **Page** | Đơn vị nội dung trong web hoặc hệ thống lưu trữ. |
| **Parent-child database** | Cấu trúc dữ liệu phân cấp – ví dụ: đơn hàng và dòng đơn hàng. |
| **Parsing** | Tách chuỗi thành các phần tử nhỏ hơn – ví dụ: tách họ tên từ chuỗi đầy đủ. |
| **Partitioned table** | Bảng chia vùng – thường theo ngày để tăng tốc truy vấn và quản lý. |
| **Partitioning of history** | Gắn từng bản ghi fact với đúng bản ghi dimension tại thời điểm lịch sử tương ứng (SCD Type 2). |
| **Periodic snapshot fact table** | Bảng ảnh chụp định kỳ – ghi lại trạng thái tại các mốc thời gian (VD: cuối ngày/tháng). |
| **Physical design** | Thiết kế vật lý – cấu trúc bảng, chỉ mục, cách lưu dữ liệu thực tế. |
| **PK (Primary Key)** | Khóa chính – định danh duy nhất cho mỗi dòng trong bảng. |
| **Point-of-sale (POS)** | Hệ thống bán hàng tại quầy – ghi nhận giao dịch trực tiếp. |
| **Portal** | Cổng thông tin tập trung – nơi người dùng bắt đầu truy cập dịch vụ, dữ liệu. |
| **Price-point analysis** | Phân tích theo mức giá – ví dụ: so sánh doanh số theo từng mức giá bán. |
| **Primary key** | Khóa chính – như PK, đảm bảo không trùng lặp và duy nhất. |
| **Product master file** | Tệp dữ liệu sản phẩm chính – chứa thông tin mô tả mọi SKU. |
| **Promotion** | Chương trình khuyến mãi – gồm giảm giá, trưng bày, quảng cáo. |
| **Proxy** | Máy chủ trung gian – thay mặt gửi yêu cầu nhằm tăng hiệu suất hoặc kiểm soát truy cập. |
| **Pseudotransaction** | Giao dịch giả lập – tạo ra từ việc so sánh trạng thái trước và sau để giả định thay đổi. |
| **Publishing the right data** | Nguyên tắc xuất bản dữ liệu – dữ liệu chỉ có giá trị nếu phục vụ đúng mục tiêu kinh doanh. |
| **Pull-down list** | Danh sách chọn thả xuống – hiển thị các lựa chọn cho người dùng trong giao diện. |

---

### 📘 Glossary Kimball - Thuật ngữ Q–S

| Thuật ngữ | Giải thích |
|----------|------------|
| **Query** | Truy vấn – yêu cầu lấy dữ liệu từ kho dữ liệu (thường là câu lệnh SQL). |
| **Ragged hierarchy** | Phân cấp không đều – có tầng sâu tầng cạn, không cố định số cấp. |
| **Real-time partitions** | Vùng dữ liệu thời gian thực – hỗ trợ cập nhật nhanh ngoài data warehouse truyền thống. |
| **Reason code** | Mã lý do – giải thích vì sao xảy ra một giao dịch như huỷ đơn, hoàn tiền... |
| **Redundancy** | Dư thừa dữ liệu – có thể làm tăng chi phí lưu trữ, nhưng đôi khi giúp tăng hiệu suất. |
| **Referential integrity (RI)** | Tính toàn vẹn tham chiếu – đảm bảo khóa ngoại trong bảng fact phải khớp khóa chính ở dimension. |
| **Referral** | Nguồn giới thiệu – xác định người dùng đến từ đâu (VD: trang trước đó). |
| **Relational DBMS (RDBMS)** | Hệ quản trị CSDL quan hệ – lưu dữ liệu theo bảng và dùng SQL. |
| **Return on Investment (ROI)** | Tỷ suất lợi nhuận đầu tư – đo lường hiệu quả sử dụng vốn. |
| **Role-playing dimension** | Dimension đóng nhiều vai – ví dụ: bảng thời gian được dùng cho cả order date và ship date. |
| **Roll up** | Tổng hợp dữ liệu – ví dụ: cộng từ cấp tỉnh lên cấp vùng. |
| **Row** | Dòng dữ liệu trong bảng – mỗi dòng là một bản ghi. |
| **Row header** | Phần không được tính toán (non-aggregated) trong SELECT – cũng là GROUP BY. |
| **Sales invoice** | Hóa đơn bán hàng – chứa thông tin giao dịch, sản phẩm, số lượng, giá cả. |
| **Scalability** | Khả năng mở rộng – hệ thống có thể xử lý khối lượng lớn hơn mà không giảm hiệu năng. |
| **Schema** | Lược đồ – thiết kế logic của hệ thống dữ liệu (các bảng, quan hệ, kiểu dữ liệu). |
| **Second-level mart** | Data mart hợp nhất dữ liệu từ nhiều quy trình nghiệp vụ (xem: consolidated data mart). |
| **SELECT DISTINCT (SQL)** | Truy vấn SQL loại bỏ dòng trùng lặp trong kết quả trả về. |
| **SELECT list (SQL)** | Danh sách cột được chọn trong truy vấn SQL sau từ khóa SELECT. |
| **Semantic layer** | Lớp giao diện logic – giúp người dùng truy vấn dễ dàng hơn mà không cần biết cấu trúc thật. |
| **Semiadditive fact** | Fact chỉ cộng được theo một số chiều – ví dụ: tồn kho không cộng được theo thời gian. |
| **Session** | Phiên làm việc – chuỗi hoạt động liên tục của người dùng trên website. |
| **Shelf displays** | Trưng bày trên kệ – hình thức khuyến mãi tại điểm bán. |
| **SKU (Stock Keeping Unit)** | Mã đơn vị lưu kho – mã định danh duy nhất cho mỗi sản phẩm. |
| **Slice and dice** | Phân tách và kết hợp dữ liệu theo nhiều chiều – kỹ thuật cơ bản trong OLAP. |
| **Slowly Changing Dimension (SCD)** | Dimension thay đổi chậm – có 3 loại chính: Type 1, 2, 3. |
| **Snapshot** | Ảnh chụp dữ liệu tại một thời điểm – gồm periodic và accumulating snapshot. |
| **Snowflake** | Mô hình dimension chuẩn hóa – bảng dimension được chia nhỏ thêm cấp phụ. |
| **Sort** | Sắp xếp dữ liệu theo thứ tự tăng hoặc giảm. |
| **Source system** | Hệ thống nguồn – nơi dữ liệu được tạo ra trong vận hành thực tế. |
| **Sparse** | Dữ liệu thưa – ít tổ hợp khoá xuất hiện so với tất cả khả năng có thể. |
| **Sparsity failure** | Tình trạng bảng tổng hợp (aggregate) không giảm kích thước đáng kể so với bảng gốc. |
| **SQL (Structured Query Language)** | Ngôn ngữ truy vấn chuẩn – dùng để thao tác dữ liệu trong RDBMS. |
| **Star schema** | Mô hình dữ liệu dạng sao – gồm một bảng fact ở trung tâm và các bảng dimension xung quanh. |
| **Stock keeping unit (SKU)** | Mã sản phẩm riêng biệt được dùng để quản lý kho hàng. |
| **Subrogation** | Chuyển quyền đòi bồi thường – thường dùng trong bảo hiểm. |
| **Supply side** | Chuỗi cung ứng – từ mua nguyên vật liệu đến sản xuất và lưu kho. |
| **Surrogate key** | Khóa thay thế – thường là số nguyên tự tăng, không mang ý nghĩa nghiệp vụ. |
| **Syndicated data suppliers** | Nhà cung cấp dữ liệu bên thứ ba – ví dụ: Nielsen, IRI. |

---

### 📘 Glossary Kimball - Thuật ngữ T–Z

| Thuật ngữ | Giải thích |
|----------|------------|
| **Table** | Bảng dữ liệu – tập hợp các dòng (record) và cột (field) trong cơ sở dữ liệu. |
| **Textual fact** | Chỉ số dạng văn bản – ví dụ: nhận xét của khách hàng, mã lý do từ chối... |
| **Third-party provider** | Bên cung cấp dữ liệu hoặc dịch vụ từ ngoài doanh nghiệp. |
| **Third normal form (3NF)** | Dạng chuẩn thứ 3 trong thiết kế CSDL – đảm bảo không dư thừa và dữ liệu nhất quán. |
| **Time dimension** | Dimension thời gian – gồm các cột như ngày, tháng, quý, năm, ngày trong tuần... |
| **Time stamping** | Gắn mốc thời gian – ghi nhận thời điểm diễn ra giao dịch hoặc cập nhật. |
| **Transaction** | Giao dịch – sự kiện đơn lẻ như đơn hàng, gọi món, bấm nút... |
| **Transaction fact table** | Bảng fact ghi nhận từng giao dịch riêng biệt – có độ chi tiết cao nhất. |
| **Transform** | Biến đổi dữ liệu – bước T trong ETL, gồm làm sạch, tính toán, chuẩn hóa. |
| **Type 1 SCD** | Ghi đè dữ liệu cũ bằng dữ liệu mới – không lưu lịch sử. |
| **Type 2 SCD** | Lưu phiên bản lịch sử bằng cách thêm dòng mới và đánh dấu bản hiện tại. |
| **Type 3 SCD** | Lưu một phiên bản cũ song song bản mới – dùng cho so sánh gần nhất. |
| **Unicode** | Bộ mã ký tự toàn cầu – hỗ trợ nhiều ngôn ngữ hơn ASCII. |
| **Unstructured data** | Dữ liệu không có cấu trúc – ví dụ: văn bản, ảnh, video. |
| **Usage tracking** | Ghi nhận hành vi người dùng – để hiểu cách họ tương tác với dữ liệu hoặc hệ thống. |
| **Value-added reseller (VAR)** | Đơn vị phân phối lại sản phẩm có thêm giá trị dịch vụ đi kèm. |
| **Variance** | Chênh lệch – giữa giá trị thực tế và kế hoạch. |
| **View (SQL)** | Bảng ảo – là kết quả của truy vấn SQL, không lưu dữ liệu vật lý. |
| **Warehouse** | Kho dữ liệu – tổ chức dữ liệu phục vụ phân tích, tách biệt hệ thống vận hành. |
| **Web log** | Nhật ký truy cập web – ghi lại các hành vi như URL, thời gian, IP người dùng. |
| **Webhouse** | Dạng kho dữ liệu tích hợp dữ liệu web với dữ liệu doanh nghiệp truyền thống. |
| **Workgroup data mart** | Data mart cho một nhóm người dùng nhỏ trong tổ chức. |
| **Workflow** | Luồng công việc – chuỗi bước xử lý trong ETL hoặc phân tích dữ liệu. |
| **XML (Extensible Markup Language)** | Ngôn ngữ đánh dấu mở rộng – dùng để lưu trữ và trao đổi dữ liệu có cấu trúc. |
| **Y2K** | Sự cố năm 2000 – liên quan đến cách lưu trữ năm bằng 2 chữ số. |
| **Yield** | Hiệu suất – tỷ lệ đầu ra hợp lệ so với đầu vào (sản xuất, tài chính...). |
| **Zip code** | Mã vùng bưu chính – dùng trong phân tích địa lý. |


---

## 🛠 Nguồn & Đóng góp

- 📘 *The Data Warehouse Toolkit – 2nd Edition*, Ralph Kimball & Margy Ross được để cùng trong repo này
- 📄 Phiên bản dịch và trình bày bởi `@tunguyenn99` đến từ [Xóm Data](https://www.facebook.com/groups/1707916343455196)

Bạn có thể đóng góp thêm định nghĩa, ví dụ minh họa hoặc chỉnh sửa bằng cách gửi PR hoặc mở issue trong repo này.

---

🎯 **Hy vọng tài liệu này sẽ giúp bạn hiểu sâu hơn về tư duy Kimball và xây dựng hệ thống dữ liệu hiệu quả hơn!**