---
title: "Tuần 4: Hệ sinh thái Container, Tự động hóa CI/CD Enterprise và Hạ tầng Mạng Hybrid nâng cao"
date: 2026-05-12
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

# Tuần 4: Làm chủ Bộ đôi Container Điều phối, Tự động hóa Chu trình Phát triển DevSecOps và Hạ tầng Mạng Phức hợp

### I. Tóm tắt tổng quan
Tuần 4 đánh dấu giai đoạn bứt phá và tích hợp toàn diện nhất trong lộ trình thực tập tại AWS Việt Nam. Tôi đã dịch chuyển hoàn toàn khỏi tư duy quản trị máy chủ truyền thống để tiến thẳng vào kỷ nguyên Hiện đại hóa ứng dụng (Application Modernization). Nội dung nghiên cứu thực nghiệm bao phủ trọn vẹn 7 bài Lab enterprise quy mô lớn: từ điều phối Microservices Serverless (Lab 16), tự động hóa chuỗi cung ứng phần mềm CI/CD đa nền tảng (Lab 17, Lab 23), gia cố an ninh trung tâm qua Security Hub (Lab 18), cho đến việc thiết kế các mô hình mạng hỗn hợp kết nối đa VPC diện rộng (Lab 19, Lab 20) và tối ưu hóa chi phí bằng kiến trúc hướng sự kiện Event-Driven (Lab 22).

### II. Mục tiêu chiến lược trong tuần
* **Hiện đại hóa ứng dụng bằng Container (Microservices Orchestration):** Làm chủ kỹ nghệ đóng gói, phân tầng và điều phối cụm dịch vụ Frontend/Backend tách biệt thông qua Amazon ECS Fargate Serverless.
* **Chuẩn hóa chu trình DevSecOps toàn diện (Automated CI/CD Pipelines):** Xây dựng các đường ống tự động hóa kiểm thử, biên dịch và triển khai mã nguồn liên tục từ GitLab/GitHub thẳng lên Cluster Container và EC2 thông qua bộ công cụ AWS Code Suite.
* **Gia cố an ninh và Định chuẩn bảo mật (Enterprise Security Governance):** Kích hoạt AWS Security Hub để liên tục rà soát, chấm điểm cấu hình hạ tầng bám sát theo các tiêu chuẩn bảo mật quốc tế nghiêm ngặt.
* **Thiết kế kiến trúc mạng đa vùng phức hợp (Hybrid Cross-VPC Mesh):** Làm chủ kỹ thuật kết nối cô lập thông qua VPC Peering và tập trung hóa luồng định tuyến đa VPC quy mô lớn bằng AWS Transit Gateway.
* **Vận hành hạ tầng tối ưu chi phí (Serverless Cost Optimization):** Ứng dụng AWS Lambda kết hợp CloudWatch Rules để tự động hóa bật/tắt tài nguyên theo lịch trình, triệt tiêu lãng phí tài chính.

---

### III. Nhật ký hoạt động & Lộ trình phân bổ chi tiết (Từ 12/05/2026 đến 18/05/2026)

| Thời gian | Danh mục hoạt động | Chi tiết các tác vụ thực hiện chuyên sâu | Kết quả/Minh chứng đạt được |
| :--- | :--- | :--- | :--- |
| **Ngày 1** *(12/05)* | Điều phối Container | Triển khai Lab 16: Cấu hình Cluster, Task Definitions đa tầng Frontend/Backend chạy trên AWS Fargate Serverless. | Cụm Microservices thông luồng qua Service Discovery nội bộ. |
| **Ngày 2** *(13/05)* | Tự động hóa CI/CD | Triển khai Lab 17: Thiết lập Pipeline tự động hóa tích hợp liên tục từ GitLab/GitHub Actions thẳng lên cụm ECS Container. | Chu trình phân phối mã nguồn tự động không cần can thiệp thủ công. |
| **Ngày 3** *(14/05)* | An ninh tập trung | Triển khai Lab 18: Kích hoạt AWS Security Hub, rà soát lỗ hổng và phân tích bảng điểm tuân thủ an toàn hạ tầng. | Bản báo cáo kiểm toán an ninh đám mây toàn diện được thiết lập. |
| **Ngày 4** *(15/05)* | Định tuyến Cross-VPC | Triển khai Lab 19: Thiết lập liên kết VPC Peering giữa hai vùng mạng ảo cách ly độc lập, tùy chỉnh Route Tables. | Luồng dữ liệu nội bộ di chuyển xuyên VPC với độ trễ tối thiểu. |
| **Ngày 5** *(16/05)* | Kiến trúc mạng Hub-Spoke | Triển khai Lab 20: Khởi tạo AWS Transit Gateway, đính kèm hệ thống 4 VPCs và phân tách bảng định tuyến tập trung. | Loại bỏ kiến trúc kết nối lưới (Mesh) cồng kềnh, tối ưu quản trị mạng. |
| **Ngày 6** *(17/05)* | Tối ưu chi phí FinOps | Triển khai Lab 22: Lập trình kịch bản AWS Lambda tự động tắt/bật máy chủ EC2 theo mốc thời gian CloudWatch Rules. | Hệ thống tự động tối ưu hóa tài chính, triệt tiêu chi phí nhàn rỗi. |
| **Ngày 7** *(18/05)* | Native CI/CD & Portfolio | Triển khai Lab 23: Xây dựng chuỗi CodePipeline nguyên bản từ AWS. Đóng gói toàn bộ tài liệu, kiểm toán ảnh và xuất bản Worklog. | Portfolio Tuần 4 lên đèn xanh sạch trên hệ thống trang Hugo cá nhân. |

