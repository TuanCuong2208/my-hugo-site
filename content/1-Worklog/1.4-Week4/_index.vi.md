---
title: "Tuần 4: Tích hợp Hybrid DNS và Quản lý AWS CLI"
date: 2026-05-25
weight: 4
chapter: false
pre: "<b>1.4. </b>"
---

Trong tuần này, tôi tập trung vào các tác vụ quản lý hạ tầng và mạng nâng cao trên AWS. Mục tiêu chính là triển khai cơ chế phân giải Hybrid DNS bằng cách sử dụng Amazon Route 53 Resolver để kết nối mạng đám mây với mạng doanh nghiệp cục bộ, đồng thời tối ưu hóa quy trình vận hành thông qua Giao diện Dòng lệnh AWS (AWS CLI).

---

## 1. Lab 7: Amazon VPC - Kiến trúc Subnet Nội bộ

Yêu cầu cốt lõi của bất kỳ triển khai cấp doanh nghiệp nào là thiết lập một mạng ảo được cô lập. Trong lab này, tôi đã xây dựng cấu trúc nền tảng **Amazon VPC (Virtual Private Cloud)** để lưu trữ tài nguyên hệ thống một cách an toàn và đảm bảo sự phân tách ranh giới được kiểm soát.

### Khái niệm cốt lõi:
* **CIDR Block:** Một phương pháp cấp phát địa chỉ IP và định tuyến các gói Internet Protocol mà không gây lãng phí (ví dụ: `10.0.0.0/16`).
* **Subnet Isolation:** Tách biệt tài nguyên frontend khỏi backend cơ sở dữ liệu nhạy cảm nhằm kiểm soát ranh giới logic ở cấp độ mạng.

### Quá trình triển khai:

#### Bước 1: Khởi tạo Virtual Private Cloud (VPC)
Tôi đã triển khai một VPC tùy chỉnh có tên `MyLabVPC` với dải IP rộng `10.0.0.0/16`, tạo ra một môi trường sandbox hoàn toàn cô lập dành riêng cho các ứng dụng doanh nghiệp.

![Step 1](/images/week4/anh1.png)

#### Bước 2: Cấp phát Public Subnets cho các thành phần Edge
Tôi đã tạo phân đoạn subnet đầu tiên thành một Public Subnet bên trong Availability Zone `us-east-1a`. Lớp giao diện mạng này xử lý kết nối tới các endpoint bên ngoài và các giao diện công khai.

![Step 2](/images/week4/anh2.png)

#### Bước 3: Thiết lập các vùng dự phòng Multi-AZ
Để ngăn ngừa các lỗ hổng single-point-of-failure, tôi mở rộng hạ tầng bằng cách thiết lập thêm các subnet bổ sung. Việc tách biệt nghiêm ngặt này đáp ứng các tiêu chí về tính sẵn sàng cao cho những triển khai tiếp theo.

![Step 3](/images/week4/anh3.png)

---

## 2. Lab 8: VPC Routing và Ingress Gateways

Một VPC được cô lập không thể giao tiếp với các dịch vụ bên ngoài nếu không có các thành phần định tuyến rõ ràng. Lab này tập trung vào việc xây dựng các kết nối cấu trúc cần thiết để định tuyến lưu lượng một cách an toàn giữa workload trên đám mây và các endpoint bên ngoài.

### Khái niệm cốt lõi:
* **Internet Gateway (IGW):** Một thành phần VPC có khả năng mở rộng theo chiều ngang, có tính dư thừa và độ sẵn sàng cao, cho phép giao tiếp giữa các instance trong VPC và internet.
* **Route Tables:** Một tập hợp các quy tắc, được gọi là routes, dùng để xác định nơi lưu lượng mạng từ subnet hoặc gateway được chuyển hướng.

### Quá trình triển khai:

#### Bước 1: Gắn Internet Gateway (IGW)
Tôi khởi tạo một gateway ảo và liên kết trực tiếp nó với `MyLabVPC`, cung cấp một cầu nối logic cho các luồng giao tiếp vào và ra.

![Step 4](/images/week4/anh4.png)

