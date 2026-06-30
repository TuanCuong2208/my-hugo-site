---
title: "Tuần 6: Di chuyển cơ sở dữ liệu, Nền tảng phân tích và Mô hình hóa NoSQL"
date: 2026-05-26
weight: 6
chapter: false
pre: "<b> 1.6. </b> "
---

### I. Tóm tắt tổng quan (Executive Summary)
Tuần này tập trung vào việc hiện đại hóa cơ sở dữ liệu và xây dựng hệ thống phân tích dữ liệu chuyên sâu trên môi trường đám mây AWS. Nội dung trọng tâm bao gồm quy trình di chuyển cơ sở dữ liệu từ on-premises lên đám mây thông qua bộ công cụ AWS DMS và SCT, xây dựng hạ tầng Data Lake hiệu quả với AWS Glue, tối ưu hóa các mẫu thiết kế truy vấn NoSQL trên DynamoDB. Cuối cùng, thiết lập nền tảng xử lý và phân tích dữ liệu lớn tích hợp đầy đủ từ khâu thu thập (Kinesis), xử lý (EMR) cho tới trực quan hóa báo cáo (QuickSight).

### II. Mục tiêu chiến lược trong tuần (Strategic Objectives)
* **Database Migration:** Làm chủ quy trình chuyển đổi Schema và di chuyển dữ liệu một cách an toàn, tự động từ hệ thống cũ lên AWS.
* **Data Lake Architecture:** Xây dựng và quản lý kho dữ liệu tập trung, tự động phân loại cấu trúc thông qua Data Catalog để chuẩn bị cho các tác vụ phân tích sâu.
* **NoSQL Optimization:** Hiểu sâu về tư duy thiết kế Single-table và tối ưu hóa hiệu suất truy vấn dựa trên các mẫu truy cập (access patterns) thực tế trong DynamoDB.
* **Analytics Automation:** Thiết lập toàn diện một Data Pipeline hoàn chỉnh, kết nối luồng luân chuyển dữ liệu từ thời gian thực cho đến các bảng dashboard trực quan hóa cho doanh nghiệp.

### III. Nhật ký hoạt động & Lộ trình phân bổ chi tiết (Từ 26/05/2026 đến 01/06/2026)

| Thời gian | Danh mục hoạt động | Chi tiết các tác vụ thực hiện chuyên sâu | Kết quả/Minh chứng đạt được |
| :--- | :--- | :--- | :--- |
| **Ngày 1** *(26/05)* | Database Migration | Triển khai Lab 43: Sử dụng AWS Schema Conversion Tool (SCT) để chuyển đổi schema cấu trúc và thiết lập AWS Database Migration Service (DMS) để đồng bộ hóa dữ liệu. | Pipeline di chuyển cơ sở dữ liệu tự động giữa môi trường nguồn và đích được thiết lập thành công. |
| **Ngày 2** *(27/05)* | Data Lake Lifecycle | Triển khai Lab 35: Xây dựng cấu trúc lưu trữ dữ liệu lớn trên Amazon S3, cấu hình AWS Glue Crawler để tự động quét và cập nhật siêu dữ liệu vào Glue Data Catalog. | Kho lưu trữ dữ liệu trung tâm (Data Lake) sẵn sàng phục vụ việc phân loại dữ liệu có cấu trúc và bán cấu trúc. |
| **Ngày 3** *(28/05)* | NoSQL Data Modeling | Triển khai Lab 39: Thực hành thiết kế khóa chính (Primary Key), khóa phân vùng (Partition Key) và các chỉ mục (GSI/LSI) tối ưu hóa mẫu truy xuất ứng dụng trên Amazon DynamoDB. | Schema thực tế được chuẩn hóa, giảm thiểu chi phí RCUs/WCUs và tăng tốc độ phản hồi truy vấn. |
| **Ngày 4** *(29/05)* | Cost & Query Analytics | Triển khai Lab 40: Áp dụng AWS Glue kết hợp với Amazon Athena để quét và thực thi các câu lệnh truy vấn SQL chuẩn trực tiếp trên log hệ thống lưu ở S3. | Trích xuất thành công báo cáo chi tiết về hiệu năng vận hành và phân tích tối ưu chi phí hạ tầng. |
| **Ngày 5-6** *(30-31/05)*| End-to-End Analytics | Triển khai Lab 72: Tích hợp chuỗi dịch vụ phân tích AWS bao gồm Amazon Kinesis (thu thập), Amazon EMR (xử lý dữ liệu lớn) và Amazon QuickSight (trực quan hóa). | Hệ thống xử lý dữ liệu dòng (Stream) hoàn thiện đi kèm Dashboard tương tác trực quan thời gian thực. |
| **Ngày 7** *(01/06)* | Audit & Packaging | Tổng hợp toàn bộ tài liệu kỹ thuật, sắp xếp và kiểm tra đường dẫn tài nguyên hình ảnh chứng minh từ hệ thống, tiến hành deploy phiên bản web cuối cùng lên nền tảng Hugo. | Báo cáo Worklog Tuần 6 được xuất bản trực tuyến ổn định trên GitHub Pages. |