---

### IV. Thực thi kỹ thuật chuyên sâu & Phân tích chi tiết qua các bài Lab

#### **1. Lab 16: Deploy Applications on Amazon Elastic Container Service (Amazon ECS)**

##### **Tổng quan (Overview)**
Trong kỷ nguyên đám mây hiện đại, việc vận hành ứng dụng phụ thuộc vào các máy chủ ảo EC2 đơn lẻ thường bộc lộ những hạn chế lớn về tốc độ co giãn, tính đồng nhất môi trường và gánh nặng quản trị hệ điều hành. Bài Lab này giải quyết triệt để bài toán trên bằng cách hiện đại hóa một ứng dụng doanh nghiệp hai tầng thực tế, thực hiện đóng gói toàn bộ mã nguồn lớp giao diện (Frontend) và lớp nghiệp vụ (Backend) vào các Docker Containers biệt lập, chịu sự điều phối tối cao của **Amazon ECS** trên hạ tầng **AWS Fargate Serverless**.

##### **Khái niệm cốt lõi (Core Concepts)**
* **Amazon ECS Cluster Fargate:** Vùng gom nhóm logic các tài nguyên chạy Container. Điểm ưu việt của Fargate là loại bỏ hoàn toàn các thực thể máy chủ ảo EC2 hiển thị trong tài khoản, giao phó lớp cấp phát phần cứng cho AWS tự động quản lý, nâng tầm an ninh biên lên mức tối đa.
* **Task Definition Topology:** Bản thiết kế chi tiết quy định cách thức Container vận hành (tương tự như tệp `docker-compose.yml`). Khai báo rõ ràng ECR Image URI, giới hạn tài nguyên nghiêm ngặt ở mức tối thiểu để tiết kiệm chi phí (`0.25 vCPU` và `0.5 GiB RAM`), đồng thời tiêm (inject) các biến môi trường cấu hình kết nối.
* **Service Discovery & AWS Cloud Map:** Do các Container chạy Serverless sẽ liên tục được tạo mới và co giãn động khiến địa chỉ IP thay đổi liên tục, hệ thống tích hợp Cloud Map bám sát Route 53 để tự động cập nhật DNS nội bộ (`ecs.local`). Lớp Frontend có thể gọi API của lớp Backend một cách bền vững mà không lo bị mất dấu luồng mạng.

##### **Quá trình triển khai chi tiết (Step-by-step Execution)**

###### **Bước 1: Khởi tạo cụm Cluster điều phối và thiết lập Namespace nội bộ**
Tôi truy cập bảng điều khiển Amazon ECS, tiến hành khởi tạo một cụm điều phối trung tâm đặt tên là `Production-Cluster` chạy hoàn toàn trên Fargate Engine. Quá trình khởi tạo đồng thời kích hoạt tự động trình định danh mạng nội bộ AWS Cloud Map, đăng ký Namespace hệ thống dạng `ecs.local` làm nền tảng cho việc tự động phát hiện dịch vụ.
<img src="/images/week4/1.png" alt="Khởi tạo cụm điều phối Amazon ECS Cluster và cấu hình Namespace" style="max-width:100%; height:auto;" />

###### **Bước 2: Soạn thảo tệp thiết kế Task Definition cho các cấu phần Microservices**
Tôi tiến hành cấu hình Task Definition cho tầng Backend Service Container. Tại mục thiết lập biến môi trường, tôi tiến hành khai báo các chuỗi kết nối và thông số bảo mật trỏ thẳng về cụm cơ sở dữ liệu Amazon RDS MySQL đã thiết lập từ trước, thiết lập các tham số giới hạn phần cứng nghiêm ngặt để giữ tài khoản an toàn trong chuẩn Free Tier.
<img src="/images/week4/2.png" alt="Cấu hình thông số Task Definition cho Backend Service Container" style="max-width:100%; height:auto;" />

###### **Bước 3: Triển khai ECS Services và rà soát chu kỳ sống của các Tasks**
Tôi ra lệnh kích hoạt ECS Services cho cả hai phân tầng ứng dụng, cấu hình số lượng Task mong muốn chạy ngầm độc lập. Di chuyển sang tab Tasks để giám sát, hệ thống ghi nhận các Container thực thể đã tải Image từ ECR về thành công và chuyển trạng thái đồng loạt sang màu xanh hoạt động ổn định (**`RUNNING`**).
<img src="/images/week4/3.png" alt="Giám sát danh sách các Container Task hoạt động ở trạng thái Running" style="max-width:100%; height:auto;" />

