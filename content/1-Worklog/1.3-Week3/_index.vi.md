---
title: "Tuần 3: Mở rộng Kiến trúc Mạng nâng cao, Hybrid DNS và Quản trị AWS CLI Enterprise"
date: 2026-05-05
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

# Tuần 3: Làm chủ Mạng ảo Nâng cao, Tích hợp Hybrid DNS Resolver và Tự động hóa Hạ tầng bằng Dòng lệnh

### I. Tóm tắt tổng quan
Tuần này đánh dấu một bước chuyển mình mang tính chiến lược trong lộ trình thực tập chương trình First Cloud AI Journey – Workforce Bootcamp 2026 tại Văn phòng AWS Việt Nam. Tôi đã dịch chuyển từ việc thiết kế hạ tầng đơn tầng sang việc xây dựng hệ thống mạng doanh nghiệp phức hợp đa tầng và kết nối lai qua 6 bài Lab lớn: Lab 7 (Kiến trúc Subnet nội bộ), Lab 8 (VPC Routing & Ingress Gateways), Lab 10 (Route 53 Hybrid DNS Resolver), Lab 11 (Quản trị bằng AWS CLI), Lab 13 (Advanced VPC Topology đa tầng cách ly), và Lab 14 (Elastic Load Balancing cân bằng tải).

### II. Mục tiêu chiến lược trong tuần
* **Phân tầng mạng lưới cô lập (Advanced VPC Engineering):** Thiết kế cấu trúc liên kết mạng nhiều lớp chuyên sâu, chia nhỏ phân vùng để cô lập hoàn toàn lớp cơ sở dữ liệu và backend khỏi lớp Web công khai.
* **Tích hợp mạng đám mây hỗn hợp (Hybrid Cloud DNS):** Hiện thực hóa cơ chế phân giải tên miền hai chiều giữa Cloud và On-Premises thông qua Route 53 Resolver, bảo vệ kiến trúc đặt tên nội bộ.
* **Tự động hóa bằng mã lệnh (CLI Automation):** Làm chủ giao diện dòng lệnh AWS CLI kết hợp bộ lọc JSON JMESPath để trích xuất dữ liệu hạ tầng quy mô lớn mà không phụ thuộc vào Web Console.
* **Phân phối lưu lượng sẵn sàng cao (High Availability):** Thiết lập Elastic Load Balancing để tự động hóa điều hướng luồng dữ liệu, loại bỏ điểm sập đơn lẻ (SPOF) cho hệ thống ứng dụng.

---

### III. Nhật ký hoạt động & Lộ trình phân bổ chi tiết (Từ 05/05/2026 đến 11/05/2026)

| Thời gian | Danh mục hoạt động | Chi tiết các tác vụ thực hiện chuyên sâu | Kết quả/Minh chứng đạt được |
| :--- | :--- | :--- | :--- |
| **Ngày 1** *(05/05)* | Kiến trúc Subnet | Khởi tạo VPC tùy chỉnh và quy hoạch các phân vùng Subnets công cộng, nội bộ dự phòng Multi-AZ. (Lab 7) | Hạ tầng mạng nền tảng sẵn sàng, phân chia ranh giới logic an toàn. |
| **Ngày 2** *(06/05)* | Định tuyến Ingress | Khởi tạo Internet Gateway (IGW), liên kết VPC và tùy chỉnh cấu trúc Route Tables công khai trỏ ra internet. (Lab 8) | Thông mạng internet hai chiều cho các phân vùng Edge thành công. |
| **Ngày 3-4** *(07-08/05)* | Liên kết Hybrid DNS | Khởi tạo Private Hosted Zone, thiết lập cấu hình Route 53 Resolver Inbound/Outbound Endpoints Multi-AZ và rà soát FinOps dọn dẹp tài nguyên. (Lab 10) | Phân giải thành công tên miền nội bộ hai chiều đám mây - doanh nghiệp. |
| **Ngày 4** *(08/05)* | Quản trị CLI | Vượt qua giới hạn CloudShell, cấu hình xác thực terminal cục bộ, thực thi truy vấn trích xuất dữ liệu EC2 bằng bộ lọc JMESPath định dạng bảng. (Lab 11) | Kiểm soát tài nguyên qua dòng lệnh, loại bỏ dữ liệu JSON cồng kềnh. |
| **Ngày 5** *(09/05)* | Mạng nâng cao đa lớp | Triển khai mô hình Advanced VPC Topology, phân phối Subnet nhiều tầng để cách ly triệt để lớp DB nhạy cảm khỏi Web Server. (Lab 13) | Ranh giới an ninh mạng được thiết lập vững chắc qua nhiều lớp bảo vệ. |
| **Ngày 6** *(10/05)* | Cân bằng tải | Khởi tạo Elastic Load Balancing (ELB) điều phối traffic thông minh đến các Web Instances nền tảng. (Lab 14) | Hệ thống đạt trạng thái sẵn sàng cao, loại bỏ rủi ro sập cục bộ. |
| **Ngày 7** *(11/05)* | Đóng gói báo cáo | Biên soạn tài liệu kỹ thuật, chuyển đổi toàn bộ mã nguồn ảnh sang thẻ HTML tĩnh, đóng gói Portfolio trên nền tảng Hugo. | Nhật ký công việc Tuần 3 hoạt động xanh sạch trên GitHub Pages. |