### IV. In-depth Technical Execution & Analysis

#### 1. Lab 43: AWS Database Schema Conversion Tool and Database Migration Service
****1. Technical Overview****
Bài lab này hướng dẫn quy trình di chuyển cơ sở dữ liệu không đồng nhất (heterogeneous database migration) lên hạ tầng đám mây AWS. Quá trình sử dụng AWS Schema Conversion Tool (SCT) để phân tích, đánh giá khả năng tương thích và tự động chuyển đổi các đối tượng schema (views, stored procedures, functions). Sau đó, sử dụng AWS Database Migration Service (DMS) cùng với Replication Instance để thực hiện nạp dữ liệu ban đầu (Full Load) và sao chép các thay đổi theo thời gian thực (CDC), giúp giảm thiểu tối đa thời gian downtime của hệ thống.

****2. Execution Process****
* **Bước 1: Khởi tạo và Cấu hình Môi trường Di chuyển:** Thiết lập Replication Instance trong AWS DMS đóng vai trò là động cơ xử lý dữ liệu. Định nghĩa các điểm cuối kết nối (Source Endpoint cho cơ sở dữ liệu nguồn và Target Endpoint cho cơ sở dữ liệu đích trên AWS) và kiểm tra kết nối mạng thành công.
* **Bước 2: Chuyển đổi Cấu trúc Schema bằng AWS SCT:** Cài đặt và sử dụng AWS SCT để kết nối tới cơ sở dữ liệu nguồn, tạo báo cáo đánh giá di chuyển (Migration Assessment Report) để xác định các đoạn mã không tương thích, tiến hành chuyển đổi schema và áp dụng cấu trúc mới lên cơ sở dữ liệu đích.
* **Bước 3: Tạo và Vận hành DMS Migration Task:** Cấu hình Database Migration Task với chế độ di chuyển dữ liệu phù hợp, thiết lập quy tắc lựa chọn bảng (Table mappings) để chỉ định chính xác các dữ liệu cần đồng bộ, kích hoạt task và giám sát tiến độ cho đến khi trạng thái chuyển sang hoàn thành toàn bộ.

****3. Proofs****
* **1.png:** Ảnh màn hình giao diện phần mềm AWS SCT hiển thị báo cáo đánh giá di chuyển (Assessment Report) cùng cấu trúc Schema nguồn và đích sau khi chuyển đổi thành công.
* **2.png:** Ảnh chụp trạng thái hoạt động của các Endpoint trong AWS DMS Console, xác nhận Source Endpoint và Target Endpoint hiển thị trạng thái kết nối thành công (`Successful`).
* **3.png:** Ảnh kết quả vận hành của Database Migration Task hiển thị trạng thái hoạt động `Load complete` với thông số chi tiết về số lượng dòng (rows) dữ liệu đã được dịch chuyển thành công sang DB đích.

---

#### 2. Lab 35: Data Lake on AWS
****1. Technical Overview****
Kiến trúc Data Lake trên AWS cung cấp giải pháp lưu trữ tập trung, bảo mật và có khả năng mở rộng vô hạn cho mọi loại dữ liệu thô (cấu trúc, bán cấu trúc và phi cấu trúc). Bài học tập trung vào việc lưu trữ dữ liệu trên Amazon S3, kết hợp với dịch vụ AWS Glue để xây dựng kho siêu dữ liệu tập trung (Glue Data Catalog), giúp các dịch vụ phân tích cấp cao có thể hiểu và truy vấn dữ liệu trực tiếp mà không cần nạp lại.