###### **Bước 4: Xác thực kết quả thông luồng hệ thống đa tầng thông qua ALB Endpoint**
Để kiểm toán toàn diện tính đúng đắn của hạ tầng, tôi trích xuất địa chỉ DNS công cộng của bộ cân bằng tải Application Load Balancer (ALB) và truy cập bằng trình duyệt cá nhân. Trang quản trị hiển thị giao diện phân phối dữ liệu mượt mà, ghi nhận Frontend Container đã phân giải DNS thành công để gọi Backend Container, thực hiện truy vấn đọc ghi dữ liệu từ cơ sở dữ liệu RDS MySQL lõi một cách hoàn hảo.
<img src="/images/week3/4.png" alt="Xác thực ứng dụng Microservices trên cụm ECS hoạt động thành công trên trình duyệt" style="max-width:100%; height:auto;" />

---

#### **2. Lab 17: Deploying CI/CD with ECS Container - Tự động hóa chu trình phát triển Microservices đa nền tảng**

##### **Tổng quan (Overview)**
Việc quản lý và triển khai các thay đổi mã nguồn (source code) lên một cụm hạ tầng Container một cách thủ công luôn tiềm ẩn rủi ro sai sót lớn và gây lãng phí thời gian của kỹ sư DevOps. Bài Lab này tập trung vào việc hiện thực hóa mô hình tự động hóa chuỗi cung ứng phần mềm **CI/CD (Continuous Integration/Continuous Deployment)**. Hệ thống được thiết kế để tự động hóa toàn bộ các công đoạn: từ việc lắng nghe sự kiện thay đổi mã nguồn, đóng gói Docker Image, đẩy lên kho lưu trữ Amazon ECR, cho đến việc cập nhật Task Definition để tái triển khai không gián đoạn (Zero-Downtime Deployment) trên Amazon ECS.

##### **Khái niệm cốt lõi (Core Concepts)**
* **Chu trình Tích hợp và Triển khai liên tục (CI/CD):** Cơ chế tự động hóa quy trình phân phối phần mềm. Mọi thay đổi khi được Commit/Push lên Git repository sẽ kích hoạt đường ống để kiểm tra, đóng gói và phát hành ứng dụng ngay lập tức.
* **Đường ống Pipeline đa nền tảng (GitLab CI & GitHub Actions):** Tận dụng sức mạnh của các file kịch bản cấu hình kịch bản (như `.gitlab-ci.yml` hoặc `deploy.yml`) để phân tầng chu trình: Lớp biên dịch (Build Stage) chạy lệnh xây dựng Docker Image, và Lớp phát hành (Deploy Stage) gọi AWS API để cập nhật dịch vụ ECS.
* **AWS CodeBuild Integration:** Công cụ biên dịch hoàn toàn do AWS quản lý (Managed Build Service), tự động cung cấp tài nguyên tính toán tạm thời để đóng gói mã nguồn và tự hủy sau khi hoàn tất nhằm tối ưu chi phí.

##### **Quá trình triển khai chi tiết (Step-by-step Execution)**

###### **Bước 1: Thiết lập cấu hình bảo mật môi trường và phân quyền vai trò (IAM Roles)**
Để các công cụ bên ngoài (GitLab Runner, GitHub Actions Enterprise) có quyền tương tác với hạ tầng AWS đám mây, tôi tiến hành khởi tạo một IAM User chuyên dụng có quyền ghi nhận vào kho lưu trữ ECR và cập nhật cụm dịch vụ ECS. Các chuỗi khóa bí mật `AWS_ACCESS_KEY_ID` và `AWS_SECRET_ACCESS_KEY` được mã hóa an toàn bên trong mục *Variables / Secrets* của kho mã nguồn Git.
<img src="/images/week4/5.png" alt="Cấu hình biến môi trường bảo mật trên Git Repository" style="max-width:100%; height:auto;" />

###### **Bước 2: Soạn thảo kịch bản tự động hóa đóng gói Docker Image**
Tôi tiến hành xây dựng file cấu hình Pipeline cho dự án. Kịch bản được lập trình để tự động thực thi lệnh `docker build` nhằm đóng gói mã nguồn thành một đối tượng Image chuẩn, tiếp theo gọi lệnh đăng nhập bảo mật vào Amazon ECR (`aws ecr get-login-password`) và đẩy (Push) tệp tin Image mới lên kho lưu trữ trung tâm kèm theo thẻ định danh phiên bản (Tag) bám sát theo mã Commit Git.
<img src="/images/week4/6.png" alt="Xây dựng kịch bản CI/CD xây dựng và đẩy Docker Image lên ECR" style="max-width:100%; height:auto;" />

