---
title: "Tuần 4: Định chuẩn An ninh Doanh nghiệp, Cấu trúc Mạng Phức hợp và Tự động hóa Chu trình Phân phối"
date: 2026-05-12
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

# Tuần 4: Làm chủ Tư thế An ninh Tập trung, Thiết kế Hạ tầng Định tuyến Liên VPC và Chuẩn hóa Đường ống Native CI/CD

### I. Tóm tắt tổng quan
Tuần 4 đánh dấu một giai đoạn tối ưu hóa hạ tầng diện rộng và gia cố an toàn hệ thống trong lộ trình thực tập chương trình First Cloud AI Journey – Workforce Bootcamp 2026 tại Văn phòng AWS Việt Nam. Tôi đã chuyển trọng tâm sang quản trị tư thế an ninh và liên kết mạng phức hợp quy mô lớn qua 5 bài Lab nền tảng: Lab 18 (Quản trị An ninh trung tâm Security Hub), Lab 19 (Đấu nối mạng ảo VPC Peering), Lab 20 (Trục định tuyến tập trung Transit Gateway), Lab 23 (Tự động hóa phân phối CodePipeline) và Lab 26 (Tường lửa ứng dụng web AWS WAF).

### II. Mục tiêu chiến lược trong tuần
* **Định chuẩn tư thế bảo mật (Cloud Security Posture):** Kích hoạt hệ thống AWS Security Hub để liên tục rà soát, kiểm toán và chấm điểm tuân thủ hạ tầng bám sát theo các tiêu chuẩn quốc tế nghiêm ngặt.
* **Quy hoạch mạng cô lập diện rộng (Multi-VPC Routing Architecture):** Thiết lập mô hình kết nối mạng một-đối-một qua VPC Peering và tập trung hóa luồng xử lý gói tin qua mô hình Hub-and-Spoke của AWS Transit Gateway.
* **Gia cố lá chắn biên ứng dụng (Application Edge Defense):** Triển khai AWS WAF nhằm thiết lập các tập luật (Rules) bảo vệ thông minh, ngăn chặn các nguy cơ tấn công khai thác lỗ hổng bảo mật phổ biến.
* **Chuẩn hóa chu trình phân phối mã nguồn (Native CodeSuite CI/CD):** Xây dựng đường ống tự động hóa kiểm thử, biên dịch và đẩy mã nguồn liên tục lên máy chủ thông qua AWS CodePipeline nguyên bản.

---

### III. Nhật ký hoạt động & Lộ trình phân bổ chi tiết (Từ 12/05/2026 đến 18/05/2026)

| Thời gian | Danh mục hoạt động | Chi tiết các tác vụ thực hiện chuyên sâu | Kết quả/Minh chứng đạt được |
| :--- | :--- | :--- | :--- |
| **Ngày 1** *(12/05)* | An ninh tập trung | Triển khai Lab 18: Kích hoạt AWS Security Hub, phân tích bảng điểm và trích xuất các lỗ hổng cấu hình sai sót. | Thiết lập thành công ranh giới kiểm toán an ninh tự động cho tài khoản. |
| **Ngày 2** *(13/05)* | Đấu nối liên mạng | Triển khai Lab 19: Thiết lập liên kết VPC Peering giữa các dải mạng con không trùng lặp, cập nhật Route Tables hai chiều. | Luồng dữ liệu nội bộ di chuyển an toàn xuyên VPC với độ trễ tối thiểu. |
| **Ngày 3-4** *(14-15/05)* | Kiến trúc Hub-Spoke | Triển khai Lab 20: Khởi tạo AWS Transit Gateway trung tâm, đính kèm hệ thống các VPC con và cô lập bảng định tuyến. | Loại bỏ cấu trúc liên kết lưới cồng kềnh, tối ưu hóa công tác quản trị mạng. |
| **Ngày 5** *(16/05)* | Lá chắn ứng dụng | Triển khai Lab 26: Cấu hình AWS WAF Web ACL, thiết lập các luật bảo vệ chống SQL Injection và gắn liên kết vào ALB. | Hệ thống Web Server được bảo vệ vững chắc trước các đợt quét tấn công. |
| **Ngày 6** *(17/05)* | Đường ống Native CI/CD | Triển khai Lab 23: Thiết lập chuỗi CodeCommit, CodeBuild, CodeDeploy kết nối khép kín dưới sự điều phối của CodePipeline. | Ứng dụng Node.js nâng cấp phiên bản tự động 100% khi có sự kiện Push code. |
| **Ngày 7** *(18/05)* | Kiểm toán & Đóng gói | Đóng gói toàn bộ mã nguồn Portfolio kỹ thuật trên nền tảng Hugo, rà soát hệ thống ảnh minh chứng chạy xanh sạch. | Nhật ký công việc Tuần 4 hoạt động ổn định trên hệ thống GitHub Pages. |