---

### IV. Thực thi kỹ thuật chuyên sâu & Phân tích chi tiết qua 6 bài Lab

#### **1. Lab 7: Amazon CloudWatch & AWS Budgets - Thiết lập Ngân sách Doanh nghiệp và Hệ thống Cảnh báo Giám sát**

##### **Tổng quan (Overview)**
Yêu cầu cốt lõi của bất kỳ triển khai hạ tầng đám mây cấp doanh nghiệp nào là kiểm soát chặt chẽ chi phí vận hành và thiết lập hệ thống giám sát tài nguyên chủ động. Trong bài Lab này, tôi đã xây dựng cấu trúc nền tảng **AWS Budgets** nhằm quản lý ranh giới tài chính và **Amazon CloudWatch** để theo dõi hiệu năng hệ thống theo thời gian thực, ngăn ngừa rủi ro phát sinh chi phí ngoài tầm kiểm soát.

##### **Khái niệm cốt lõi (Core Concepts)**
* **AWS Budgets:** Công cụ quản trị FinOps cho phép thiết lập các hạn mức chi phí tùy chỉnh, theo dõi chu kỳ gia hạn định kỳ (Monthly Recurring) và tự động tính toán các kịch bản dự báo tiêu hao tài chính.
* **CloudWatch Metrics & Alarms:** Hệ thống thu thập chỉ số vận hành (như `CPUUtilization`). Khi tài nguyên vượt ngưỡng cấu hình (Threshold), hệ thống sẽ lập tức kích hoạt trạng thái báo động (`ALARM`) và gửi thông báo qua Amazon SNS.

##### **Quá trình triển khai chi tiết (Step-by-step Execution)**

###### **Bước 1: Cấu hình hạn mức chi phí và bộ lọc bộ định tuyến tài chính**
Tôi tiến hành khởi tạo một chính sách ngân sách cố định hàng tháng với hạn mức `20.00 USD`. Hệ thống được thiết lập bộ lọc nâng cao tập trung vào chiều chi phí của dịch vụ máy chủ ảo EC2 để kiểm soát triệt để các workload thử nghiệm.
<img src="/images/week3/1.png" alt="Cấu hình hạn mức chi phí ngân sách AWS Budgets" style="max-width:100%; height:auto;" />

###### **Bước 2: Thiết lập các ngưỡng cảnh báo tài chính đa tầng**
Để đảm bảo an toàn, tôi cấu hình 3 tầng cảnh báo dựa trên tỷ lệ phần trăm tiêu hao: bộ cảnh báo số 1 kích hoạt khi chi phí dự báo (Forecasted) chạm ngưỡng 80%, bộ số 2 chạm mức 100% chi phí dự báo, và bộ số 3 kích hoạt ngay khi chi phí thực tế (Actual) vượt quá 100% hạn mức.
<img src="/images/week3/2.png" alt="Rà soát cấu trúc các tầng cảnh báo tài chính" style="max-width:100%; height:auto;" />