###### **Bước 3: Tích hợp AWS CodeBuild và kích hoạt luồng tự động cập nhật Hạ tầng**
Đối với nhánh triển khai gốc AWS native, tôi cấu hình dịch vụ **AWS CodeBuild** để đảm nhận vai trò máy chủ biên dịch. Tệp cấu hình `buildspec.yml` được tối ưu hóa để tự động sinh ra file manifest `imagedefinitions.json` sau khi hoàn tất giai đoạn đóng gói, trực tiếp chỉ định mã định danh Image mới cho ECS Fargate Task.
<img src="/images/week4/7.png" alt="Cấu hình dự án biên dịch tự động trên giao diện AWS CodeBuild" style="max-width:100%; height:auto;" />

###### **Bước 4: Xác thực kết quả triển khai Rolling Update tự động trên Amazon ECS**
Khi thực hiện một lệnh Push code thay đổi giao diện, hệ thống đường ống tự động kích hoạt lập tức. Quan sát trên bảng điều khiển Amazon ECS, dịch vụ Service chuyển sang trạng thái cập nhật cuốn chiếu (Rolling Update) an toàn: Một Task cũ được giữ lại để phục vụ traffic trong khi Task mới chứa mã nguồn cải tiến được kéo lên chạy song song. Khi bài kiểm tra sức khỏe (Health Check) báo trạng thái lành mạnh, Task cũ tự động bị tiêu hủy, hoàn tất chu trình nâng cấp ứng dụng 100% tự động.
<img src="/images/week4/8.png" alt="Xác thực luồng cập nhật Tasks tự động trên cụm hạ tầng Amazon ECS" style="max-width:100%; height:auto;" />

---

#### **3. Lab 18: Getting Started with AWS Security Hub - Quản trị và Định chuẩn An ninh đám mây tập trung**

##### **Tổng quan (Overview)**
Khi quy mô tài nguyên và dịch vụ trên đám mây gia tăng, việc giám sát thủ công từng lỗ hổng bảo mật hay cấu hình sai sót (misconfiguration) trên các dịch vụ riêng lẻ trở nên bất khả thi. Bài Lab này tập trung vào việc thiết lập và vận hành **AWS Security Hub**. Đây là trung tâm quản trị an ninh tối cao, tự động hóa quy trình thu thập, hợp nhất và ưu tiên hóa các cảnh báo bảo mật từ nhiều dịch vụ cốt lõi (như Amazon GuardDuty, Amazon Inspector, Amazon Macie) cũng như các giải pháp từ đối tác AWS để đưa ra một góc nhìn phòng thủ toàn diện.

##### **Khái niệm cốt lõi (Core Concepts)**
* **AWS Security Hub:** Dịch vụ quản lý tư thế an ninh đám mây (Cloud Security Posture Management - CSPM), giúp tập hợp và chuẩn hóa các phát hiện bảo mật (Findings) thành một bảng điều khiển (Dashboard) tương tác trực quan.
* **Tiêu chuẩn kiểm toán bảo mật (Security Standards):** Hệ thống các bộ quy tắc tự động rà soát hạ tầng bám sát theo các tiêu chuẩn quốc tế nghiêm ngặt như **AWS Foundations Security Best Practices** và chuẩn **CIS AWS Foundations Benchmark**.
* **Điểm số tuân thủ (Compliance Score):** Chỉ số phần trăm (%) đánh giá mức độ an toàn của tài khoản dựa trên số lượng bài kiểm tra cấu hình thành công, giúp kỹ sư phát hiện lập tức các điểm yếu hạ tầng để khắc phục (Remediation).

##### **Quá trình triển khai chi tiết (Step-by-step Execution)**

###### **Bước 1: Kích hoạt trung tâm bảo mật AWS Security Hub tập trung**
Tôi truy cập vào bảng điều khiển **AWS Security Hub**, nhấn nút kích hoạt dịch vụ để hệ thống bắt đầu thiết lập quyền hạn và khởi tạo các vai trò dịch vụ liên kết (Service-Linked Roles) cần thiết.
<img src="/images/week4/9.png" alt="Kích hoạt trung tâm bảo mật AWS Security Hub" style="max-width:100%; height:auto;" />

###### **Bước 2: Lựa chọn và định chuẩn các bộ tiêu chuẩn an ninh quốc tế**
Tại mục cấu hình tiêu chuẩn, tôi tiến hành bật các bộ quy chuẩn cốt lõi bao gồm *AWS Foundational Security Best Practices* và *CIS AWS Foundations Benchmark*. Hệ thống sẽ tự động lên lịch trình chạy ngầm các bài kiểm tra cấu hình tự động (Automated Compliance Checks) đối với toàn bộ tài nguyên.
<img src="/images/week4/10.png" alt="Lựa chọn các tiêu chuẩn bảo mật Security Standards" style="max-width:100%; height:auto;" />

