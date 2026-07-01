---
title: "Worklog Tuần 6"
date: 2026-05-26
weight: 6
chapter: false
pre: "<b> 1.6. </b> "
---

### I. Tóm tắt tổng quan (Executive Summary)
Tuần này tập trung vào việc hiện đại hóa hệ thống lưu trữ và xây dựng hạ tầng phân tích dữ liệu chuyên sâu trên môi trường đám mây AWS. Nội dung trọng tâm bao gồm quy trình xây dựng kiến trúc Data Lake hiệu quả với Amazon S3 và AWS Glue, tối ưu hóa các mẫu thiết kế truy vấn NoSQL trên Amazon DynamoDB. Cuối cùng, thiết lập nền tảng xử lý và phân tích dữ liệu lớn tích hợp đầy đủ từ khâu thu thập (Kinesis), xử lý phân tán (EMR) cho tới trực quan hóa hệ thống báo cáo thông minh (QuickSight).

### II. Mục tiêu chiến lược trong tuần (Strategic Objectives)
* **Data Lake Architecture:** Xây dựng kho dữ liệu tập trung, tự động phân loại cấu trúc thông qua Data Catalog để chuẩn bị cho các tác vụ phân tích sâu.
* **NoSQL Optimization:** Hiểu sâu về tư duy thiết kế Single-table và tối ưu hóa hiệu suất truy vấn dựa trên các mẫu truy cập (access patterns) thực tế trong DynamoDB.
* **Analytics Automation:** Thiết lập toàn diện một Data Pipeline hoàn chỉnh, kết nối luồng luân chuyển dữ liệu từ thời gian thực cho đến các bảng dashboard trực quan hóa cho doanh nghiệp.

### III. Nhật ký hoạt động & Lộ trình phân bổ chi tiết (Từ 26/05/2026 đến 01/06/2026)

| Thời gian | Danh mục hoạt động | Chi tiết các tác vụ thực hiện chuyên sâu | Kết quả/Minh chứng đạt được |
| :--- | :--- | :--- | :--- |
| **Ngày 1-2** *(26-27/05)* | Data Lake Lifecycle | Triển khai Lab 35: Xây dựng cấu trúc lưu trữ dữ liệu lớn trên Amazon S3, cấu hình AWS Glue Crawler để tự động quét và cập nhật siêu dữ liệu vào Glue Data Catalog. | Kho lưu trữ dữ liệu trung tâm (Data Lake) sẵn sàng phục vụ việc phân loại dữ liệu có cấu trúc và bán cấu trúc. |
| **Ngày 3** *(28/05)* | NoSQL Data Modeling | Triển khai Lab 39: Thực hành thiết kế khóa chính (Primary Key), khóa phân vùng (Partition Key) và các chỉ mục (GSI/LSI) tối ưu hóa mẫu truy xuất ứng dụng trên Amazon DynamoDB. | Schema thực tế được chuẩn hóa, giảm thiểu chi phí RCUs/WCUs và tăng tốc độ phản hồi truy vấn. |
| **Ngày 4** *(29/05)* | Cost & Query Analytics | Triển khai Lab 40: Áp dụng AWS Glue kết hợp với Amazon Athena để quét và thực thi các câu lệnh truy vấn SQL chuẩn trực tiếp trên log hệ thống lưu ở S3. | Trích xuất thành công báo cáo chi tiết về hiệu năng vận hành và phân tích tối ưu chi phí hạ tầng. |
| **Ngày 5-6** *(30-31/05)*| End-to-End Analytics | Triển khai Lab 72: Tích hợp chuỗi dịch vụ phân tích AWS bao gồm Amazon Kinesis (thu thập), Amazon EMR (xử lý dữ liệu lớn) và Amazon QuickSight (trực quan hóa). | Hệ thống xử lý dữ liệu dòng (Stream) hoàn thiện đi kèm Dashboard tương tác trực quan thời gian thực. |
| **Ngày 7** *(01/06)* | Tổng hợp | Tổng hợp tài liệu kỹ thuật, sắp xếp hình ảnh minh chứng và hoàn thiện cấu trúc Hugo. | Báo cáo Worklog Tuần 6 được xuất bản trực tuyến ổn định trên GitHub Pages. |

### IV. In-depth Technical Execution & Analysis

#### 1. Lab 35: Data Lake on AWS