###### **Bước 3: Xác thực trạng thái hoạt động của hệ thống quản lý ngân sách**
Chính sách ngân sách mang tên `My AWS budget` được khởi tạo thành công trên bảng điều khiển. Trạng thái hiển thị xanh sạch (`OK` và `Healthy`) xác nhận hệ thống FinOps đã bắt đầu theo dõi dòng tiền tài khoản đám mây.
<img src="/images/week3/3.png" alt="Xác thực trạng thái kích hoạt ngân sách thành công" style="max-width:100%; height:auto;" />

###### **Bước 4: Xây dựng Dashboard giám sát hiệu năng CPU thực tế**
Chuyển sang cấu phần giám sát hạ tầng, tôi khởi tạo một bảng điều khiển tùy chỉnh `EC2-Monitor-Dashboard` trên Amazon CloudWatch, thực hiện cấu hình widget đồ thị để liên tục kéo về chỉ số tiêu hao vi xử lý (`CPUUtilization`).
<img src="/images/week3/4.png" alt="Dashboard theo dõi đồ thị metric CPUUtilization trên CloudWatch" style="max-width:100%; height:auto;" />

###### **Bước 5: Cấu hình bộ Alarm cảnh báo quá tải vi xử lý**
Tôi thiết lập một bộ cảnh báo tự động mang tên `EC2-High-CPU-Alarm`. Điều kiện kích hoạt được lập trình chính xác: nếu chỉ số `CPUUtilization > 80%` liên tục trong vòng 1 mốc dữ liệu (5 phút), hệ thống sẽ lập tức đổi trạng thái sang báo động để kỹ sư hạ tầng can thiệp kịp thời.
<img src="/images/week3/5.png" alt="Thiết lập bộ tự động báo động CloudWatch Alarm" style="max-width:100%; height:auto;" />

---

#### **2. Lab 8: Amazon Route 53 - Quy hoạch và Khởi tạo Hệ thống Private Hosted Zone nội bộ**

##### **Tổng quan (Overview)**
Một hệ thống mạng cô lập không thể giao tiếp an toàn nếu các thành phần máy chủ phải gọi nhau trực tiếp bằng địa chỉ IP thô dễ biến động. Bài Lab này tập trung vào việc thiết lập **Amazon Route 53 Private Hosted Zone**, xây dựng không gian đặt tên miền nội bộ an toàn bảo mật, tách biệt hoàn toàn khỏi internet công cộng.

##### **Khái niệm cốt lõi (Core Concepts)**
* **Private Hosted Zone (PHZ):** Vùng chứa bản ghi DNS nội bộ được ẩn hoàn toàn khỏi mạng internet bên ngoài. Các truy vấn phân giải tên miền chỉ có hiệu lực bên trong phạm vi các mạng ảo VPC được chỉ định liên kết xác thực.
* **DNS Resolution & DNS Hostnames:** Các thuộc tính cấu hình bắt buộc phải kích hoạt ở cấp độ VPC nhằm cho phép các máy chủ ảo gửi truy vấn đệ quy tới máy chủ DNS mặc định của AWS (`AWS-provided DNS server`).

##### **Quá trình triển khai chi tiết (Step-by-step Execution)**
Tôi tiến hành khởi tạo một Private Hosted Zone dưới tên miền doanh nghiệp nội bộ là `hutech.local`. Tại giao diện cấu hình, vùng mạng ảo `VPC ID` tùy chỉnh được chọn để ánh xạ trực tiếp với Hosted Zone này, đảm bảo mọi tài nguyên máy chủ nằm trong dải mạng nội bộ đều có khả năng phân giải tên miền an toàn.
<img src="/images/week3/6.png" alt="Khởi tạo cấu hình miền nội bộ Private Hosted Zone" style="max-width:100%; height:auto;" />

---

#### **3. Lab 10: Amazon Route 53 Resolver - Tích hợp Hạ tầng Kết nối Hybrid DNS**

##### **Tổng quan (Overview)**
Trong các kiến trúc đám mây hỗn hợp (Hybrid Cloud), mạng nội bộ của doanh nghiệp hoặc trường đại học cần phân giải các domain AWS nội bộ một cách liền mạch, và ngược lại các máy chủ đám mây cũng cần đọc được tài nguyên của trung tâm dữ liệu cục bộ. Bài Lab này hiện thực hóa cầu nối mạng gốc đó thông qua việc thiết lập **Amazon Route 53 Resolver Endpoints**.