###### **Bước 3: Phân tích bảng điều khiển Dashboard và rà soát điểm số an ninh**
Sau khi hệ thống hoàn tất chu kỳ quét hạ tầng, tôi truy cập vào trang Dashboard tổng quan. Màn hình hiển thị biểu đồ phân tích trực quan, phân loại các phát hiện bảo mật theo mức độ nghiêm trọng từ Thấp (`Low`) đến Tối nguy hiểm (`Critical`), đồng thời cung cấp điểm số tuân thủ cụ thể của tài khoản đám mây.
<img src="/images/week4/11.png" alt="Bảng điều khiển trực quan Dashboard hiển thị điểm số tuân thủ Security Hub" style="max-width:100%; height:auto;" />

###### **Bước 4: Trích xuất danh sách lỗ hổng và lập kịch bản xử lý lỗi cấu hình**
Tôi chuyển sang tab **Findings** để lọc ra các cấu hình sai sót có mức độ ưu tiên cao (chẳng hạn như IAM User chưa bật MFA, hoặc Security Group mở cổng port nhạy cảm công khai). Tại đây, Security Hub cung cấp chi tiết đường dẫn tài nguyên bị ảnh hưởng và hướng dẫn từng bước để kỹ sư thực hiện vá lỗi bảo mật.
<img src="/images/week4/12.png" alt="Rà soát danh sách chi tiết các phát hiện bảo mật Findings" style="max-width:100%; height:auto;" />

---

#### **4. Lab 19: Setting Up VPC Peering - Đấu nối liên kết và Định tuyến liên vùng mạng ảo cách ly**

##### **Tổng quan (Overview)**
Theo mặc định, các vùng mạng ảo độc lập Amazon VPC trong môi trường đám mây AWS được cô lập hoàn toàn và không thể giao tiếp trực tiếp với nhau. Bài Lab này tập trung vào việc thiết lập và cấu hình dịch vụ **VPC Peering**. Đây là giải pháp kết nối mạng an toàn, tạo ra một đường ống định tuyến nội bộ giữa hai VPC riêng biệt, giúp các tài nguyên máy chủ có thể chia sẻ dữ liệu trực tiếp với độ trễ thấp tối thiểu mà không cần phải đi vòng ra ngoài môi trường internet công cộng đầy rủi ro.

##### **Khái niệm cốt lõi (Core Concepts)**
* **VPC Peering Connection:** Liên kết mạng logic một-đối-một nối giữa hai mạng VPC. Đường truyền này vận hành dựa trên hạ tầng xương sống của AWS (AWS Backbone Network), đảm bảo lưu lượng dữ liệu luôn được mã hóa và không bao giờ đi qua internet công cộng.
* **Không gian địa chỉ không trùng lặp (Non-overlapping CIDR):** Điều kiện tiên quyết để thiết lập liên kết Peering thành công là dải địa chỉ IP CIDR của hai mạng VPC tuyệt đối không được trùng lặp hoặc giao nhau (ví dụ: `172.31.0.0/16` và `10.10.0.0/16`), tránh gây xung đột khi định tuyến gói tin.
* **Cập nhật Bảng định tuyến hai chiều (Bidirectional Routing):** Việc tạo liên kết Peering chỉ là bước thiết lập cổng kết nối vật lý logic. Để luồng gói tin thực sự lưu thông, kỹ sư bắt buộc phải bổ sung dòng luật định tuyến thủ công vào Route Table của cả hai VPC, chỉ định dải IP đích trỏ thẳng vào cổng Peering Connection ID (`pcx-xxxx`).

##### **Quá trình triển khai chi tiết (Step-by-step Execution)**

###### **Bước 1: Khởi tạo yêu cầu liên kết mạng ảo Peering Connection**
Tôi truy cập bảng điều khiển VPC, chọn mục **Peering connections** và nhấn nút tạo mới. Tôi thiết lập VPC cục bộ của tài khoản thực tập làm bên gửi yêu cầu (Requester) và trỏ chính xác mã định danh của VPC mục tiêu đóng vai trò bên nhận (Accepter), sau đó gửi lệnh khởi tạo.
<img src="/images/week4/13.png" alt="Khởi tạo yêu cầu kết nối Peering Connection" style="max-width:100%; height:auto;" />

###### **Bước 2: Chấp nhận yêu cầu đấu nối và xác thực trạng thái thông suốt**
Chuyển sang vai trò của VPC bên nhận, tôi tiến hành duyệt và bấm chọn **Accept Request** từ menu hành động Actions. Hệ thống đám mây lập tức thiết lập đường ống liên kết, chuyển đổi trạng thái kết nối sang màu xanh hoạt động ổn định (**`Active`**).
<img src="/images/week4/14.png" alt="Chấp nhận yêu cầu đấu nối đưa trạng thái về Active" style="max-width:100%; height:auto;" />

###### **Bước 3: Cấu hình cập nhật Route Tables điều phối gói tin nội bộ**
Để hoàn tất bài Lab, tôi lần lượt truy cập vào các Bảng định tuyến (Route Tables) thuộc phân vùng Public Subnet của cả hai mạng VPC. Tại tab **Routes**, tôi thêm dòng luật định tuyến: nhập dải địa chỉ CIDR của mạng đối phương làm đích đến và chọn Target đầu ra chính là mã liên kết Peering vừa thiết lập để chính thức thông luồng dữ liệu.
<img src="/images/week4/15.png" alt="Cập nhật Route Table bổ sung luật định tuyến Peering" style="max-width:100%; height:auto;" />