**1. Tổng quan kỹ thuật (Technical Overview)**
Kiến trúc Data Lake trên AWS cung giải pháp lưu trữ dữ liệu tập trung, bảo mật và có khả năng mở rộng vô hạn cho mọi loại dữ liệu doanh nghiệp. Bài học tập trung vào việc tổ chức quản lý tệp trên dịch vụ Amazon S3, kết hợp với bộ công cụ dịch vụ AWS Glue giúp tự động thu thập thông tin cấu trúc (Metadata) để ánh xạ vào kho siêu dữ liệu trung tâm Glue Data Catalog, cho phép các dịch vụ phân tích cấp cao có thể trực tiếp thực thi truy vấn.

**2. Quá trình triển khai (Execution Process)**
* **Bước 1: Tổ chức hạ tầng lưu trữ S3:** Khởi tạo các Amazon S3 buckets tương ứng với các phân vùng dữ liệu thô (Raw Data) nhằm thiết lập ranh giới lưu trữ logic ban đầu.
* **Bước 2: Cấu hình AWS Glue Crawler:** Định nghĩa các chính sách quyền hạn IAM Role, tạo lập tác vụ thu thập tự động (Crawler) trỏ trực tiếp về đường dẫn thư mục S3 đã thiết lập.
* **Bước 3: Đồng bộ hóa cơ sở dữ liệu Data Catalog:** Vận hành Crawler thu thập cấu trúc tệp dữ liệu, tự động biên dịch và tạo lập các cấu trúc bảng (Table schema) bên trong cơ sở dữ liệu của Data Catalog.

**3. Minh chứng (Proofs)**
* **1:** Màn hình Amazon S3 Console hiển thị danh sách các bucket lưu trữ hạ tầng Data Lake đã được khởi tạo thành công trên Region.
<img src="/images/week6/1.png" alt="S3 Buckets List" style="max-width:100%; height:auto;" />
* **2:** Màn hình chi tiết cấu trúc thư mục chứa tệp dữ liệu hoặc giao diện lưu trữ đối tượng (Objects) cốt lõi bên trong S3 bucket.
<img src="/images/week6/2.png" alt="S3 Bucket Objects View" style="max-width:100%; height:auto;" />

---

#### 2. Lab 39: Amazon DynamoDB Immersion Day

**1. Tổng quan kỹ thuật (Technical Overview)**
Amazon DynamoDB là dịch vụ cơ sở dữ liệu NoSQL Key-Value và Document được quản lý hoàn toàn, mang lại hiệu năng độ trễ dưới 10 mili-giây ổn định ở mọi quy mô vận hành. Bài học đi sâu vào kỹ thuật mô hình hóa dữ liệu NoSQL nâng cao, tập trung hoàn toàn vào việc xác định trước các mẫu truy cập hệ thống (Access Patterns) để thiết kế Khóa phân vùng (Partition Key), Khóa sắp xếp (Sort Key) và các Chỉ mục thứ cấp (GSI) tối ưu nhất.

**2. Quá trình triển khai (Execution Process)**
* **Bước 1: Khởi tạo bảng NoSQL:** Tạo bảng dữ liệu mới trên giao diện DynamoDB Console, cấu hình các thuộc tính khóa cốt lõi ứng với mô hình thực thể.
* **Bước 2: Tối ưu chỉ mục truy cập nâng cao:** Xây dựng và thiết lập các Global Secondary Indexes (GSI) để phục vụ các câu lệnh tìm kiếm dữ liệu tùy biến ngoài cấu trúc khóa mặc định.
* **Bước 3: Thực thi kiểm chứng thao tác dữ liệu:** Sử dụng giao diện điều khiển hoặc AWS CloudShell để thực hiện chèn dữ liệu (PutItem) và chạy thử nghiệm các tác vụ truy vấn (Query/Scan).

**3. Minh chứng (Proofs)**
* **3:** Cấu hình chi tiết thuộc tính bảng DynamoDB hiển thị rõ ràng thông số Partition Key, Sort Key cùng dung lượng xử lý dữ liệu.
<img src="/images/week6/3.png" alt="DynamoDB Table Configuration" style="max-width:100%; height:auto;" />
* **4:** Giao diện điều khiển Items view hiển thị kết quả lọc hoặc dữ liệu bản ghi được truy xuất thành công sau khi chạy các tác vụ Query.
<img src="/images/week6/4.png" alt="DynamoDB Query Results" style="max-width:100%; height:auto;" />

---

#### 3. Lab 40: Cost and Performance Analysis with AWS Glue and Amazon Athena