##### **Khái niệm cốt lõi (Core Concepts)**
* **Inbound Endpoint:** Cặp giao diện mạng Elastic Network Interfaces (ENIs) dư thừa sở hữu IP nội bộ chuyên dụng trong VPC, đóng vai trò làm đầu mối lắng nghe và tiếp nhận các truy vấn DNS từ môi trường On-Premises chuyển tiếp vào nội bộ AWS.
* **Outbound Endpoint:** Thành phần chặn các truy vấn DNS xuất phát từ đám mây đám mây và chuyển tiếp chúng một cách an toàn ra các hệ thống DNS Server cục bộ bên ngoài dựa trên các quy tắc định tuyến có điều kiện (Conditional Forwarding Rules).

##### **Quá trình triển khai chi tiết (Step-by-step Execution)**

###### **Bước 1: Thiết lập cấu hình đầu mối tiếp nhận Inbound Endpoint**
Tôi khởi tạo cấu hình cho đầu mối tiếp nhận mang tên `Hutech-Inbound-Endpoint`. Để đảm bảo khả năng chịu lỗi cao và loại bỏ điểm sập đơn lẻ (SPOF), hệ thống bắt buộc phân bổ giao diện mạng trải rộng trên tối thiểu hai Availability Zones riêng biệt (`us-east-1a` và `us-east-1b`) gắn với dải IP tự động.
<img src="/images/week3/7.png" alt="Cấu hình phân bổ Multi-AZ cho Inbound Endpoint" style="max-width:100%; height:auto;" />

###### **Bước 2: Khởi tạo cấu phần Outbound Endpoint và rà soát trạng thái vận hành**
Để thiết lập luồng phân giải hai chiều, tôi triển khai cấu phần đầu ra `Hutech-Outbound-Endpoint` sử dụng cùng mô hình phân phối Multi-AZ có tính sẵn sàng cao. Hệ thống giám sát ghi nhận trạng thái vận hành đã chuyển sang màu xanh ổn định (`Operational`), xác nhận các ENI sẵn sàng định tuyến gói tin theo thời gian thực.
<img src="/images/week3/8.png" alt="Xác thực trạng thái Operational hoạt động của Outbound Endpoint" style="max-width:100%; height:auto;" />

---

#### **4. Lab 11: Quản trị Hạ tầng Doanh nghiệp thông qua Dòng lệnh AWS CLI**

##### **Tổng quan (Overview)**
**AWS Command Line Interface (AWS CLI)** chuyển đổi toàn bộ quy trình quản lý hệ thống từ các thao tác bấm chuột thủ công dễ gây sai sót trên giao diện đồ họa trực quan sang các cấu trúc dòng lệnh tự động, chính xác và có thể viết script. Điều này cho phép các kỹ sư tự động hóa hạ tầng và trích xuất trạng thái hệ thống một cách có hệ thống.

##### **Khái niệm cốt lõi (Core Concepts)**
* **AWS CloudShell:** Terminal quản trị tích hợp trực tiếp trên trình duyệt web, tự động xác thực thông tin tài khoản và tích hợp sẵn đầy đủ bộ công cụ phát triển AWS CLI giúp tối ưu hóa thời gian bảo trì.
* **JMESPath Query Filter (`--query`):** Ngôn ngữ truy vấn cấu trúc dữ liệu JSON phía client, giúp chọn lọc, cắt tỉa và loại bỏ các trường dữ liệu thừa, chỉ giữ lại các thông tin vận hành cốt lõi.

##### **Quá trình triển khai chi tiết (Step-by-step Execution)**

###### **Bước 1: Khởi chạy môi trường dòng lệnh xác thực an toàn**
Tôi kích hoạt môi trường terminal quản trị trực tuyến thông qua AWS CloudShell. Hệ thống tự động thiết lập phiên làm việc được ủy quyền bảo mật an toàn bám sát theo quyền hạn của IAM User đang đăng nhập.