---

#### **5. Lab 20: Set Up AWS Transit Gateway - Xây dựng trục mạng trung tâm và Quy hoạch định tuyến Hub-and-Spoke**

##### **Tổng quan (Overview)**
Khi số lượng mạng ảo Amazon VPC trong doanh nghiệp tăng lên, việc kết nối chúng lại với nhau bằng mô hình mạng lưới (Mesh Topology) sử dụng VPC Peering truyền thống sẽ trở nên cực kỳ cồng kềnh, phức tạp và khó kiểm soát. Nếu có $N$ VPC, chúng ta sẽ cần tới $\frac{N(N-1)}{2}$ liên kết Peering riêng biệt. Bài Lab này tập trung giải quyết triệt để bài toán quy mô lớn đó bằng cách thiết lập **AWS Transit Gateway (TGW)**. Đây là một bộ định tuyến đám mây thông minh đóng vai trò là "Hub" trung tâm, kết nối tập trung hệ thống gồm 4 VPCs biệt lập ("Spokes") lại với nhau, giúp đơn giản hóa sơ đồ mạng và tối ưu hóa quản trị định tuyến từ một điểm duy nhất.

##### **Khái niệm cốt lõi (Core Concepts)**
* **AWS Transit Gateway:** Một trung tâm đám mây mạng quản lý tập trung, hoạt động như một bộ định tuyến ảo lớp 3 nâng cao để điều phối và kiểm soát toàn bộ luồng traffic di chuyển giữa các mạng VPC, VPN nội bộ và kết nối AWS Direct Connect.
* **Transit Gateway Attachments:** Tiến trình đấu nối logic các tài nguyên mạng vào Transit Gateway. Bài lab thực hiện đính kèm cả **4 VPCs** độc lập vào TGW, cho phép cổng này bắt đầu tiếp nhận gói tin từ các phân vùng subnet.
* **TGW Route Tables & Isolation Control:** Bảng định tuyến tập trung nằm bên trong Transit Gateway. Bằng cách chia tách các bảng định tuyến và cấu hình cơ chế liên kết (Associations) / truyền bá luật (Propagations) có chủ đích, kỹ sư có thể cô lập hoặc cho phép các VPC giao tiếp với nhau mà không cần cấu hình thủ công tại từng trạm.

##### **Quá trình triển khai chi tiết (Step-by-step Execution)**

###### **Bước 1: Khởi tạo thực thể mạng trung tâm AWS Transit Gateway**
Tôi truy cập vào phân hệ VPC Dashboard, tìm mục **Transit gateways** và tiến hành nhấn nút khởi tạo một Transit Gateway trung tâm đặt tên là `Hub-TGW`. Tôi cấu hình dải ASN (Amazon Side Autonomous System Number) riêng biệt và kích hoạt tính năng tự động chấp nhận các yêu cầu đấu nối tài nguyên.
<img src="/images/week4/16.png" alt="Khởi tạo thực thể bộ định tuyến trung tâm AWS Transit Gateway" style="max-width:100%; height:auto;" />

###### **Bước 2: Đấu nối hệ thống 4 VPCs (Spokes) vào cụm bộ định tuyến trung tâm**
Tôi di chuyển đến mục **Transit gateway attachments** để tiến hành cấu hình luồng kết nối cho các chi nhánh mạng con. Tôi lần lượt tạo 4 lượt đính kèm độc lập, chọn loại tài nguyên liên kết là *VPC*, trỏ chính xác định danh ID của **bốn mạng VPC** mục tiêu và chỉ định các Public Subnets chịu trách nhiệm giao tiếp biên.
<img src="/images/week4/17.png" alt="Cấu hình Transit Gateway Attachments liên kết hệ thống 4 VPCs" style="max-width:100%; height:auto;" />

###### **Bước 3: Cấu hình bảng định tuyến VPC Route Tables hướng tâm**
Để luồng dữ liệu từ các máy chủ ảo nằm trong các VPC có thể tìm đường đi đến bộ định tuyến trung tâm, tôi truy cập vào Bảng định tuyến (Route Tables) nội bộ của từng VPC con. Tại tab **Routes**, tôi thêm dòng luật: định nghĩa dải IP đích của các VPC đối phương (hoặc dải tổng hợp) và chọn Target đầu ra trỏ thẳng về thực thể `Transit Gateway` vừa dựng để chính thức thông suốt toàn bộ trục mạng.
<img src="/images/week4/18.png" alt="Cập nhật Route Table nội bộ của VPC hướng tâm về Transit Gateway" style="max-width:100%; height:auto;" />

---

#### **6. Lab 22: Optimizing EC2 Costs with Lambda - Tối ưu hóa chi phí máy chủ bằng kiến trúc Serverless hướng sự kiện**