---

### IV. Thực thi kỹ thuật chuyên sâu & Phân tích chi tiết qua các bài Lab

#### **1. Lab 18: Getting Started with AWS Security Hub - Quản trị và Định chuẩn An ninh đám mây tập trung**

##### **Tổng quan (Overview)**
Khi quy mô tài nguyên và dịch vụ trên đám mây gia tăng, việc giám sát thủ công từng lỗ hổng bảo mật hay cấu hình sai sót (misconfiguration) trên các dịch vụ riêng lẻ trở nên bất khả thi. Bài Lab này tập trung vào việc thiết lập và vận hành AWS Security Hub. Đây là trung tâm quản trị an ninh tối cao, tự động hóa quy trình thu thập, hợp nhất và ưu tiên hóa các cảnh báo bảo mật từ nhiều dịch vụ cốt lõi (như Amazon GuardDuty, Amazon Inspector, Amazon Macie) cũng như các giải pháp từ đối tác AWS để đưa ra một góc nhìn phòng thủ toàn diện.

##### **Khái niệm cốt lõi (Core Concepts)**
* **AWS Security Hub:** Dịch vụ quản lý tư thế an ninh đám mây (Cloud Security Posture Management - CSPM), giúp tập hợp và chuẩn hóa các phát hiện bảo mật (Findings) thành một bảng điều khiển (Dashboard) tương tác trực quan.
* **Tiêu chuẩn kiểm toán bảo mật (Security Standards):** Hệ thống các bộ quy tắc tự động rà soát hạ tầng bám sát theo các tiêu chuẩn quốc tế nghiêm ngặt như AWS Foundations Security Best Practices và chuẩn CIS AWS Foundations Benchmark.

##### **Quá trình triển khai chi tiết (Step-by-step Execution)**

###### **Bước 1: Kích hoạt trung tâm bảo mật AWS Security Hub tập trung**
Tôi truy cập vào bảng điều khiển AWS Security Hub, nhấn nút kích hoạt dịch vụ để hệ thống bắt đầu thiết lập quyền hạn và khởi tạo các vai trò dịch vụ liên kết (Service-Linked Roles) cần thiết.
<img src="/images/week4/1.png" alt="Kích hoạt trung tâm bảo mật AWS Security Hub" style="max-width:100%; height:auto;" />

###### **Bước 2: Lựa chọn và định chuẩn các bộ tiêu chuẩn an ninh quốc tế**
Tại mục cấu hình tiêu chuẩn, tôi tiến hành bật các bộ quy chuẩn cốt lõi bao gồm AWS Foundational Security Best Practices và CIS AWS Foundations Benchmark. Hệ thống sẽ tự động lên lịch trình chạy ngầm các bài kiểm tra cấu hình tự động đối với toàn bộ tài nguyên.
<img src="/images/week4/2.png" alt="Lựa chọn các tiêu chuẩn bảo mật Security Standards" style="max-width:100%; height:auto;" />

###### **Bước 3: Phân tích bảng điều khiển Dashboard và rà soát điểm số an ninh**
Sau khi hệ thống hoàn tất chu kỳ quét hạ tầng, tôi truy cập vào trang Dashboard tổng quan. Màn hình hiển thị biểu đồ phân tích trực quan, phân loại các phát hiện bảo mật theo mức độ nghiêm trọng từ Thấp (Low) đến Tối nguy hiểm (Critical), đồng thời cung cấp điểm số tuân thủ cụ thể của tài khoản đám mây.
<img src="/images/week4/3.png" alt="Bảng điều khiển trực quan Dashboard hiển thị điểm số tuân thủ Security Hub" style="max-width:100%; height:auto;" />