****2. Execution Process****
* **Bước 1: Tổ chức Kiến trúc Lưu trữ S3:** Thiết lập các S3 bucket đại diện cho các phân tầng dữ liệu thô (Raw Data Lake) và dữ liệu đã qua xử lý chuẩn hóa.
* **Bước 2: Cấu hình và Vận hành AWS Glue Crawler:** Định nghĩa IAM Role phù hợp cấp quyền cho Glue truy cập dữ liệu S3. Khởi tạo một Glue Crawler trỏ trực tiếp vào S3 dữ liệu thô để tự động quét cấu trúc tệp dữ liệu.
* **Bước 3: Kiểm tra và Chuẩn hóa Glue Data Catalog:** Chạy Crawler để dịch vụ tự động nhận diện lược đồ dữ liệu (schema inference), tạo lập cơ sở dữ liệu logic và các bảng tương ứng bên trong kho lưu trữ dữ liệu trung tâm Glue Data Catalog.

****3. Proofs****
* **4.png:** Ảnh màn hình Amazon S3 Console hiển thị danh sách các bucket lưu trữ dữ liệu và cấu trúc thư mục chứa các tệp dữ liệu thô đầu vào của Data Lake.
* **5.png:** Ảnh màn hình chi tiết Table Schema bên trong AWS Glue Data Catalog sau khi Crawler chạy xong, hiển thị đầy đủ tên các cột dữ liệu (Columns) và định dạng kiểu dữ liệu (Data types) thu thập được.

---

#### 3. Lab 39: Amazon DynamoDB Immersion Day
****1. Technical Overview****
Amazon DynamoDB là dịch vụ cơ sở dữ liệu NoSQL Key-Value và Document được quản lý hoàn toàn, mang lại hiệu năng độ trễ dưới 10 mili-giây ở mọi quy mô. Bài lab đi sâu vào tư duy thiết kế mô hình hóa dữ liệu NoSQL nâng cao, tập trung vào việc xác định các mẫu truy cập của ứng dụng ứng với cách thiết lập Khóa chính (Primary Key), Khóa phân vùng (Partition Key), Khóa sắp xếp (Sort Key) và các Chỉ mục thứ cấp (GSI/LSI) nhằm tối ưu hiệu năng và tiết kiệm chi phí vận hành.

****2. Execution Process****
* **Bước 1: Khởi tạo và Định nghĩa Bảng DynamoDB:** Tạo bảng dữ liệu mới trên DynamoDB, lựa chọn chế độ quản lý tài nguyên (Provisioned hoặc On-Demand) và chỉ định thuộc tính làm khóa phân vùng cốt lõi cho thực thể dữ liệu.
* **Bước 2: Thiết kế Access Patterns nâng cao:** Thực hành xây dựng các Global Secondary Indexes (GSI) để hỗ trợ các câu lệnh truy vấn ngoài cấu trúc khóa chính thông thường, cho phép ứng dụng truy xuất linh hoạt theo nhiều chiều dữ liệu khác nhau.
* **Bước 3: Thực thi Truy xuất Dữ liệu:** Sử dụng giao diện Console hoặc các câu lệnh CLI thông qua AWS CloudShell để thực hiện các tác vụ Query và Scan dữ liệu, kiểm tra tính chính xác của kết quả và lượng RCUs tiêu thụ.

****3. Proofs****
* **6.png:** Ảnh màn hình chi tiết thông số cấu hình bảng trên giao diện DynamoDB Console, hiển thị rõ cấu trúc Partition Key, Sort Key và danh sách các chỉ mục GSI đã được thiết lập thành công.
* **7.png:** Ảnh kết quả trả về của các tác vụ truy vấn (Query/Scan items) hiển thị trực quan các bản ghi dữ liệu có trong bảng thông qua giao diện quản lý DynamoDB Items hoặc từ AWS CloudShell.

---

#### 4. Lab 40: Cost and Performance Analysis with AWS Glue and Amazon Athena
****1. Technical Overview****
Hệ thống kết hợp giữa AWS Glue và Amazon Athena tạo nên giải pháp phân tích dữ liệu phi máy chủ (Serverless Analytics) vô cùng mạnh mẽ và tối ưu chi phí. AWS Glue Crawler chịu trách nhiệm tự động hóa việc trích xuất và định nghĩa cấu trúc từ các tệp log thô (như log chi phí, log hệ thống) lưu trên S3, trong khi Amazon Athena cho phép người dùng chạy trực tiếp các câu lệnh truy vấn SQL tiêu chuẩn để phân tích sâu hiệu suất hệ thống mà không cần quản lý hay duy trì bất kỳ máy chủ nào.