#### Bước 2: Cập nhật ánh xạ Route Ingress và Egress
Tôi chỉnh sửa Route Table công khai đang hoạt động bằng cách thêm route mặc định (`0.0.0.0/0`) hướng tới Internet Gateway vừa triển khai, cho phép các node xử lý các yêu cầu hướng internet.

![Step 5](/images/week4/anh5.png)

---

## 3. Lab 10: Amazon Route 53 - Tích hợp Hybrid DNS Resolver

**Amazon Route 53 Resolver** cung cấp một cầu nối gốc cho môi trường Hybrid Cloud. Trong triển khai doanh nghiệp, các mạng doanh nghiệp (On-Premises, chẳng hạn như mạng nội bộ của trường đại học) cần phân giải các domain AWS nội bộ một cách liền mạch, trong khi workload AWS đồng thời cần phân giải tài nguyên của trung tâm dữ liệu cục bộ mà không làm lộ cấu trúc nội bộ ra internet công cộng.

### Khái niệm cốt lõi:
* **Private Hosted Zone (PHZ):** Một vùng chứa cục bộ lưu trữ các bản ghi DNS cho một domain cần được ẩn khỏi internet công cộng và chỉ có thể được phân giải trong các VPC được liên kết xác thực cụ thể.
* **Inbound Endpoint:** Một cặp Elastic Network Interfaces (ENIs) dư thừa với các địa chỉ IP nội bộ chuyên dụng bên trong VPC. Chúng hoạt động như các bộ lắng nghe mục tiêu cho các DNS forwarder bên ngoài hoặc on-premises để chuyển tiếp truy vấn vào AWS.
* **Outbound Endpoint:** Các giao diện mạng được sử dụng để chặn các truy vấn DNS xuất phát từ đám mây và chuyển tiếp chúng một cách an toàn ra các DNS server on-premises bên ngoài dựa trên các quy tắc định tuyến có điều kiện.
* **Authoritative Split-Horizon Records:** Việc tạo tự động các bản ghi Start of Authority (SOA) và Name Server (NS) nhằm tách biệt cấu trúc đặt tên nội bộ của đám mây khỏi vòng lặp đệ quy của internet công cộng.
#### Bước 1: Tạo Private Hosted Zone
Tôi khởi tạo một Private Hosted Zone dưới tên miền nội bộ `hutech.local`. Zone này được liên kết rõ ràng với VPC đang hoạt động. Sau khi tạo, Route 53 lập tức cung cấp metadata SOA bắt buộc cùng với một tập hợp Name Server cục bộ để xử lý phản hồi có thẩm quyền nội bộ.

![Step 6](/images/week4/anh6.png)

#### Bước 2: Cấu hình Route 53 Resolver Inbound Endpoint
Để chấp nhận các yêu cầu đệ quy đến từ các hệ thống bên ngoài, tôi khởi tạo cấu hình cho Inbound Endpoint có tên `Hutech-Inbound-Endpoint`. Trong quá trình cấp phát, AWS áp đặt một ràng buộc kiến trúc bắt buộc: endpoint phải trải rộng trên tối thiểu hai Availability Zone riêng biệt (`us-east-1a` và `us-east-1b`) nhằm đảm bảo khả năng chịu lỗi và giảm thiểu rủi ro single-point-of-failure.

Do các giới hạn nghiêm ngặt về khả năng cấp phát IP bên trong VPC tùy chỉnh ban đầu của lab, cấu hình đã được chuyển động sang Default VPC được cấu hình sẵn. Sự điều chỉnh mang tính chiến lược này cung cấp sơ đồ subnet rõ ràng trên nhiều vùng, mở khóa trạng thái giao diện bị vô hiệu hóa và cho phép gán các địa chỉ IPv4 nội bộ được chọn tự động.

![Step 7](/images/week4/anh7.png)

#### Bước 3: Khởi tạo Outbound Endpoints và theo dõi trạng thái vận hành
Để thiết lập khả năng phân giải hai chiều hoàn chỉnh, tôi cấu hình Outbound Endpoint bổ sung có tên `Hutech-Outbound-Endpoint` sử dụng cùng mô hình phân phối Multi-AZ có tính sẵn sàng cao. Cả hai endpoint đều được theo dõi cho đến khi trạng thái chuyển sang `Operational`, nghĩa là các giao diện mạng đã được liên kết thành công và sẵn sàng xử lý việc chuyển tiếp gói tin theo thời gian thực.