---

#### **2. Lab 19: Setting Up VPC Peering - Đấu nối liên kết và Định tuyến liên vùng mạng ảo cách ly**

##### **Tổng quan (Overview)**
Theo mặc định, các vùng mạng ảo độc lập Amazon VPC trong môi trường đám mây AWS được cô lập hoàn toàn và không thể giao tiếp trực tiếp với nhau. Bài Lab này tập trung vào việc thiết lập và cấu hình dịch vụ VPC Peering. Đây là giải pháp kết nối mạng an toàn, tạo ra một đường ống định tuyến nội bộ giữa hai VPC riêng biệt, giúp các tài nguyên máy chủ có thể chia sẻ dữ liệu trực tiếp với độ trễ thấp tối thiểu mà không cần phải đi vòng ra ngoài môi trường internet công cộng đầy rủi ro.

##### **Khái niệm cốt lõi (Core Concepts)**
* **VPC Peering Connection:** Liên kết mạng logic một-đối-một nối giữa hai mạng VPC. Đường truyền này vận hành dựa trên hạ tầng xương sống của AWS (AWS Backbone Network), đảm bảo lưu lượng dữ liệu luôn được mã hóa và không bao giờ đi qua internet công cộng.
* **Không gian địa chỉ không trùng lặp (Non-overlapping CIDR):** Điều kiện tiên quyết để thiết lập liên kết Peering thành công là dải địa chỉ IP CIDR của hai mạng VPC tuyệt đối không được trùng lặp hoặc giao nhau (ví dụ: `172.31.0.0/16` và `10.10.0.0/16`), tránh gây xung đột khi định tuyến gói tin.

##### **Quá trình triển khai chi tiết (Step-by-step Execution)**

###### **Bước 1: Khởi tạo yêu cầu liên kết mạng ảo Peering Connection**
Tôi truy cập bảng điều khiển VPC, chọn mục Peering connections và nhấn nút tạo mới. Tôi thiết lập VPC cục bộ của tài khoản thực tập làm bên gửi yêu cầu (Requester) và trỏ chính xác mã định danh của VPC mục tiêu đóng vai trò bên nhận (Accepter), sau đó gửi lệnh khởi tạo.
<img src="/images/week4/4.png" alt="Khởi tạo yêu cầu kết nối Peering Connection" style="max-width:100%; height:auto;" />

###### **Bước 2: Chấp nhận yêu cầu đấu nối và xác thực trạng thái thông suốt**
Chuyển sang vai trò của VPC bên nhận, tôi tiến hành duyệt và bấm chọn Accept Request từ menu hành động Actions. Hệ thống đám mây lập tức thiết lập đường ống liên kết, chuyển đổi trạng thái kết nối sang màu xanh hoạt động ổn định (Active).
<img src="/images/week4/5.png" alt="Chấp nhận yêu cầu đấu nối đưa trạng thái về Active" style="max-width:100%; height:auto;" />

###### **Bước 3: Cấu hình cập nhật Route Tables điều phối gói tin nội bộ**
Để hoàn tất bài Lab, tôi lần lượt truy cập vào các Bảng định tuyến (Route Tables) thuộc phân vùng Public Subnet của cả hai mạng VPC. Tại tab Routes, tôi thêm dòng luật định tuyến: nhập dải địa chỉ CIDR của mạng đối phương làm đích đến và chọn Target đầu ra chính là mã liên kết Peering vừa thiết lập để chính thức thông luồng dữ liệu.
<img src="/images/week4/6.png" alt="Cập nhật Route Table bổ sung luật định tuyến Peering" style="max-width:100%; height:auto;" />

---

#### **3. Lab 20: Set Up AWS Transit Gateway - Xây dựng trục mạng trung tâm và Quy hoạch định tuyến Hub-and-Spoke**