###### **Bước 2: Xây dựng và thực thi các câu lệnh truy vấn lọc dữ liệu nâng cao**
Thay vì gọi một lệnh mô tả EC2 thông thường vốn trả về hàng chục trang dữ liệu JSON thô cồng kềnh, tôi xây dựng một bộ lọc bộ truy vấn JMESPath chính xác nhằm trích xuất đúng 3 thuộc tính vận hành thiết yếu: Instance ID, Trạng thái vòng đời và Loại phần cứng cấu hình, xuất ra định dạng bảng ASCII rõ ràng.
```bash
aws ec2 describe-instances --query "Reservations[*].Instances[*].[InstanceId,State.Name,InstanceType]" --output table
```
###### **Bước 3: Phân tích và xác thực đầu ra trạng thái hạ tầng dạng bảng**
API gateway đã xử lý yêu cầu đã xác thực và trả về một ma trận văn bản có cấu trúc, hoàn toàn loại bỏ dữ liệu JSON thô cồng kềnh. Kết quả đầu ra trên terminal hiển thị máy lab đang hoạt động với Instance ID (`i-058d40dc31f87c225`), trạng thái vòng đời vận hành đang hoạt động (`running`) và phân loại loại instance (`t2.micro`), xác nhận rằng hạ tầng đám mây đang hoạt động chính xác dưới sự kiểm soát trực tiếp bằng dòng lệnh.
<img src="/images/week3/9.png" alt="Xác thực kết quả thực thi lệnh CLI dạng bảng" style="max-width:100%; height:auto;" />

---

#### **5. Lab 13: Advanced VPC Topology - Kiến trúc mạng đa tầng bảo mật cô lập và Cấu hình Định tuyến Phân vùng**

##### **1. Tổng quan (Overview)**
Khi quy mô hệ thống doanh nghiệp tăng lên, một mô hình mạng phẳng hay đơn lớp (Flat Network) không còn đủ khả năng bảo vệ các thành phần nhạy cảm trước các nguy cơ tấn công mạng. Bài Lab này hiện thực hóa cấu trúc liên kết mạng nâng cao (Advanced VPC Topology), thực hiện phân bổ Subnet nhiều tầng (Multi-tier Subnet) nhằm chia tách hoàn toàn lớp giao diện công cộng, lớp nghiệp vụ ứng dụng nội bộ và lớp lưu trữ dữ liệu cốt lõi. Việc thiết lập hệ thống dải mạng con cô lập này đảm bảo việc quản lý luồng dữ liệu vào/ra một cách có chủ đích và gia cố bảo mật chuyên sâu.

##### **2. Khái niệm cốt lõi (Core Concepts)**
* **Kiến trúc mạng 3 tầng (3-Tier Architecture):** Mô hình chuẩn hóa kiến trúc mạng bằng cách phân chia logic thành 3 lớp biệt lập: Lớp công khai (Public/Web Tier) tiếp nhận traffic từ Internet; Lớp ứng dụng (Application Tier) xử lý logic nghiệp vụ; và Lớp cơ sở dữ liệu (Database Tier) hoàn toàn cô lập để lưu trữ tài nguyên nhạy cảm.
* **Isolation Control & Cấu trúc Bảng định tuyến (Route Tables):** Cơ chế kiểm soát luồng gói tin ở tầng mạng. Bằng cách sử dụng các bảng định tuyến riêng biệt cho từng lớp mạng con, chúng ta có thể ngăn chặn hoàn toàn việc các thực thể từ internet công cộng có khả năng quét (scanning), đánh hơi dữ liệu hoặc truy cập trực tiếp vào vùng Database nội bộ.
* **Quy hoạch dải CIDR (Classless Inter-Domain Routing):** Phân chia địa chỉ IP một cách khoa học để tránh xung đột mạng, tối ưu hóa không gian địa chỉ và tạo tiền đề cho việc thiết lập các luật tường lửa (Security Groups/NACLs) chính xác sau này.

##### **3. Quá trình triển khai chi tiết (Step-by-step Execution)**

###### **Bước 1: Khởi tạo và quy hoạch các dải mạng con hạ tầng chuyên dụng**
Để mở rộng cấu trúc liên kết mạng hiện tại của `MyLabVPC`, tôi tiến hành khởi tạo thêm các dải mạng con cô lập mới phục vụ riêng cho tầng lưu trữ dữ liệu nội bộ. Phân vùng này được đặt tên định danh là `Private-DB-Subnet-1A`, gán vào Availability Zone chỉ định và quy hoạch vùng địa chỉ CIDR hẹp mang tính cô lập cao là `10.0.3.0/24`. Tiến trình khai báo trên bảng điều khiển AWS được xác thực hoàn thành chính xác và hệ thống ghi nhận trạng thái sẵn sàng hoạt động.
<img src="/images/week3/10.png" alt="Khai báo thông số dải Subnet cô lập cho Database" style="max-width:100%; height:auto;" />