![Step 8](/images/week4/anh8.png)

#### Bước 4: Thực hiện giải phóng tài nguyên và dọn dẹp môi trường đám mây
Tuân thủ nghiêm ngặt trụ cột Tối ưu Chi phí của AWS Well-Architected Framework, một chuỗi quy trình ngừng hoạt động chính xác đã được thực hiện sau khi thử nghiệm vận hành hoàn tất. Vì các Resolver Endpoints đang hoạt động sẽ phát sinh chi phí theo giờ cho các ENI nền tảng, hệ thống phân cấp tài nguyên đã được dọn dẹp theo thứ tự ngược lại: Outbound và Inbound Endpoints được hủy liên kết và xóa có hệ thống để giải phóng IP đã đặt trước, sau đó xóa an toàn `hutech.local` Private Hosted Zone.

---

## 4. Lab 11: Quản trị Hạ tầng Doanh nghiệp thông qua AWS CLI

**AWS Command Line Interface (AWS CLI)** chuyển đổi việc quản lý hệ thống từ các thao tác thủ công dễ gây lỗi trên giao diện đồ họa sang các lệnh tự động có thể viết script. Cấu trúc dòng lệnh này cho phép các kỹ sư quản lý đồng thời hàng nghìn tài nguyên, xây dựng các hook hỗ trợ Infrastructure-as-Code và trích xuất trạng thái có tính xác định.

### Khái niệm cốt lõi:
* **AWS CloudShell:** Một terminal quản trị có thể truy cập từ trình duyệt, đã được xác thực sẵn và tích hợp đầy đủ bộ công cụ AWS CLI, loại bỏ việc xử lý thông tin xác thực cục bộ trong quá trình bảo trì môi trường đám mây.
* **JMESPath Query Engine (`--query`):** Một ngôn ngữ truy vấn JSON phía client tích hợp sẵn trong AWS CLI, dùng để phân tích, lựa chọn và rút gọn các phản hồi API lớn thành các mảng key-value cụ thể.
* **Output Matrix Restructuring (`--output table`):** Một chỉ thị định dạng giúp chuyển đổi dữ liệu JSON thô thành các bảng ASCII rõ ràng, dễ đọc để đánh giá vận hành tức thời.

### Quá trình triển khai:

#### Bước 1: Xác định giới hạn hệ thống và các hướng thực thi thay thế
Khi khởi chạy AWS CloudShell tích hợp trên web tại vùng chính, môi trường gặp phải khóa trạng thái tenant hạn chế: `Unable to create the environment. Your account verification is in progress...`. Đây là một cơ chế giới hạn tài nguyên dịch vụ phổ biến được áp dụng cho các tài khoản học thuật hoặc tài khoản sandbox trong thời gian sử dụng cao.

Để vượt qua trở ngại này mà không làm gián đoạn quá trình vận hành, hướng thực thi đã được chuyển sang một môi trường terminal xác thực thay thế, thể hiện khả năng giải quyết vấn đề linh hoạt và tính bền bỉ trong quản trị.
#### Bước 2: Xây dựng và thực thi các truy vấn API nâng cao có bộ lọc

Sử dụng terminal, tôi đã xây dựng một truy vấn cấu trúc nâng cao hướng tới endpoint Amazon EC2. Thay vì gọi một lệnh mô tả chung vốn kéo về các bản ghi dữ liệu dài nhiều trang, tôi xây dựng một bộ lọc JMESPath chính xác nhằm trích xuất chỉ ba thuộc tính vận hành thiết yếu: mã định danh máy duy nhất, trạng thái vòng đời theo thời gian thực và loại phần cứng.

Chuỗi lệnh được tối ưu hóa được thực thi như sau:

```bash
aws ec2 describe-instances --query "Reservations[*].Instances[*].[InstanceId,State.Name,InstanceType]" --output table
```

#### Bước 3: Phân tích và xác thực đầu ra trạng thái hạ tầng dạng bảng