##### **Tổng quan (Overview)**
Khi số lượng mạng ảo Amazon VPC trong doanh nghiệp tăng lên, việc kết nối chúng lại với nhau bằng mô hình mạng lưới (Mesh Topology) sử dụng VPC Peering truyền thống sẽ trở nên cực kỳ cồng kềnh, phức tạp và khó kiểm soát. Bài Lab này tập trung giải quyết triệt để bài toán quy mô lớn đó bằng cách thiết lập AWS Transit Gateway (TGW). Đây là một bộ định tuyến đám mây thông minh đóng vai trò là "Hub" trung tâm, kết nối tập trung hệ thống gồm nhiều VPCs biệt lập ("Spokes") lại với nhau, giúp đơn giản hóa sơ đồ mạng và tối ưu hóa quản trị định tuyến từ một điểm duy nhất.

##### **Khái niệm cốt lõi (Core Concepts)**
* **AWS Transit Gateway (TGW):** Một trung tâm đám mây mạng quản lý tập trung, hoạt động như một bộ định tuyến ảo lớp 3 nâng cao để điều phối và kiểm soát toàn bộ luồng traffic di chuyển giữa các mạng VPC, VPN nội bộ và kết nối AWS Direct Connect.
* **Transit Gateway Attachments:** Tiến trình đấu nối logic các tài nguyên mạng vào Transit Gateway. Bài lab thực hiện đính kèm các VPCs độc lập vào TGW, cho phép cổng này bắt đầu tiếp nhận gói tin từ các phân vùng subnet.

##### **Quá trình triển khai chi tiết (Step-by-step Execution)**

###### **Bước 1: Khởi tạo thực thể mạng trung tâm AWS Transit Gateway**
Tôi truy cập vào phân hệ VPC Dashboard, tìm mục Transit gateways và tiến hành nhấn nút khởi tạo một Transit Gateway trung tâm đặt tên là `Hub-TGW`. Tôi cấu hình dải ASN riêng biệt và kích hoạt tính năng tự động chấp nhận các yêu cầu đấu nối tài nguyên.
<img src="/images/week4/7.png" alt="Khởi tạo thực thể bộ định tuyến trung tâm AWS Transit Gateway" style="max-width:100%; height:auto;" />

###### **Bước 2: Đấu nối các VPCs (Spokes) vào cụm bộ định tuyến trung tâm**
Tôi di chuyển đến mục Transit gateway attachments để tiến hành cấu hình luồng kết nối cho các chi nhánh mạng con. Tôi lần lượt tạo các lượt đính kèm độc lập, chọn loại tài nguyên liên kết là VPC, trỏ chính xác định danh ID của các mạng VPC mục tiêu và chỉ định các Public Subnets chịu trách nhiệm giao tiếp biên.
<img src="/images/week4/8.png" alt="Cấu hình Transit Gateway Attachments liên kết hệ thống các VPCs" style="max-width:100%; height:auto;" />

###### **Bước 3: Cấu hình bảng định tuyến VPC Route Tables hướng tâm**
Để luồng dữ liệu từ các máy chủ ảo nằm trong các VPC có thể tìm đường đi đến bộ định tuyến trung tâm, tôi truy cập vào Bảng định tuyến (Route Tables) nội bộ của từng VPC con. Tại tab Routes, tôi thêm dòng luật: định nghĩa dải IP đích của các VPC đối phương và chọn Target đầu ra trỏ thẳng về thực thể Transit Gateway vừa dựng để chính thức thông suốt toàn bộ trục mạng.
<img src="/images/week4/9.png" alt="Cập nhật Route Table nội bộ của VPC hướng tâm về Transit Gateway" style="max-width:100%; height:auto;" />

---

#### **5. Lab 23: Deploy Applications to EC2 with AWS CodePipeline - Chuẩn hóa chu trình CI/CD tự động bằng bộ công cụ AWS Native**