Hệ thống mạng con sau khi cấu hình được đồng bộ hóa và hiển thị trên sơ đồ kiến trúc trực quan của `MyLabVPC`, đảm bảo các thuộc tính quản lý về VPC ID, trạng thái liên kết logic và cấu phần định tuyến mạng ban đầu được thiết lập đúng chuẩn.
<img src="/images/week3/11.png" alt="Xác thực trạng thái Subnet mới hoạt động trên VPC Dashboard" style="max-width:100%; height:auto;" />

###### **Bước 2: Tạo Bảng định tuyến độc lập và thiết lập luật cô lập dữ liệu Biên**
Một mạng con cô lập chỉ thực sự an toàn khi nó được điều hướng bởi một thực thể định tuyến biệt lập. Tôi đã cấu hình một bảng định tuyến hoàn toàn mới mang tên `DB-Route-Table` trong mạng `MyLabVPC`. Bảng định tuyến này được thiết kế có chủ đích: tuyệt đối không thêm dòng luật mặc định hướng ngoại (`0.0.0.0/0 -> igw`), đồng nghĩa với việc chặn đứng mọi đường truyền trực tiếp từ bên ngoài biên vào vùng mạng con này.
<img src="/images/week3/12.png" alt="Khởi tạo thực thể định tuyến DB-Route-Table" style="max-width:100%; height:auto;" />

Sau khi khởi tạo thực thể định tuyến, tôi tiến hành thực hiện bước liên kết mạng con (Subnet Association), map trực tiếp dải mạng con `Private-DB-Subnet-1A` vào bảng định tuyến `DB-Route-Table` vừa tạo. Cấu hình này chính thức tách biệt lớp lưu trữ dữ liệu khỏi tầm ảnh hưởng của cổng Internet Gateway công cộng, thiết lập ranh giới bảo mật đa tầng kiên cố cho hệ thống đám mây.
<img src="/images/week3/13.png" alt="Gắn liên kết mạng con Database vào bảng định tuyến cô lập" style="max-width:100%; height:auto;" />

---

#### **6. Lab 14: Elastic Load Balancing - Triển khai Hạ tầng Điều phối Lưu lượng và Cân bằng tải Sẵn sàng cao**

##### **1. Overview**
Trong môi trường production thực tế, một ứng dụng (như hệ thống đặt tour du lịch hay cổng thông tin tuyển dụng) nếu chỉ chạy trên một máy chủ đơn lẻ sẽ đối mặt với nguy cơ sập hệ thống rất cao khi lượng người dùng tăng đột biến hoặc khi phần cứng gặp sự cố (Single Point of Failure). Bài Lab này giải quyết triệt để bài toán chịu tải và đảm bảo tính sẵn sàng cao (High Availability) bằng cách triển khai giải pháp cân bằng tải ứng dụng thông minh **Amazon ELB (Elastic Load Balancing)** hoạt động ở tầng ứng dụng (Layer 7). Bộ cân bằng tải đóng vai trò là điểm tiếp nhận duy nhất cho mọi traffic hướng ngoại và tự động điều phối luồng dữ liệu đến các máy chủ đích một cách tối ưu.

##### **2. Khái niệm cốt lõi (Core Concepts)**
* **Application Load Balancer (ALB):** Bộ cân bằng tải hoạt động tại tầng 7 của mô hình OSI. ALB có khả năng kiểm tra sâu vào gói tin HTTP/HTTPS, phân tích các thuộc tính như URL path, HTTP headers để điều phối traffic một cách thông minh đến các nhóm đích khác nhau bên dưới.
* **Target Group & Đăng ký Thực thể (Target Registration):** Nhóm tài nguyên logic chứa danh sách các máy chủ EC2 chịu trách nhiệm xử lý yêu cầu. ALB sẽ dựa vào danh sách này để phân phát các request của người dùng theo các thuật toán cân bằng tải (như Round Robin).
* **Health Checks (Kiểm tra sức khỏe chủ động):** Cơ chế ALB liên tục gửi các gói tin kiểm tra định kỳ (ping) tới các máy chủ trong Target Group theo một giao thức và đường dẫn cấu hình sẵn. Nếu một máy chủ không phản hồi (Unhealthy), ALB lập tức cô lập node đó, ngừng chuyển hướng traffic sang và tự động định tuyến lại dòng dữ liệu sang các máy chủ lành lặn còn lại, giúp hệ thống không bị downtime.