API gateway đã xử lý yêu cầu đã xác thực và trả về một ma trận văn bản có cấu trúc, hoàn toàn loại bỏ dữ liệu JSON thô cồng kềnh. Kết quả đầu ra trên terminal hiển thị máy lab đang hoạt động với Instance ID (`i-058d40dc31f87c225`), trạng thái vòng đời vận hành đang hoạt động (`running`) và phân loại loại instance (`t2.micro`), xác nhận rằng hạ tầng đám mây đang hoạt động chính xác dưới sự kiểm soát trực tiếp bằng dòng lệnh.

🧠 Các góc nhìn quan trọng & Bài học kỹ thuật rút ra

Thực tế của kiến trúc Hybrid: Thiết kế mạng Hybrid đòi hỏi sự hiểu biết sâu sắc về định tuyến split-horizon. Inbound Endpoint và Outbound Endpoint không đơn thuần chỉ là các tùy chọn cấu hình; chúng đại diện cho các cầu nối mạng chuyên biệt đòi hỏi bố cục subnet có chủ đích và triển khai Multi-AZ để tránh các sự cố DNS trên toàn doanh nghiệp.

Giải quyết vấn đề vận hành: Quy trình vận hành trên đám mây hiếm khi diễn ra theo đường thẳng hoàn hảo. Khi các dịch vụ đám mây được quản lý như AWS CloudShell gặp hạn chế vùng hoặc khóa xác minh, kỹ sư hệ thống cần chuyển hướng nhanh chóng — bằng cách chuyển môi trường thực thi, cấu hình proxy terminal cục bộ hoặc tận dụng các shell thay thế để duy trì tiến độ triển khai.

Kỷ luật vòng đời và kiểm soát chi phí: Môi trường đám mây tự động yêu cầu tuân thủ nghiêm ngặt việc quản lý vòng đời tài nguyên. Việc để các hạ tầng không sử dụng tiếp tục hoạt động — đặc biệt là các thành phần mạng chuyên sâu như Route 53 Resolver Endpoints hoặc Elastic IP chưa được liên kết — sẽ dẫn đến chi phí vận hành không cần thiết. Thiết lập quy trình có hệ thống gồm tạo, xác thực và xóa tài nguyên là một thói quen cơ bản của một chuyên gia cloud hiệu quả.

🚀 Hướng tới tương lai: Mục tiêu & Cột mốc Tuần 5

Để duy trì động lực trong chương trình First Cloud AI Journey – Workforce Bootcamp 2026, mục tiêu của tôi trong Tuần 5 sẽ chuyển hướng sang bảo mật hạ tầng, ranh giới mạng nhiều tầng, cân bằng tải hiệu năng cao và phân phối nội dung toàn cầu.

📋 Các mô-đun Lab dự kiến:

Lab 13: Advanced VPC Topology - Xây dựng kiến trúc VPC nâng cao với phân phối Subnet nhiều tầng nhằm tách biệt lớp cơ sở dữ liệu khỏi các web instance.

Lab 14: Elastic Load Balancing - Thiết lập Elastic Load Balancing (ELB) để quản lý lưu lượng ứng dụng đến một cách tự động.

Lab 15: Auto Scaling Groups - Triển khai Auto Scaling Groups (ASG) nhằm đảm bảo khả năng mở rộng động và khả năng chịu lỗi của hệ thống dựa trên tải lưu lượng theo thời gian thực.

Lab 16: Amazon CloudFront - Cấu hình Amazon CloudFront nhằm phân phối nội dung toàn cầu với độ trễ thấp thông qua các edge cache theo khu vực.

📅 Tham gia sự kiện:

Ngoài việc hoàn thành các mô-đun kỹ thuật nâng cao trong phòng lab, tôi dự định tham gia Sự kiện Bootcamp Chính thức lần thứ 2 được tổ chức tại Văn phòng AWS Việt Nam (Bitexco Financial Tower). Buổi làm việc này sẽ mang lại các cơ hội quan trọng để đồng bộ với các kiến trúc sư giải pháp cloud, đánh giá các framework triển khai doanh nghiệp cấp sản xuất và tăng cường kết nối cộng đồng với các chuyên gia trong ngành.