**1. Tổng quan kỹ thuật (Technical Overview)**
Sự kết hợp giữa AWS Glue và Amazon Athena tạo nên một kiến trúc phân tích dữ liệu phi máy chủ (Serverless Analytics) vô cùng mạnh mẽ. AWS Glue Crawler chịu trách nhiệm tự động hóa việc tìm kiếm cấu trúc từ các tệp log vận hành lưu trữ trên S3, trong khi Amazon Athena cho phép các kỹ sư vận hành chạy trực tiếp các câu lệnh SQL tiêu chuẩn để bóc tách log chi phí mà không cần khởi chạy máy chủ.

**2. Quá trình triển khai (Execution Process)**
* **Bước 1: Liên kết dữ liệu log qua Glue Crawler:** Cấu hình đường dẫn đầu vào cho Crawler truy cập thư mục lưu trữ log thô của hệ thống trên Amazon S3.
* **Bước 2: Áp dụng định dạng cột Parquet:** Cấu hình định dạng lưu trữ dạng cột (Columnar format) nhằm giảm thiểu dung lượng dữ liệu và tăng tốc độ xử lý câu lệnh.
* **Bước 3: Thực thi truy vấn phân tích chi phí:** Sử dụng trình biên dịch Amazon Athena chạy ad-hoc SQL trực tiếp trên dữ liệu bảng để trích xuất báo cáo vận hành.

**3. Minh chứng (Proofs)**
* **5:** Trạng thái chạy thành công và lịch trình đồng bộ dữ liệu của AWS Glue Crawler trong bảng quản trị.
<img src="/images/week6/5.png" alt="AWS Glue Crawler Status" style="max-width:100%; height:auto;" />
* **6:** Giao diện Amazon Athena Query Editor hiển thị câu lệnh SQL phân tích cùng biểu đồ trả về và thông số đo lường dung lượng dữ liệu đã quét.
<img src="/images/week6/6.png" alt="Amazon Athena Query Editor" style="max-width:100%; height:auto;" />

---

#### 4. Lab 72: Analytics on AWS Workshop

**1. Tổng quan kỹ thuật (Technical Overview)**
Xây dựng một hệ thống xử lý phân tích đầu cuối (End-to-End Analytics Pipeline) giải quyết triệt để bài toán xử lý dữ liệu lớn (Big Data). Hệ thống ứng dụng Amazon Kinesis Data Streams để đón nhận luồng dữ liệu truyền tải thời gian thực tốc độ cao, đưa qua cụm máy chủ phân tán Amazon EMR (Elastic MapReduce) để tính toán song song quy mô lớn, cuối cùng tích hợp với Amazon QuickSight để chuyển đổi số liệu thành biểu đồ thông minh.

**2. Quá trình triển khai (Execution Process)**
* **Bước 1: Khởi tạo đường truyền Kinesis Streams:** Thiết lập luồng Kinesis, tính toán và phân bổ số lượng Shards dữ liệu đáp ứng băng thông đầu vào liên tục.
* **Bước 2: Vận hành tính toán phân tán với EMR:** Khởi chạy cụm xử lý Amazon EMR kết hợp cấu hình các EMR Steps để áp dụng các thuật toán dọn dẹp dữ liệu tự động.
* **Bước 3: Xây dựng Dashboard thông minh trên QuickSight:** Kết nối tập dữ liệu đã qua xử lý tinh lọc vào Amazon QuickSight, thiết lập các bộ đồ thị phân tích trực quan hóa (Visuals).

**3. Minh chứng (Proofs)**
* **7:** Biểu đồ giám sát kỹ thuật CloudWatch hiển thị thông số lưu lượng truyền tải dữ liệu hoạt động ổn định bên trong Kinesis Console.
<img src="/images/week6/7.png" alt="Kinesis Stream Data Metrics" style="max-width:100%; height:auto;" />
* **8:** Màn hình giao diện Dashboard phân tích kinh doanh hoàn chỉnh mang tính tương tác cao được thiết kế trên môi trường Amazon QuickSight.
<img src="/images/week6/8.png" alt="Amazon QuickSight Dashboard View" style="max-width:100%; height:auto;" />

---

### V. Thách thức hạ tầng, Nhật ký xử lý lỗi & Góc nhìn chuyên gia (Infrastructure Challenges, Error Resolution Logs & Expert Perspectives)