##### **Tổng quan (Overview)**
Bên cạnh việc sử dụng các bên thứ ba, hệ sinh thái AWS cung cấp một bộ giải pháp tích hợp toàn diện giúp xây dựng các đường ống phân phối phần mềm an toàn, khép kín và có khả năng kiểm soát truy cập đồng nhất qua IAM. Bài Lab này tập trung vào việc hiện thực hóa quy trình triển khai tự động một ứng dụng Node.js lên máy chủ ảo EC2 bằng cách kết nối chuỗi dịch vụ native bao gồm AWS CodeCommit, AWS CodeBuild, AWS CodeDeploy dưới sự điều phối tối cao của AWS CodePipeline.

##### **Khái niệm cốt lõi (Core Concepts)**
* **AWS CodePipeline:** Trình điều phối chu trình phát triển (Orchestration Service), tự động hóa các giai đoạn kiểm thử, biên dịch và phát hành ứng dụng bám sát theo các mô hình kiểm soát chất lượng (Stage Gates).
* **CodeDeploy Agent & AppSpec File:** Trình tác vụ chạy ngầm bên trong máy chủ EC2 kết hợp với tệp tin cấu hình kịch bản `appspec.yml` để định nghĩa chu kỳ triển khai, quản lý các tệp cấu trúc và kích hoạt kịch bản shell tự động lúc nâng cấp mã nguồn.

##### **Quá trình triển khai chi tiết (Step-by-step Execution)**

###### **Bước 1: Khởi tạo kho lưu trữ mã nguồn nội bộ AWS CodeCommit**
Tôi truy cập bảng điều khiển CodeCommit, tiến hành tạo một repository bảo mật đặt tên là `NodeJS-App-Repo`. Tiếp theo, cấu hình phân quyền truy cập và thực hiện đẩy (Push) toàn bộ mã nguồn ứng dụng Node.js cùng tệp cấu hình `buildspec.yml` và `appspec.yml` từ máy tính cục bộ lên đám mây.
<img src="/images/week4/10.png" alt="Khởi tạo và đẩy mã nguồn lên kho lưu trữ AWS CodeCommit" style="max-width:100%; height:auto;" />

###### **Bước 2: Cấu hình kịch bản phân phối deployment ứng dụng qua AWS CodeDeploy**
Tôi di chuyển đến mục AWS CodeDeploy, khởi tạo một ứng dụng (Application) và nhóm đích triển khai (Deployment Group) ứng dụng. Tôi cấu hình hệ thống trỏ thẳng vào thẻ Tag của máy chủ EC2 đích, chỉ định cơ chế cài đặt deployment cuốn chiếu và gán vai trò IAM Role phù hợp để CodeDeploy Agent trên EC2 có quyền giao tiếp an toàn.
<img src="/images/week4/11.png" alt="Thiết lập nhóm triển khai Deployment Group trên AWS CodeDeploy" style="max-width:100%; height:auto;" />

###### **Bước 3: Đấu nối trục liên kết đường ống tổng thể AWS CodePipeline và kiểm toán kết quả**
Cuối cùng, tôi khởi tạo một đường ống tổng thể AWS CodePipeline kết nối tuần tự: lấy mã nguồn từ *CodeCommit Source Stage*, chuyển tiếp sang máy chủ biên dịch *CodeBuild Stage*, và kết thúc tại lớp phát hành *CodeDeploy Stage*. Hệ thống tự động kích hoạt chu trình phân phối, báo trạng thái đồng loạt chuyển sang màu xanh thành công (**`Succeeded`**), giúp ứng dụng Node.js vận hành mượt mà trên môi trường EC2 thực tế.
<img src="/images/week4/12.png" alt="Xác thực trạng thái Succeeded hoàn tất đường ống phân phối tự động AWS CodePipeline" style="max-width:100%; height:auto;" />

---

### V. Thách thức hạ tầng, Nhật ký xử lý lỗi & Góc nhìn từ chuyên gia

Trong suốt quá trình thực thi chuỗi 5 bài Lab hạ tầng phức tạp tuần này, tôi đã liên tục đối mặt với các bài toán thực tế và rút ra được những bài học kinh nghiệm xương máu:

* **Bài toán bảo mật IAM và Giới hạn quyền trên tài khoản Sandbox:** Thách thức lớn nhất trong tuần xuất hiện ở giai đoạn đầu khi hệ thống báo lỗi nghiêm trọng trong việc khởi tạo ECS Cluster do thiếu đặc quyền Service-Linked Role (`AWSServiceRoleForECS`). Việc Web Console bị thắt chặt quyền tạo role tự động đòi hỏi kỹ sư phải có tư duy linh hoạt: lách qua giao diện đồ họa bằng cách cấu hình Access Key bảo mật trên Command Prompt cá nhân và dùng công cụ AWS CLI để ra lệnh ép hệ thống kích hoạt vai trò chạy ngầm thành công.
* **Kỷ luật vòng đời và FinOps kiểm soát tài nguyên:** Vận hành các giải pháp mạng enterprise đa vùng (VPC Peering, Transit Gateway) luôn đi kèm với chi phí duy trì cổng kết nối ngầm rất đắt đỏ. Tuân thủ nghiêm ngặt quy trình "làm đến đâu, kiểm toán ảnh đến đó và tiến hành xóa sạch tài nguyên ngay lập tức" theo thứ tự ngược từ ngọn về gốc là thói quen cốt lõi của một chuyên gia điện toán đám mây chuyên nghiệp để bảo vệ ngân sách tài khoản.

---

### VI. Suy ngẫm nghề nghiệp (Professional Reflections)

Kiến trúc điện toán đám mây cấp doanh nghiệp (Enterprise Cloud Engineering) hoàn toàn không phải là những hành động bấm chuột may rủi dựa trên giao diện đồ họa trực quan. Đó là một bộ môn khoa học đòi hỏi tính toán dải không gian địa chỉ chính xác tuyệt đối (CIDR Allocation), thiết kế luồng đi của gói tin có chủ đích bám sát theo các quy tắc Route Tables nâng cao, và gia cố lá chắn bảo mật vững chắc nhiều lớp từ ranh giới kiểm toán an ninh (Security Hub) cho đến tường lửa lớp ứng dụng biên (AWS WAF). Việc làm chủ chuỗi hạ tầng này là bệ phóng vững chắc để tôi tiếp tục thiết kế các hệ thống phân phối nội dung quy mô lớn ở chặng đường tiếp theo.

---

### VII. Kế hoạch chiến lược & Lộ trình tối ưu cho tuần tiếp theo

Để chuẩn bị hành trang cho các giai đoạn chuyên sâu tiếp theo của dự án và tối ưu hóa năng lực kiến trúc hệ thống, lộ trình hành động trong tuần tới sẽ tập trung triển khai các mũi nhọn sau:

* **Họp nhóm & Định hướng Kiến trúc Dự án Tốt nghiệp:** Tổ chức buổi họp với các thành viên trong nhóm để thảo luận và thống nhất về kiến trúc hệ thống cho đồ án tốt nghiệp (Hệ thống Website Đặt tour du lịch Việt Nam tích hợp Chatbot AI tư vấn thông minh). Nhóm sẽ tiến hành hoạch định ranh giới các microservices, phân chia cấu trúc mã nguồn các kho lưu trữ và lên kế hoạch triển khai tài nguyên hạ tầng trên nền tảng AWS.
* **Tham gia Sự kiện Bootcamp & Kết nối Kỹ thuật:** Tham dự các buổi workshop kỹ thuật và sự kiện chuyên sâu tiếp theo thuộc chương trình Workforce Bootcamp được tổ chức trực tiếp tại văn phòng AWS Việt Nam để tham vấn ý kiến từ các Solutions Architects về các bài toán thắt nút cổ chai (bottleneck) và mô hình đóng gói production tối ưu.
* **Tích lũy kiến thức chuyên sâu:** Dành thời gian nghiên cứu các bài giảng kỹ thuật, các chuỗi video hướng dẫn từ các chuyên gia giải pháp (Solutions Architects) trên YouTube để cập nhật tư duy thiết kế tối ưu, xử lý các bài toán thắt nút cổ chai (Bottleneck) về hiệu năng và chuẩn bị sẵn sàng cho việc đóng gói Container hóa ứng dụng.