##### **Tổng quan (Overview)**
Trong quản trị vận hành điện toán đám mây (FinOps), việc để các máy chủ ảo EC2 thuộc môi trường thử nghiệm (Development/Staging) chạy liên tục 24/7 trong những khoảng thời gian nhàn rỗi (như ban đêm hoặc ngày cuối tuần) gây ra sự lãng phí tài chính rất lớn. Bài Lab này tập trung thiết lập một giải pháp tối ưu hóa chi phí tự động dựa trên kiến trúc hướng sự kiện (Event-Driven Architecture). Bằng cách kết hợp **Amazon CloudWatch Rules (EventBridge)** và hàm tính toán serverless **AWS Lambda**, hệ thống sẽ tự động hóa chu trình bật/tắt máy chủ theo lịch trình cố định mà không cần sự can thiệp thủ công từ quản trị viên.

##### **Khái niệm cốt lõi (Core Concepts)**
* **Kiến trúc hướng sự kiện Serverless:** Mô hình vận hành không phụ thuộc vào máy chủ chạy thường trực. Hàm Lambda chỉ được kích hoạt và tính phí theo số mili-giây xử lý khi nhận được tín hiệu sự kiện từ bộ kích hoạt.
* **CloudWatch Rules / EventBridge Cron Schedule:** Công cụ lập lịch trình tự động dựa trên cú pháp Cron, đóng vai trò phát tín hiệu (Trigger) định kỳ để gọi hàm xử lý.
* **Resource Tagging (Định danh tài nguyên):** Kỹ thuật gán các cặp khóa-giá trị (ví dụ: `Environment: Development`) lên máy chủ EC2, giúp hàm Lambda nhận diện chính xác tập hợp các thực thể cần xử lý mà không làm ảnh hưởng đến môi trường Production.

##### **Quá trình triển khai chi tiết (Step-by-step Execution)**

###### **Bước 1: Thiết lập cơ chế định danh Instance Tags và khởi tạo vai trò IAM Role**
Tôi tiến hành gán một cặp thẻ Tag định danh chuyên dụng lên các máy chủ EC2 cần tối ưu chi phí. Tiếp theo, tại phân hệ IAM, tôi cấu hình một IAM Execution Role cấp quyền cho phép hàm Lambda có đủ đặc quyền thực thi hai lệnh API cốt lõi: `ec2:StartInstances` và `ec2:StopInstances`.
<img src="/images/week4/19.png" alt="Khởi tạo vai trò IAM Role cấp quyền thực thi cho Lambda" style="max-width:100%; height:auto;" />

###### **Bước 2: Lập trình mã nguồn xử lý tự động bật/tắt trên AWS Lambda**
Tôi truy cập vào dịch vụ **AWS Lambda**, tạo một hàm chạy trên môi trường Python và gắn vai trò IAM Role vừa cấu hình. Tôi tiến hành viết đoạn mã kịch bản sử dụng thư viện `boto3` để tự động quét qua danh sách máy chủ, lọc ra các thực thể sở hữu Tag chỉ định và ra lệnh chuyển đổi trạng thái vòng đời của chúng.
<img src="/images/week3/20.png" alt="Soạn thảo mã nguồn xử lý kịch bản Python bên trong AWS Lambda" style="max-width:100%; height:auto;" />

###### **Bước 3: Cấu hình bộ kích hoạt lịch trình CloudWatch Rule và xác thực kết quả**
Để hoàn tất, tôi khởi tạo một quy tắc **CloudWatch Rule** chạy theo cơ chế lịch trình Cron (ví dụ: tự động tắt máy vào 20:00 mỗi tối và bật lại vào 08:00 sáng hôm sau) và cấu hình Target đầu ra trỏ thẳng vào hàm Lambda. Tiến hành kiểm thử giả lập sự kiện, hệ thống phản hồi chính xác, lệnh API được thực thi giúp đưa trạng thái các máy chủ EC2 thử nghiệm về trạng thái dừng hoạt động một cách hoàn hảo, đồng thời bắn thông báo xác nhận thành công.
<img src="/images/week3/21.png" alt="Xác thực kết quả thực thi tắt máy chủ tự động bám sát theo lịch trình sự kiện" style="max-width:100%; height:auto;" />

---

#### **7. Lab 23: Deploy Applications to EC2 with AWS CodePipeline - Chuẩn hóa chu trình CI/CD tự động bằng bộ công cụ AWS Native**

##### **Tổng quan (Overview)**
Bên cạnh việc sử dụng các bên thứ ba, hệ sinh thái AWS cung cấp một bộ giải pháp tích hợp toàn diện giúp xây dựng các đường ống phân phối phần mềm an toàn, khép kín và có khả năng kiểm soát truy cập đồng nhất qua IAM. Bài Lab này tập trung vào việc hiện thực hóa quy trình triển khai tự động một ứng dụng Node.js lên máy chủ ảo EC2 bằng cách kết nối chuỗi dịch vụ native bao gồm **AWS CodeCommit**, **AWS CodeBuild**, **AWS CodeDeploy** dưới sự điều phối tối cao của **AWS CodePipeline**.