****2. Execution Process****
* **Bước 1: Cấu hình Glue Crawler quét Log hệ thống:** Thiết lập một Crawler chuyên dụng trỏ tới thư mục lưu trữ các tệp log vận hành hoặc log chi phí trên Amazon S3 để bắt đầu quá trình đồng bộ lược đồ.
* **Bước 2: Áp dụng Chuyển đổi sang dạng Cột (Columnar format):** Tìm hiểu cơ chế tối ưu hiệu năng thông qua việc chuyển đổi dữ liệu log từ dạng thô (CSV/JSON) sang định dạng lưu trữ dạng cột (Parquet) nhằm giảm lượng dữ liệu cần quét.
* **Bước 3: Thực thi Serverless SQL Queries trên Athena:** Mở trình biên dịch câu lệnh Amazon Athena, lựa chọn Database và Table được ánh xạ từ Glue Data Catalog, thực hiện viết các câu lệnh SELECT, WHERE để phân tích chi phí và hiệu suất.

****3. Proofs****
* **8.png:** Ảnh màn hình trạng thái vận hành của AWS Glue Crawler hiển thị trạng thái `Ready` hoặc lịch trình chạy quét log thành công vào Data Catalog.
* **9.png:** Ảnh chụp giao diện Query Editor của Amazon Athena hiển thị chi tiết câu lệnh SQL đã thực thi thành công, kết quả bảng dữ liệu đầu ra và các thông số đo lường bao gồm thời gian chạy (Run time), dung lượng dữ liệu đã quét (Data scanned).

---

#### 5. Lab 72: Analytics on AWS Workshop
****1. Technical Overview****
Kiến trúc luồng xử lý phân tích dữ liệu toàn diện (End-to-End Analytics Pipeline) trên AWS giải quyết bài toán xử lý dữ liệu lớn từ khâu thu thập đến báo cáo kinh doanh. Hệ thống tích hợp Amazon Kinesis Data Streams để tiếp nhận luồng dữ liệu thời gian thực với tốc độ cao, chuyển tiếp sang Amazon EMR (Elastic MapReduce) để thực hiện tính toán, xử lý phân tán song song quy mô lớn dựa trên Apache Spark/Hadoop, và cuối cùng kết nối với Amazon QuickSight để trực quan hóa thành các chỉ số thông minh.

****2. Execution Process****
* **Bước 1: Khởi tạo Luồng thu thập Kinesis Data Streams:** Thiết lập luồng luân chuyển dữ liệu Kinesis, cấu hình số lượng Shards để đảm bảo băng thông tiếp nhận dữ liệu liên tục từ các nguồn phát (Data Generators).
* **Bước 2: Triển khai Cụm xử lý Dữ liệu lớn Amazon EMR:** Khởi chạy cụm máy chủ Amazon EMR với các phần mềm mã nguồn mở cốt lõi, cấu hình các tiến trình bước (EMR Steps) để thực thi ứng dụng lọc, biến đổi cấu trúc dữ liệu thô thành dữ liệu phân tích.
* **Bước 3: Kết nối và Trực quan hóa trên Amazon QuickSight:** Đăng nhập không gian QuickSight, tạo một tập dữ liệu (Data set) kết nối trực tiếp với nguồn dữ liệu đã xử lý và thiết lập các biểu đồ đồ thị (Visuals) để hoàn thiện Dashboard.

****3. Proofs****
* **10.png:** Ảnh màn hình bảng điều khiển Amazon Kinesis Data Streams hiển thị các biểu đồ giám sát kỹ thuật (CloudWatch metrics) chứng minh luồng dữ liệu thô đang được đổ về hệ thống một cách liên tục và ổn định.
* **11.png:** Ảnh chụp giao diện Dashboard phân tích nghiệp vụ hoàn chỉnh và tương tác trực quan trên môi trường làm việc của Amazon QuickSight.

---

### V. Infrastructure Challenges, Error Resolution Logs & Expert Perspectives
*(Mục này sẽ được phân tích sâu và ghi nhận chi tiết về các lỗi hệ thống phát sinh sau khi hoàn thành toàn bộ các bài Lab trên)*

### VI. Professional Reflections
*(Mục này sẽ ghi lại các bài học kinh nghiệm cá nhân rút ra sau quá trình thực hành thực tế)*

### VII. Strategic Planning & Optimization Roadmap for Next Week
*(Mục này sẽ vạch ra kế hoạch hành động tiếp theo dựa trên tiến độ tuần này)*