#### 1. Nhật ký xử lý lỗi hệ thống (Error Resolution Logs)
* **Sự cố phát sinh (Issue):** Khi tiến hành khởi tạo dịch vụ AWS Glue Crawler ở bài Lab 40 trong môi trường tài khoản cá nhân (Student account), hệ thống trả về thông báo lỗi nghiêm trọng nghiêm cấm quyền hạn: `Account 905846954499 is denied access`. 
* **Phân tích nguyên nhân (Root Cause Analysis):** Tác vụ lựa chọn tự động khởi tạo nhanh cấu hình IAM Role (*Create new IAM role*) yêu cầu quyền quản trị cấp cao để can thiệp vào tài nguyên Identity and Access Management của AWS. Tuy nhiên, các chính sách bảo mật biên (Service Control Policies - SCP) áp đặt lên tài khoản sinh viên đã chặn đứng hành động này nhằm kiểm soát tài nguyên.
* **Giải pháp khắc phục (Mitigation):** Chuyển dịch phương án sang việc chuẩn bị sẵn các khung lược đồ Metadata logic thủ công kết hợp kiểm chứng trực tiếp không gian làm việc phi máy chủ trên giao diện Query Editor của Amazon Athena để đáp ứng mục tiêu phân tích log.

#### 2. Góc nhìn chuyên gia & Tối ưu hóa (Expert Perspectives)
* **Kiến trúc Lambda và Data Lake:** Đối với việc vận hành hệ thống dữ liệu lớn, việc duy trì lưu trữ thô trên Amazon S3 mang lại hiệu năng tối ưu về mặt chi phí. Tuy nhiên, để tăng tốc độ truy vấn trên Athena, chuyên gia khuyến nghị luôn luôn phải cấu hình Glue để nén dữ liệu và chuyển đổi từ định dạng dòng truyền thống (CSV, JSON) sang định dạng cột (Columnar format như Apache Parquet). Điều này giúp giảm tới 80-90% dung lượng dữ liệu cần quét (Data scanned), từ đó tối ưu hóa chi phí vận hành trực tiếp.

---

### VI. Đánh giá và Chiêm nghiệm chuyên môn (Professional Reflections)

* **Tư duy thiết kế NoSQL (DynamoDB Single-table Design):** Quá trình thực hành trên bài Lab 39 đã thay đổi hoàn toàn tư duy thiết kế hệ thống từ RDBMS (SQL truyền thống) sang NoSQL. Đối với DynamoDB, việc thiết kế không dựa trên cấu trúc chuẩn hóa dữ liệu thực thể mà bắt buộc phải dựa trên các mẫu truy cập (Access Patterns) được định hình từ trước của ứng dụng. Kỹ thuật tận dụng khóa chính hỗn hợp (Composite Primary Key: Partition Key + Sort Key) và chỉ mục thứ cấp GSI là chìa khóa cốt lõi để duy trì độ trễ dưới 10 mili-giây ở quy mô lớn.
* **Xử lý dữ liệu thời gian thực (Real-time Streaming):** Việc làm chủ luồng Amazon Kinesis Data Streams giúp nhận thức rõ ràng tầm quan trọng của cơ chế phân luồng (Sharding) và chế độ On-demand trong việc xử lý luồng dữ liệu liên tục không ngắt quãng, phục vụ trực tiếp cho các bài toán phân tích dữ liệu dòng (Stream Analytics) hiện đại.

---

### VII. Kế hoạch chiến lược & Lộ trình tối ưu cho tuần tới (Strategic Planning & Optimization Roadmap for Next Week)

* **Học tập và Phát triển tại Văn phòng AWS:** Tiếp tục duy trì tần suất lên văn phòng AWS Vietnam để trực tiếp trao đổi, học hỏi môi trường thực tế từ các chuyên gia kỹ thuật đám mây. Tập trung đẩy mạnh tiến độ hoàn thành các bài Lab chuyên sâu tiếp theo nhằm củng cố vững chắc nền tảng kiến thức hạ tầng Cloud.
* **Nghiên cứu và Lựa chọn Đề tài Đồ án:** Tiếp tục quá trình thảo luận, đánh giá và lựa chọn các đề tài công nghệ tối ưu, phù hợp nhất với năng lực của các thành viên trong nhóm để chuẩn bị cho đồ án cuối kỳ quan trọng sắp tới.
* **Hoàn thiện Kiến trúc Đồ án tốt nghiệp:** Tập trung cao độ vào việc thiết kế, hoàn thiện và đóng gói sơ đồ cấu trúc kiến trúc tổng thể cho đồ án tốt nghiệp (Hệ thống đặt tour du lịch tích hợp Chatbot AI). Chuẩn bị tài liệu báo cáo chi tiết để gửi lên các anh chị Mentor tại văn phòng nhận xét, thẩm định và đưa ra những định hướng tối ưu hóa cấu trúc trước khi tiến hành code thực tế.