##### **Khái niệm cốt lõi (Core Concepts)**
* **AWS CodePipeline:** Trình điều phối chu trình phát triển (Orchestration Service), tự động hóa các giai đoạn kiểm thử, biên dịch và phát hành ứng dụng bám sát theo các mô hình kiểm soát chất lượng (Stage Gates).
* **CodeDeploy Agent & AppSpec File:** Trình tác vụ chạy ngầm bên trong máy chủ EC2 kết hợp với tệp tệp tin cấu hình kịch bản `appspec.yml` để định nghĩa chu kỳ triển khai, quản lý các tệp cấu trúc và kích hoạt kịch bản shell tự động lúc nâng cấp mã nguồn.
* **Quản trị mã nguồn bảo mật (CodeCommit & S3 Artifacts):** Hệ thống lưu trữ mã nguồn Git nội bộ kết hợp phân vùng S3 Bucket mã hóa để trung chuyển các gói dữ liệu (Artifacts) giữa các giai đoạn một cách an toàn và bảo mật cao.

##### **Quá trình triển khai chi tiết (Step-by-step Execution)**

###### **Bước 1: Khởi tạo kho lưu trữ mã nguồn nội bộ AWS CodeCommit**
Tôi truy cập bảng điều khiển CodeCommit, tiến hành tạo một repository bảo mật đặt tên là `NodeJS-App-Repo`. Tiếp theo, cấu hình phân quyền truy cập và thực hiện đẩy (Push) toàn bộ mã nguồn ứng dụng Node.js cùng tệp cấu hình `buildspec.yml` và `appspec.yml` từ máy tính cục bộ lên đám mây.
<img src="/images/week4/22.png" alt="Khởi tạo và đẩy mã nguồn lên kho lưu trữ AWS CodeCommit" style="max-width:100%; height:auto;" />

###### **Bước 2: Cấu hình kịch bản phân phối deployment ứng dụng qua AWS CodeDeploy**
Tôi di chuyển đến mục **AWS CodeDeploy**, khởi tạo một ứng dụng (Application) và nhóm đích triển khai (Deployment Group) ứng dụng. Tôi cấu hình hệ thống trỏ thẳng vào thẻ Tag của máy chủ EC2 đích, chỉ định cơ chế cài đặt deployment cuốn chiếu và gán vai trò IAM Role phù hợp để CodeDeploy Agent trên EC2 có quyền giao tiếp an toàn.
<img src="/images/week4/23.png" alt="Thiết lập nhóm triển khai Deployment Group trên AWS CodeDeploy" style="max-width:100%; height:auto;" />

###### **Bước 3: Đấu nối trục liên kết đường ống tổng thể AWS CodePipeline và kiểm toán kết quả**
Cuối cùng, tôi khởi tạo một đường ống tổng thể **AWS CodePipeline** kết nối tuần tự: lấy mã nguồn từ *CodeCommit Source Stage*, chuyển tiếp sang máy chủ biên dịch *CodeBuild Stage*, và kết thúc tại lớp phát hành *CodeDeploy Stage*. Hệ thống tự động kích hoạt chu trình phân phối, báo trạng thái đồng loạt chuyển sang màu xanh thành công (**`Succeeded`**), giúp ứng dụng Node.js vận hành mượt mà trên môi trường EC2 thực tế.
<img src="/images/week4/24.png" alt="Xác thực trạng thái Succeeded hoàn tất đường ống phân phối tự động AWS CodePipeline" style="max-width:100%; height:auto;" />

---

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
* **Họp nhóm & Định hướng Kiến trúc Dự án Tốt nghiệp:** Tổ chức buổi họp với các thành viên trong nhóm để thảo luận và thống nhất về kiến trúc hệ thống cho đồ án tốt nghiệp (Hệ thống Website Đặt tour du lịch Việt Nam tích hợp Chatbot AI tư vấn thông minh). Nhóm sẽ tiến hành hoạch định ranh giới các microservices, phân chia cấu trúc mã nguồn các kho lưu trữ và lên kế hoạch triển khai tài nguyên hạ tầng trên nền tảng AWS.
* **Tham gia Sự kiện Bootcamp & Kết nối Kỹ thuật:** Tham dự các buổi workshop kỹ thuật và sự kiện chuyên sâu tiếp theo thuộc chương trình Workforce Bootcamp được tổ chức trực tiếp tại văn phòng AWS Việt Nam để tham vấn ý kiến từ các Solutions Architects về các bài toán thắt nút cổ chai (bottleneck) và mô hình đóng gói production tối ưu.
* **Tích lũy kiến thức chuyên sâu:** Dành thời gian nghiên cứu các bài giảng kỹ thuật, các chuỗi video hướng dẫn từ các chuyên gia giải pháp (Solutions Architects) trên YouTube để cập nhật tư duy thiết kế tối ưu, xử lý các bài toán thắt nút cổ chai (Bottleneck) về hiệu năng và chuẩn bị sẵn sàng cho việc đóng gói Container hóa ứng dụng.