##### **3. Quá trình triển khai chi tiết (Step-by-step Execution)**

###### **Bước 1: Khởi tạo cấu hình thực thể Application Load Balancer**
Từ bảng quản trị Amazon EC2, tôi truy cập vào mục Load Balancing và tiến hành khởi tạo một Application Load Balancer. Thực thể được đặt tên định danh là `MyWebALB`, cấu hình lược đồ hướng Internet (Internet-facing) để làm cổng đón traffic công cộng, và thiết lập chế độ phân giải địa chỉ IPv4 thông dụng.
<img src="/images/week3/14.png" alt="Thiết lập thông số cơ bản cho Application Load Balancer" style="max-width:100%; height:auto;" />

Để đảm bảo kiến trúc dự phòng lỗi và sẵn sàng cao trên diện rộng, tôi thực hiện cấu hình Network Mapping cho ALB. Bộ điều hướng lưu lượng này được ánh xạ trực tiếp vào mạng `MyLabVPC` và được chỉ định hoạt động đồng thời trên cả hai phân vùng mạng công cộng Public Subnets thuộc các Availability Zones (Multi-AZ) khác nhau, đảm bảo hệ thống vẫn sống sót kể cả khi một trung tâm dữ liệu của AWS gặp thảm họa vật lý.
<img src="/images/week3/15.png" alt="Cấu hình sơ đồ mạng Multi-AZ dự phòng cho bộ cân bằng tải" style="max-width:100%; height:auto;" />

###### **Bước 2: Thiết lập Target Group và cấu hình cơ chế Health Check chủ động**
Tiếp theo, tôi xây dựng một Target Group mang tên `Web-TG` hoạt động trên giao thức HTTP, cổng 80 chuẩn web để làm đích đến cho luồng traffic sau khi đi qua ALB. Tại mục cấu hình kiểm tra sức khỏe nâng cao, tôi thiết lập đường dẫn kiểm tra mặc định là `/` kèm theo các ngưỡng thiết lập thời gian phản hồi (Timeout), chu kỳ gửi gói tin và số lần thử lại tối đa trước khi đưa ra kết luận về trạng thái của máy chủ.

Sau đó, tôi tiến hành đăng ký (Register) các máy chủ EC2 hiện có vào nhóm Target Group này, kích hoạt cơ chế theo dõi và sẵn sàng tiếp nhận điều phối luồng request từ bộ cân bằng tải ALB.
<img src="/images/week3/16.png" alt="Khởi tạo và cấu hình nhóm đích Target Group hoàn chỉnh" style="max-width:100%; height:auto;" />

---

### V. Thách thức hạ tầng, Nhật ký xử lý lỗi & Góc nhìn từ chuyên gia

Trong suốt quá trình thực thi chuỗi 6 bài Lab hạ tầng phức tạp tuần này, tôi đã liên tục đối mặt với các bài toán thực tế và rút ra được những bài học kinh nghiệm xương máu:

* **Bài toán "Chi phí ẩn" từ NAT Gateway tự động:** Khi thực hiện quy hoạch sơ đồ mạng lưới tại bài Lab 3 (VPC), trình cấu hình tự động thuật toán của AWS liên tục đưa ra khuyến nghị khởi tạo hệ thống bao gồm kèm theo 1 NAT Gateway để phục vụ mạng Private. Bằng việc phân tích sâu bảng chi phí hạ tầng, tôi nhận ra NAT Gateway được tính phí theo giờ chạy thực tế rất đắt đỏ ($0.045/hour) vượt ngoài phạm vi tài khoản học tập. Tôi đã chủ động chọn cấu hình mạng "None" cho mục này, đưa toàn bộ luồng kết nối đi trực tiếp qua Internet Gateway biên để giải quyết trọn vẹn mục tiêu bài học mà không làm phát sinh hóa đơn tiền tỷ cho tài khoản Sandbox.
* **Giải quyết vấn đề vận hành:** Quy trình vận hành trên đám mây hiếm khi diễn ra theo đường thẳng hoàn hảo. Khi các dịch vụ đám mây được quản lý như AWS CloudShell gặp hạn chế vùng hoặc khóa xác minh, kỹ sư hệ thống cần chuyển hướng nhanh chóng — bằng cách chuyển môi trường thực thi, cấu hình proxy terminal cục bộ hoặc tận dụng các shell thay thế để duy trì tiến độ triển khai.
* **Kỷ luật vòng đời và kiểm soát chi phí:** Môi trường đám mây tự động yêu cầu tuân thủ nghiêm ngặt việc quản lý vòng đời tài nguyên. Việc để các hạ tầng không sử dụng tiếp tục hoạt động — đặc biệt là các thành phần mạng chuyên sâu như Route 53 Resolver Endpoints hoặc Elastic IP chưa được liên kết — sẽ dẫn đến chi phí vận hành không cần thiết. Thiết lập quy trình có hệ thống gồm tạo, xác thực và xóa tài nguyên là một thói quen cơ bản của một chuyên gia cloud hiệu quả.

---

### VI. Suy ngẫm nghề nghiệp (Professional Reflections)

Việc tự tay cấu hình thành công và nhìn thấy một gói tin dữ liệu di chuyển một cách tuần tự: từ môi trường internet công cộng bên ngoài, xuyên qua cổng router biên Internet Gateway, được dẫn hướng chính xác bởi các dòng luật định tuyến trong Route Table để tiếp cận vào đúng bộ cân bằng tải Application Load Balancer, rồi từ đó điều phối nhịp nhàng sang các máy chủ EC2 ẩn sâu sau lớp mạng bảo mật đa tầng là trải nghiệm công nghệ giá trị nhất mà tôi tích lũy được cho đến thời điểm hiện tại.

Kỹ nghệ kiến trúc điện toán đám mây (Cloud Engineering) hoàn toàn không phải là những hành động bấm chuột may rủi, ngẫu nhiên dựa trên giao diện đồ họa trực quan. Đó là một bộ môn khoa học đòi hỏi sự tư duy logic mạch lạc, tính toán dải địa chỉ chính xác tuyệt đối và thiết kế hạ tầng có chủ đích dựa trên các bộ quy tắc, tiêu chuẩn kiến trúc tối ưu (*AWS Well-Architected Framework*). Việc làm chủ hạ tầng core này là bệ phóng vững chắc để tôi tiếp tục tiến sâu vào các bài toán đóng gói ứng dụng container hóa tự động ở các giai đoạn thực tập tiếp theo.

---

### VII. Kế hoạch chiến lược & Lộ trình tối ưu cho tuần tiếp theo

Để chuẩn bị hành trang cho các giai đoạn chuyên sâu tiếp theo của dự án và tối ưu hóa năng lực kiến trúc hệ thống, lộ trình hành động trong tuần tới sẽ tập trung triển khai các mũi nhọn sau:

* **Mở rộng chuỗi bài Lab nâng cao:** Tiếp tục thiết kế và thực thi thực tế các bài Lab chuyên sâu tiếp theo trên nền tảng AWS Sandbox nhằm làm chủ các cơ chế tự động mở rộng (Auto Scaling Groups - Lab 15), phân phối nội dung CDN (Amazon CloudFront - Lab 16).
* **Nghiên cứu Module ứng dụng thực tế:** Khai thác sâu các nguồn tài nguyên học tập chất lượng cao trên nền tảng YouTube nhằm phân tích cấu trúc, sơ đồ kiến trúc lớp và cách thức tích hợp các module chức năng phức tạp vào hệ thống đám mây.
* **Tích lũy kiến thức chuyên sâu:** Dành thời gian nghiên cứu các bài giảng kỹ thuật, các chuỗi video hướng dẫn từ các chuyên gia giải pháp (Solutions Architects) trên YouTube để cập nhật tư duy thiết kế tối ưu, xử lý các bài toán thắt nút cổ chai (Bottleneck) về hiệu năng và chuẩn bị sẵn sàng cho việc đóng gói Container hóa ứng dụng.