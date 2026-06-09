---
title: "Tuần 2: Nền tảng Kiến trúc & Các dịch vụ lõi"
date: 2026-04-28
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---


### I. Tóm tắt tổng quan
Tuần này đánh dấu một bước chuyển mình mang tính chiến lược và toàn diện trong lộ trình thực tập. Tôi đã dịch chuyển hoàn toàn từ các tư duy nhận thức bề nổi sang việc trực tiếp thiết kế, cấu hình và làm chủ các mảnh ghép hạ tầng cốt lõi nhất trên hệ sinh thái điện toán đám mây AWS. Nội dung nghiên cứu trải dài qua 6 bài Lab lớn: từ việc khảo sát hạ tầng vật lý toàn cầu, thắt chặt an ninh định danh bằng IAM, quy hoạch mạng lưới ảo hóa biệt lập bằng VPC, cho đến việc trực tiếp triển khai bộ ba dịch vụ lõi cấu thành nên một ứng dụng thực tế: Máy chủ tính toán (EC2), Hệ thống lưu trữ đối tượng (S3), và Cơ sở dữ liệu quan hệ quản trị (RDS). 

### II. Mục tiêu chiến lược trong tuần
* **Thắt chặt an ninh định danh (IAM Security):** Hiện thực hóa triệt để mô hình bảo mật "Zero Trust", cô lập hoàn toàn tài khoản Root tối cao và thiết lập môi trường vận hành hàng ngày dựa trên đặc quyền tối thiểu (PoLP).
* **Ảo hóa hạ tầng mạng (VPC Engineering):** Tự tay thiết kế và quy hoạch một vùng mạng ảo cách ly logic, làm chủ các cơ chế định tuyến, phân chia Subnet và quản lý luồng dữ liệu ra vào Internet.
* **Làm chủ tài nguyên tính toán và lưu trữ (Core Infrastructure):** Triển khai, vận hành và tối ưu hóa bộ ba dịch vụ cốt lõi: EC2 (Compute), S3 (Storage), và RDS (Database) dưới mô hình chuẩn hóa.
* **Tối ưu hóa chi phí vận hành (FinOps Integration):** Thiết lập tư duy quản lý vòng đời tài nguyên nghiêm ngặt (Tạo - Xác minh kết quả - Xóa sạch tài nguyên phụ thuộc), loại bỏ hoàn toàn các nguy cơ phát sinh chi phí ngoài ý muốn trên tài khoản Sandbox.

---

### III. Nhật ký hoạt động & Lộ trình phân bổ chi tiết (Từ 28/04/2026 đến 04/05/2026)

| Thời gian | Danh mục hoạt động | Chi tiết các tác vụ thực hiện chuyên sâu | Kết quả/Minh chứng đạt được |
| :--- | :--- | :--- | :--- |
| **Ngày 1-2** *(28-29/04)* | Hòa nhập & Bảo mật | Khảo sát cấu trúc phân tán vật lý toàn cầu của AWS. Triển khai cấu hình phân quyền nâng cao, cô lập tài khoản Root và thiết lập IAM Admin User. | Tài khoản Root được bảo vệ đa lớp bằng Virtual MFA, IAM Admin sẵn sàng vận hành. |
| **Ngày 3** *(30/04)* | Ảo hóa mạng lưới | Quy hoạch cấu trúc mạng nội bộ, khởi tạo Virtual Private Cloud (VPC), phân chia địa chỉ Public Subnet, thiết lập Internet Gateway và tùy chỉnh Route Table. | Hệ thống mạng ảo cách ly logic hoàn chỉnh, sẵn sàng định tuyến gói tin. |
| **Ngày 4** *(01/05)* | Máy chủ ảo | Thực thi quy trình khởi chạy máy chủ ảo Linux, cấu hình tường lửa Security Group chiều Inbound, cấu hình mã hóa User Data để tự động hóa cài đặt Apache Web Server. | Máy chủ phản hồi mượt mà thông qua việc truy cập trực tiếp bằng địa chỉ IP Public. |
| **Ngày 5** *(02/05)* | Lưu trữ đám mây | Khởi tạo S3 Bucket độc nhất toàn cầu, gỡ bỏ cơ chế chặn truy cập công khai mặc định, cấu hình Bucket Policy bằng mã JSON, upload source code tĩnh. | Trang web tĩnh được phân phối diện rộng toàn cầu thông qua AWS Endpoint link. |
| **Ngày 6** *(03/05)* | Cơ sở dữ liệu | Khởi tạo thực thể cơ sở dữ liệu quan hệ MySQL Server thông qua Amazon RDS, kiểm soát cấu hình phần cứng tối thiểu gp3 và db.t3.micro để giữ chuẩn Free Tier. | Cơ sở dữ liệu chuyển trạng thái hoạt động Available, trích xuất thành công Endpoint kết nối. |
| **Ngày 7** *(04/05)* | Tài liệu hóa & FinOps | Tổng hợp toàn bộ nhật ký lỗi (RDS UI bug, IAM Policy), rà soát dọn dẹp sạch tài nguyên phụ thuộc, đóng gói báo cáo Portfolio trên nền tảng Hugo. | Hoàn thiện cấu trúc Portal Nhật ký công việc tuần tự và sạch sẽ. |

---

### IV. Thực thi kỹ thuật chuyên sâu & Phân tích chi tiết qua 6 bài Lab

#### **LAB 1: Giới thiệu Hạ tầng Toàn cầu AWS (AWS Global Infrastructure)**

##### **1. Tổng quan (Overview)**
Trước khi bắt tay vào cấu hình các thực thể kỹ thuật phức tạp, việc thấu hiểu cách thức AWS phân bổ tài nguyên vật lý trên quy mô toàn cầu là điều bắt buộc. Bài nghiên cứu này giúp định hình tư duy thiết kế hệ thống đảm bảo tính sẵn sàng cao (High Availability), khả năng mở rộng không giới hạn (Scalability) và khả năng chống chịu thảm họa (Fault Tolerance).

##### **2. Kiến thức kỹ thuật chuyên sâu (Core Concepts)**
* **AWS Regions (Vùng địa lý):** Là các vị trí địa lý hoàn toàn độc lập trên thế giới, được thiết kế để tuân thủ các quy định nghiêm ngặt về chủ quyền dữ liệu và giảm thiểu độ trễ cho người dùng cuối. Trong suốt chuỗi bài Lab, tôi ưu tiên lựa chọn vùng **`us-east-1` (N. Virginia)** do đây là vùng lõi trung tâm của AWS, có mức chi phí tối ưu nhất và luôn được cập nhật sớm nhất các tính năng kỹ thuật mới.
* **Availability Zones - AZs (Miền khả dụng):** Trong mỗi Region sẽ bao gồm nhiều AZs riêng biệt (tối thiểu là 3). Mỗi AZ cấu thành từ một hoặc nhiều trung tâm dữ liệu vật lý khổng lồ, được trang bị nguồn điện, hệ thống làm mát dự phòng và kết nối với nhau qua mạng lưới cáp quang độ trễ siêu thấp.
* **Tư duy Single Point of Failure (SPOF):** Tôi nhận thức sâu sắc rằng, việc triển khai toàn bộ ứng dụng trên một AZ duy nhất là một sai lầm chí mạng. Khi thiết kế hệ thống, bắt buộc phải phân bổ tài nguyên (như máy chủ hay database) chạy song song trên ít nhất 2 AZs khác nhau. Nếu một trung tâm dữ liệu gặp sự cố vật lý (thiên tai, mất điện diện rộng), luồng traffic sẽ ngay lập tức được chuyển hướng sang AZ còn lại, đảm bảo hệ thống không bị gián đoạn.

##### **3. Kết quả thu được & Phân tích chuyên môn**
* Làm chủ kỹ năng lựa chọn Region tối ưu dựa trên ba tham số cốt lõi: Vị trí người dùng cuối (giảm latency), Tính tuân thủ pháp lý của quốc gia, và Giá thành của từng loại dịch vụ.
* Xây dựng thành công sơ đồ tư duy phân tầng hạ tầng: `AWS Global` $\rightarrow$ `Regions` $\rightarrow$ `Availability Zones` $\rightarrow$ `Edge Locations` (Phục vụ mạng phân phối nội dung CDN CloudFront).

---

#### **LAB 2: AWS IAM Access Control - Thiết lập nền tảng bảo mật đa lớp**

##### **1. Tổng quan (Overview)**
Bảo mật luôn là ưu tiên tối cao trên môi trường đám mây theo mô hình trách nhiệm chia sẻ (Shared Responsibility Model). Bài Lab này tập trung vào việc hiện thực hóa mô hình an ninh mạng **Zero Trust** thông qua dịch vụ AWS Identity and Access Management (IAM), thắt chặt toàn bộ các lối vào hệ thống và ngăn chặn tối đa nguy cơ rò rỉ quyền quản trị.

##### **2. Kiến thức kỹ thuật chuyên sâu (Core Concepts)**
* **Nguyên tắc quyền hạn tối thiểu (Principle of Least Privilege - PoLP):** Đây là kim chỉ nam trong quản trị đám mây. Mọi thực thể (người dùng, ứng dụng, máy chủ) chỉ được cấp phát đúng và đủ những quyền hạn tối thiểu để hoàn thành công việc được chỉ định.
* **Sự nguy hiểm của Root-user:** Tài khoản Root (tạo bằng email đăng ký ban đầu) nắm giữ quyền sinh quyền sát cao nhất, bao gồm cả quyền xóa tài khoản và thay đổi thông tin thanh toán. Do đó, quy tắc bất di bất dịch là: **Cô lập tài khoản Root, khóa nó lại và tuyệt đối không sử dụng cho các tác vụ cấu hình hàng ngày.**
* **Cấu trúc JSON Policy:** Bản chất của mọi sự phân quyền trên AWS đều được định nghĩa qua các văn bản JSON. Tôi đã tiến hành mổ xẻ một IAM Policy tiêu chuẩn và nắm rõ 4 thành phần bắt buộc:
  * `Effect`: Xác định trạng thái chọn (`Allow` hoặc `Deny`).
  * `Action`: Các lệnh gọi API chính xác được hệ thống cho phép hoặc chặn (ví dụ: `ec2:RunInstances`, `s3:CreateBucket`).
  * `Resource`: ARN (Amazon Resource Name) định danh chính xác tuyệt đối tài nguyên nào chịu tác động từ chính sách này.
  * `Condition` (Tùy chọn): Các điều kiện ràng buộc đi kèm (Ví dụ: Chỉ cho phép truy cập nếu IP từ công ty, hoặc trong một khung giờ nhất định).

##### **3. Quá trình thực hiện chi tiết (Step-by-step Execution)**
1. Đăng nhập vào AWS Console bằng tài khoản Root tối cao, tìm kiếm và truy cập vào trang quản trị dịch vụ **IAM**.
2. Di chuyển đến mục **Users** > Chọn **Create user**. Tiến hành khởi tạo một tài khoản người dùng chuyên dụng đặt tên là `Admin-Cuong`.
3. Tại bước thiết lập quyền hạn (Set permissions), tôi không gán quyền trực tiếp cho User để tránh khó quản lý sau này. Thay vào đó, tôi chọn **Create group** đặt tên là `Admins`, gán chính sách quản trị tối cao do AWS quản lý (**`AdministratorAccess`**) vào nhóm này, sau đó thêm User `Admin-Cuong` vào nhóm.
4. Sau khi khởi tạo xong, đăng xuất tài khoản Root. Tiến hành thiết lập cơ chế bảo mật đa lớp **Virtual MFA (Multi-Factor Authentication)** thông qua ứng dụng Google Authenticator trên điện thoại cá nhân cho cả tài khoản Root và tài khoản IAM `Admin-Cuong`. từ đây về sau, mọi thao tác cấu hình hệ thống đều được thực hiện an toàn trên User IAM mới này.

##### **4. Hệ thống ảnh minh chứng (Screenshots Verification)**
<img src="/images/week2/iam-create-user-step1.png" alt="Khởi tạo người dùng IAM" style="max-width:100%; height:auto;" /> : Ảnh chụp màn hình chi tiết bước khởi tạo người dùng IAM mang tên định danh `Admin-Cuong`, thực hiện cấu hình các tham số đăng nhập thông qua giao diện quản trị AWS Management Console.
<img src="/images/week2/iam-dashboard.png" alt="Bảng điều khiển danh tính IAM" style="max-width:100%; height:auto;" /> : Ảnh chụp giao diện tổng quan của bảng điều khiển IAM Dashboard. Màn hình ghi nhận trạng thái tuân thủ an ninh tuyệt đối với các dấu tích xanh, biểu thị tài khoản Gốc (Root) đã được kích hoạt bảo mật đa lớp MFA và tài khoản IAM được phân quyền theo cấu trúc nhiều tầng bảo mật.

---

#### **LAB 3: Virtual Private Cloud (VPC) - Quy hoạch và thiết kế mạng ảo cách ly**

##### **1. Tổng quan (Overview)**
Mạng máy tính là nền móng của mọi hệ thống hạ tầng. Bài Lab này hướng dẫn chi tiết quy trình tự tay thiết kế, tính toán dải IP và xây dựng một mạng ảo biệt lập có tên là **Amazon VPC (Virtual Private Cloud)** trên đám mây, đóng vai trò như một Data Center ảo để bảo vệ các máy chủ ứng dụng bên trong.

##### **2. Kiến thức kỹ thuật chuyên sâu (Core Concepts)**
* **Tính toán dải CIDR Block:** Khi thiết kế VPC, việc chọn dải IP là cực kỳ quan trọng để tránh trùng lặp với mạng nội bộ (On-premises) khi kết nối VPN sau này. Tôi lựa chọn dải IP tiêu chuẩn `10.0.0.0/16`. Sử dụng công thức toán học subnetting, dải này cung cả thảy $2^{(32-16)} = 2^{16} = 65.536$ địa chỉ IP nội bộ hợp lệ.
* **Public Subnet & Internet Gateway (IGW):** Một Subnet được coi là "Public" (Công cộng) khi và chỉ khi nó có một đường vạch rõ ràng trong Route Table trỏ ra Internet Gateway. IGW đóng vai trò như một router biên, thực hiện biên dịch địa chỉ mạng (NAT) từ IP nội bộ của máy chủ sang IP Public để giao tiếp với thế giới bên ngoài.

##### **3. Quá trình thực hiện chi tiết (Step-by-step Execution)**
1. Truy cập vào bảng điều khiển **VPC**. Nhấn nút **Create VPC**, chọn chế độ cấu hình thủ công (*VPC only*), đặt tên mạng là `MyLabVPC` và nhập dải CIDR là `10.0.0.0/16`.
2. Di chuyển đến mục **Subnets** > Chọn **Create subnet**. Chọn VPC vừa tạo, đặt tên phân vùng mạng con này là `Public-Subnet-1A`, chọn Miền khả dụng là `us-east-1a` và gán dải CIDR con hẹp hơn là `10.0.1.0/24` (Cung cấp 256 địa chỉ IP, trong đó AWS giữ lại 5 IP đầu cuối cho mục đích hệ thống).
3. Di chuyển đến mục **Internet Gateways** > Bấm **Create internet gateway**, đặt tên định danh là `MyLab-IGW`. Sau khi tạo xong, bấm vào nút **Actions** > Chọn **Attach to VPC** và trỏ trực tiếp gateway này vào `MyLabVPC`.
4. Di chuyển đến mục **Route Tables** (Bảng định tuyến). Hệ thống tự tạo một bảng định tuyến mặc định (Main Route Table) cho VPC. Tôi tiến hành chọn bảng định tuyến này, chuyển sang tab **Routes** > Chọn **Edit routes**. Tiến hành thêm một dòng định tuyến mới: tại cột *Destination* nhập dải IP đại diện cho toàn bộ internet công cộng là `0.0.0.0/0`, tại cột *Target* chọn đầu ra là `Internet Gateway` và trỏ vào cái `MyLab-IGW` vừa tạo. Bấm lưu lại để chính thức thông mạng ra ngoài cho Public Subnet.

##### **4. Hệ thống ảnh minh chứng (Screenshots Verification)**
<img src="/images/week2/vpc-architecture.png" alt="Sơ đồ kiến trúc mạng VPC" style="max-width:100%; height:auto;" /> : Sơ đồ tư duy quy hoạch phân vùng mạng, cấu trúc chia nhỏ các dải IP CIDR và luồng di chuyển của gói tin đi qua cổng Internet Gateway biên.
<img src="/images/week2/vpc-create-success.png" alt="Khởi tạo VPC thành công" style="max-width:100%; height:auto;" /> : Bảng tổng hợp trạng thái trên AWS Console xác nhận hệ thống mạng `MyLabVPC` đã chuyển sang trạng thái hoạt động (Active), đính kèm chính xác bảng định tuyến Route Table chứa dòng luật `0.0.0.0/0 -> igw`.

---

#### **LAB 4: Amazon Elastic Compute Cloud (EC2) - Triển khai tự động hóa Virtual Web Server**

##### **1. Tổng quan (Overview)**
Sau khi đã dựng xong bộ khung bảo mật và mạng lưới, bài Lab này tiến hành khai thác tài nguyên tính toán core bằng cách khởi chạy một máy chủ ảo dựa trên dịch vụ **Amazon EC2 (Elastic Compute Cloud)**. Để tối ưu hóa quá trình triển khai thực tế, tôi áp dụng kỹ thuật tự động hóa script (User Data) nhằm biến một máy chủ thô thành một Apache Web Server hoạt động hoàn chỉnh mà không cần can thiệp thủ công bằng lệnh SSH sau khi bật máy.

##### **2. Kiến thức kỹ thuật chuyên sâu (Core Concepts)**
* **Hệ điều hành thế hệ mới (Amazon Linux 2023 - AL2023):** Đây là hệ điều hành Linux tiêu chuẩn được AWS tối ưu hóa sâu, loại bỏ các package thừa thãi để tăng tốc độ khởi động, tăng cường bảo mật và tích hợp sẵn trình quản lý package thế hệ mới `dnf` thay thế cho `yum` cũ.
* **Cơ chế tường lửa Security Group (Stateful):** Security Group đóng vai trò là một tường lửa ảo kiểm soát traffic ở cấp độ lớp mạng của từng máy chủ ảo riêng biệt. Do có đặc tính **Stateful (Nhớ trạng thái)**, nếu tôi mở một cổng Inbound (chiều đi vào, ví dụ cổng 80 cho người dùng xem web), thì tự động luồng Outbound (chiều phản hồi dữ liệu ngược ra từ máy chủ) sẽ được mở tự động mà không cần phải cấu hình thêm bất kỳ luật phản hồi nào ở chiều ra.
* **Sức mạnh của User Data Automation:** AWS cho phép dán một đoạn kịch bản shell script chạy ở đặc quyền tối cao `root` vào thời điểm máy chủ boot lần đầu tiên. Điều này giúp chuẩn hóa quy trình cài đặt phần mềm môi trường nền tảng một cách đồng loạt và nhất quán.

##### **3. Quá trình thực hiện chi tiết (Step-by-step Execution)**
1. Tại giao diện bảng điều khiển **EC2**, nhấn nút màu cam **Launch instance**. tại mục *Name*, đặt tên định danh cho máy chủ ảo này là `MyWebServer`.
2. Tại mục *Application and OS Images (AMI)*, tích chọn vào hệ điều hành **Amazon Linux 2023 AMI** bản 64-bit chuẩn tối ưu.
3. Tại mục *Instance type*, lựa chọn dòng chip phần cứng là **`t2.micro`** (Cung cấp cấu hình lõi đơn 1 vCPU và bộ nhớ 1 GiB RAM) để đảm bảo máy chủ chạy hoàn toàn trong hạn mức miễn phí Free Tier của hệ thống AWS.
4. Tại mục *Key pair (login)*, bấm tạo một cặp khóa bảo mật mới đặt tên là `my-key`. Hệ thống sẽ tự động tải một file có tên `my-key.pem` về máy tính cá nhân. File này chứa private key dùng để mã hóa và giải mã khi thực hiện các kết nối quản trị bảo mật SSH sau này.
5. Tại mục *Network settings*, nhấn vào nút **Edit**. Sửa lựa chọn mặc định, trỏ máy chủ vào đúng cái mạng ảo **`MyLabVPC`** và phân vùng **`Public-Subnet-1A`** đã tự tay thiết kế ở bài Lab 3. Tại dòng *Auto-assign public IP*, chọn **Enable** để máy chủ được AWS cấp phát cho một địa chỉ IP công cộng duy nhất khi lên đèn hoạt động.
6. Ngay bên dưới phần mạng, khởi tạo một Security Group mới đặt tên là `Web-SG`. Thiết lập hai dòng luật Inbound quy chuẩn bảo mật:
   * Dòng 1: Loại hình `SSH`, cổng mặc định `22`, nguồn chọn `My IP` (Chỉ cho phép máy tính cá nhân của tôi có quyền truy cập terminal quản trị).
   * Dòng 2: Loại hình `HTTP`, cổng mạng tiêu chuẩn `80`, nguồn chọn Any IPv4 (`0.0.0.0/0`) để cho phép toàn bộ người dùng trên mạng toàn cầu có thể truy cập vào website.
7. Kéo xuống dưới cùng trang, mở rộng mục **Advanced details**. Cuộn chuột xuống ô cuối cùng có tên là **User data**, tiến hành dán chính xác đoạn mã cấu hình kịch bản shell tự động cài cắm môi trường sau:
   ```bash
   #!/bin/bash
   # Thực hiện cập nhật toàn bộ hệ thống thư viện core của hệ điều hành
   sudo dnf update -y
   # Tiến hành tải và cài đặt phần mềm Apache Web Server (httpd)
   sudo dnf install httpd -y
   # Kích hoạt tiến trình Apache hoạt động ngay lập tức
   sudo systemctl start httpd
   # Cấu hình cho phép Apache tự động khởi động cùng hệ điều hành khi reboot máy chủ
   sudo systemctl enable httpd
   # Ghi đè mã nguồn HTML vào tệp tin index mặc định để kiểm tra kết quả ứng dụng
   echo "<h1>Welcome to My AWS Web Server running on Docker infrastructure context!</h1>" > /var/www/html/index.html
8. Nhấn nút màu cam **Launch instance** ở góc phải màn hình để ra lệnh cho hạ tầng AWS khởi tạo máy chủ thực tế.

##### **4. Hệ thống ảnh minh chứng (Screenshots Verification)**
<img src="/images/week2/anh1.png" alt="Đặt tên máy chủ EC2" style="max-width:100%; height:auto;" /> : Ảnh chụp màn hình bước đặt tên máy chủ `MyWebServer` và lựa chọn hệ điều hành Amazon Linux 2023 AMI từ kho lưu trữ.
<img src="/images/week2/anh2.png" alt="Cấu hình phần cứng và Key Pair" style="max-width:100%; height:auto;" /> : Minh chứng cấu hình phần cứng giới hạn `t2.micro` và bước khởi tạo thành công cặp khóa private key bảo mật `my-key.pem`.
<img src="/images/week2/anh3.png" alt="Cấu hình Security Group mạng lưới" style="max-width:100%; height:auto;" /> : Ảnh chụp toàn bộ bảng Network Settings, ghi nhận việc đưa máy chủ vào dải mạng tùy chỉnh `MyLabVPC`, gán IP Public và cấu hình mở tường lửa cổng 80 công cộng.
<img src="/images/week2/anh4.png" alt="Cấu hình tự động hóa User Data" style="max-width:100%; height:auto;" /> : Ảnh chụp chi tiết ô cấu hình nâng cao User Data, hiển thị nguyên vẹn đoạn script shell cài cắm tự động dịch vụ web Apache.
<img src="/images/week2/anh5.png" alt="Máy chủ hoạt động Running" style="max-width:100%; height:auto;" /> : Giao diện danh sách máy chủ hoạt động, hiển thị dòng máy chủ `MyWebServer` chuyển màu xanh `Running` rực rỡ và vượt qua bài kiểm tra sức khỏe 2/2 checks passed của AWS hạ tầng.
<img src="/images/week2/anh6.png" alt="Kiểm tra trình duyệt truy cập Web Server" style="max-width:100%; height:auto;" /> : Ảnh chụp thực tế trình duyệt Chrome của máy cá nhân. Khi gõ địa chỉ IP Public của máy chủ vào thanh URL, trang web lập tức hiển thị dòng chữ tiêu đề lớn *"Welcome to My AWS Web Server..."*, chứng minh toàn bộ script tự động hóa hoạt động hoàn hảo 100%.

---

#### **LAB 5: Amazon Simple Storage Service (S3) - Phân phối mã nguồn thông qua Static Website Hosting**

##### **1. Tổng quan (Overview)**
Khi khối lượng tệp tin (hình ảnh, mã nguồn giao diện frontend HTML/CSS/JS) tăng lên, việc lưu trữ trực tiếp trên ổ đĩa của máy chủ EC2 sẽ gây lãng phí tài nguyên tính toán và khó mở rộng. Bài Lab này hướng dẫn cách khai thác dịch vụ lưu trữ đối tượng dẫn đầu thị trường – **Amazon S3 (Simple Storage Service)**, đồng thời cấu hình tính năng Static Website Hosting để biến một thùng chứa dữ liệu thuần túy thành một địa chỉ phân phối trang web tĩnh hiệu năng cao, chịu tải hàng triệu user với chi phí gần như bằng 0.

##### **2. Kiến thức kỹ thuật chuyên sâu (Core Concepts)**
* **Kiến trúc lưu trữ đối tượng (Object Storage):** S3 không quản lý dữ liệu theo dạng cây thư mục phân cấp giống như ổ cứng thông thường, mà quản lý theo dạng phẳng dưới dạng các Đối tượng (Objects). Mỗi đối tượng bao gồm: Dữ liệu thô (File dữ liệu), Định danh Metadata (Các thuộc tính mô tả như kiểu file, ngày tạo), và một chuỗi Key duy nhất làm đường dẫn định danh.
* **Tính độc nhất toàn cầu của S3 Bucket Name:** Khi tạo một thùng chứa (Bucket) trên S3, cái tên bạn đặt bắt buộc phải là duy nhất trên toàn bộ hệ thống toàn cầu của AWS chứ không chỉ riêng trong tài khoản của bạn. Điều này là do AWS sẽ dùng chính cái tên bucket đó để map trực tiếp thành một đường link domain truy cập internet công cộng.
* **Cơ chế phân quyền Bucket Policy nâng cao:** Mặc định khi tạo mới, toàn bộ dữ liệu trong S3 đều ở chế độ bảo mật tuyệt đối (Private). Để biến nó thành website tĩnh phân phối diện rộng, ta phải viết một đoạn mã JSON định nghĩa quyền. Đoạn mã này sử dụng ký tự đại diện `*` tại mục Principal để biểu thị: Cho phép tất cả mọi người dùng internet có quyền thực thi hành động đọc tệp (`s3:GetObject`).

##### **3. Quá trình thực hiện chi tiết (Step-by-step Execution)**
1. Trên thanh tìm kiếm đầu trang AWS Console, gõ dịch vụ **S3** và bấm chọn. Tại giao diện trang, bấm nút màu cam **Create bucket**.
2. Tại ô *Bucket name*, nhập một cái tên duy nhất toàn cầu (Ví dụ: `cuong-static-website-2026`). Tại mục *Region*, giữ nguyên vùng `us-east-1` đồng bộ hạ tầng mạng.
3. Kéo xuống mục cấu hình an toàn *Block Public Access settings for this bucket*. Tiến hành bỏ tích chọn tại ô trống tối cao **"Block all public access"**. Việc này giống như ta mở chốt một ổ khóa bảo vệ, chấp nhận rằng bucket này có khả năng công khai dữ liệu ra ngoài internet nếu được phân quyền. Tích chọn vào ô cam xác nhận bên dưới để đồng ý với thiết lập. Kéo xuống cuối trang bấm **Create bucket**.
4. Bấm click chọn trực tiếp vào tên bucket `cuong-static-website-2026` vừa tạo thành công trên danh sách. Di chuyển sang tab có tên là **Properties** (Thuộc tính). Kéo cuộn chuột xuống vị trí cuối cùng của trang tìm mục **Static website hosting** > Chọn **Edit**.
5. Chuyển trạng thái từ *Disable* sang **Enable**. Tại dòng *Hosting type*, tích chọn ô *Host a static website*. Tại ô chỉ mục *Index document*, nhập chính xác tên tệp tin trang chủ cấu trúc là `index.html`. Bấm lưu lại cấu hình. Lúc này, AWS sẽ tự động sinh ra một chuỗi địa chỉ liên kết có tên là *Bucket website endpoint* ở cuối trang.
6. Chuyển tiếp sang tab có tên là **Permissions** (Quyền truy cập). Tìm đến mục **Bucket policy** > Chọn **Edit**. Tiến hành dán đoạn mã định dạng cấu trúc JSON phân quyền đọc dữ liệu công khai chuẩn xác sau vào trình soạn thảo:
   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "PublicReadGetObject",
               "Effect": "Allow",
               "Principal": "*",
               "Action": "s3:GetObject",
               "Resource": "arn:aws:s3:::cuong-static-website-2026/*"
           }
       ]
   }
*(Lưu ý kỹ thuật: Ký tự `/*` ở cuối chuỗi Resource biểu thị áp dụng quyền đọc cho toàn bộ tất cả các file nằm bên trong bucket này).* Bấm lưu lại chính sách.

7. Quay trở lại tab đầu tiên **Objects**. Bấm nút **Upload** > Chọn **Add files** và chọn một file code giao diện `index.html` sẵn có từ máy tính cá nhân để tải lên hệ thống.

##### **4. Hệ thống ảnh minh chứng (Screenshots Verification)**
<img src="/images/week2/anh7.png" alt="Khởi tạo S3 Bucket thành công" style="max-width:100%; height:auto;" /> : Giao diện trang khởi tạo S3 Bucket thành công, ghi nhận việc cấu hình tên định danh độc nhất và bước gỡ bỏ thành công tấm khiên chắn truy cập công khai mặc định.
<img src="/images/week2/anh8.png" alt="Kích hoạt Static Website Hosting" style="max-width:100%; height:auto;" /> : Ảnh chụp màn hình mục Properties xác nhận tính năng Static website hosting đã bật sang chế độ xanh hoạt động kèm việc khai báo tệp chỉ mục mặc định `index.html`.
<img src="/images/week2/anh9.png" alt="Soạn thảo cấu trúc Bucket Policy" style="max-width:100%; height:auto;" /> : Ảnh chụp giao diện soạn thảo Bucket Policy, hiển thị trọn vẹn đoạn mã JSON phân quyền truy cập đọc file diện rộng mà không phát sinh bất kỳ lỗi cú pháp nào.
<img src="/images/week2/anh10.png" alt="Upload index html thành công" style="max-width:100%; height:auto;" /> : Bảng danh sách quản lý đối tượng hiển thị trạng thái tệp tin mã nguồn `index.html` đã được upload thành công lên đám mây, báo trạng thái *Succeeded* màu xanh.
<img src="/images/week2/anh11.png" alt="Kiểm tra giao diện qua link Endpoint S3" style="max-width:100%; height:auto;" /> : Ảnh chụp giao diện website hoàn thiện chạy mượt mà trên trình duyệt khi người dùng click trực tiếp vào đường link URL Endpoint do dịch vụ S3 phân phối toàn cầu.

---

#### **LAB 6: Amazon Relational Database Service (RDS) - Khởi tạo hạ tầng Cơ sở dữ liệu quan hệ quản trị**

##### **1. Tổng quan (Overview)**
Mảnh ghép cuối cùng để cấu thành nên cấu trúc của một ứng dụng hoàn chỉnh chính là nơi lưu trữ dữ liệu có cấu trúc. Bài Lab này hướng dẫn chi tiết quy trình tự tay triển khai một thực thể cơ sở dữ liệu quan hệ mã nguồn mở phổ biến nhất thế giới – **MySQL Server** thông qua dịch vụ dịch vụ quản trị tự động **Amazon RDS (Relational Database Service)**. Điểm cốt lõi của bài lab là xử lý các xung đột giao diện để đưa cấu hình phần cứng về mức tối thiểu, đảm bảo tài khoản chạy an toàn trong hạn mức Free Tier.

##### **2. Kiến thức kỹ thuật chuyên sâu (Core Concepts)**
* **Sự ưu việt của Managed Database Service (RDS):** Nếu ta tự cài MySQL lên một máy chủ EC2, ta phải tự tay lo liệu từ việc vá lỗi hệ điều hành, cấu hình sao lưu (Backup), đến việc thiết lập cụm dự phòng (Replication). Sử dụng Amazon RDS, toàn bộ các tác vụ quản trị hạ tầng nặng nề đó đều được AWS tự động hóa hoàn toàn, giúp lập trình viên tập trung 100% vào việc tối ưu hóa truy vấn SQL.
* **Cơ chế Endpoint và Topology kết nối:** Khi khởi tạo xong một Database trên RDS, hệ thống sẽ hoàn toàn không cấp địa chỉ IP tĩnh để kết nối trực tiếp. Thay vào đó, AWS cung cấp một chuỗi ký tự DNS định danh duy nhất gọi là **Endpoint**. Khi cấu hình các ứng dụng Backend (như Spring Boot, Next.js hay NestJS), lập trình viên sẽ trỏ chuỗi Endpoint này vào file biến môi trường để thực hiện các phiên truy vấn dữ liệu bảo mật qua cổng mạng mặc định `3306`.

##### **3. Quá trình thực hiện chi tiết (Step-by-step Execution)**
1. Trên thanh tìm kiếm tối cao của AWS Console, gõ chữ `RDS`. Tại danh sách hiện ra, bấm chọn vào dịch vụ **Aurora and RDS** (Có biểu tượng hình khối vuông màu xanh dương).
2. Tại bảng điều khiển chính, nhấn nút màu cam **Create database**. Tiến hành cấu hình chi tiết theo các tham số kỹ thuật chuẩn hóa sau:
   * *Choose a database creation method*: Tích chọn ô **Standard create** để hiển thị toàn bộ tất cả các quyền kiểm soát thông số phần cứng từ gốc.
   * *Engine options*: Bấm chọn ô hình con cá heo đại diện cho hệ quản trị cơ sở dữ liệu **MySQL**.
   * *Templates*: Cuộn chuột xuống dưới. Do giao diện cập nhật mới nhất của AWS đã thay đổi thuật ngữ, tại đây tôi bấm chọn vào ô mẫu **Dev/Test** (hoặc gói cấu hình tương đương Sandbox) để hệ thống cho phép hạ cấu hình máy về mức tiết kiệm tối đa.
3. Tại mục cấu hình tài khoản định danh **Settings**:
   * *DB instance identifier*: Đặt tên quản trị cho con database này là `my-docker-db`.
   * *Master username*: Giữ nguyên định danh mặc định hệ thống là `admin`.
   * *Credentials management*: Tích chọn ô *Self managed*. Tại ô mật khẩu *Master password* và ô xác nhận *Confirm master password*, tiến hành nhập chính xác chuỗi ký tự: **`DockerDB.2026`**. *(Lưu ý kỹ thuật cốt lõi: Tuyệt đối không chứa ký tự đặc biệt `@` do quy định của bộ giải mã RDS AWS sẽ tính đây là ký tự lỗi cú pháp và khóa menu chọn cấu hình bên dưới).*
4. Tại mục cấu hình tài nguyên **Instance configuration**:
   * Tại ô menu thả xuống *Instance type, bấm chọn dòng máy ảo tiết kiệm tài nguyên nhỏ nhất là **`db.t3.micro`** (Cung cấp cấu hình lõi kép 2 vCPUs và bộ nhớ ram 1 GiB RAM), đây là dòng chip nằm trọn vẹn trong danh mục bảo trợ miễn phí Free Tier của AWS.
5. Tại mục cấu hình dung lượng ổ đĩa **Storage**:
   * *Storage type*: Bấm chọn dòng công nghệ ổ cứng mới tối ưu hiệu năng là **General Purpose SSD (gp3)**.
   * *Allocated storage*: Xóa bỏ hoàn toàn con số mặc định dung lượng lớn của hệ thống, nhập vào chính xác con số dữ liệu nhỏ là **`20` GiB** (Mức dung lượng lưu trữ tiêu chuẩn được AWS cấp phát miễn phí cho mục đích học tập).
6. Kéo thẳng xuống cuối trang, giữ nguyên toàn bộ các thông số mặc định an toàn khác và nhấn nút màu cam lớn **Create database**. Hệ thống sẽ chuyển hướng quay trở về danh sách quản trị chính của RDS Databases.

##### **4. Hệ thống ảnh minh chứng (Screenshots Verification)**
<img src="/images/week2/anh12.png" alt="Lựa chọn cấu hình Engine MySQL" style="max-width:100%; height:auto;" /> : Ảnh chụp màn hình bước lựa chọn Engine MySQL kết hợp với việc tích chọn phân vùng mẫu mã nguồn Dev/Test trên giao diện tạo mới Database RDS.
<img src="/images/week2/anh13.png" alt="Hạ bậc cấu hình db t3 micro và ổ đĩa 20GB" style="max-width:100%; height:auto;" /> : Minh chứng ghi nhận việc khai báo thành công mật khẩu bảo mật chuẩn không chứa ký tự cấm và bước hạ bậc cấu hình chip về dòng `db.t3.micro` cùng phân vùng ổ đĩa gp3 giới hạn 20 GiB dữ liệu.
<img src="/images/week2/anh14.png" alt="Trạng thái cơ sở dữ liệu Available" style="max-width:100%; height:auto;" /> : Ảnh chụp bảng danh sách Databases hoàn thiện. Dòng tên cơ sở dữ liệu `my-docker-db` đã chuyển màu từ trạng thái khởi tạo sang trạng thái xanh hoạt động ổn định hoàn toàn là **`Available`**, đồng thời hiển thị trọn vẹn chuỗi địa chỉ liên kết Endpoint sẵn sàng cho các kết nối backend tương lai.

---

### V. Thách thức hạ tầng, Nhật ký xử lý lỗi & Góc nhìn từ chuyên gia

Trong suốt quá trình thực thi chuỗi 6 bài Lab hạ tầng phức tạp tuần này, tôi đã liên tục đối mặt với các bài toán thực tế và rút ra được những bài học kinh nghiệm xương máu:

* **Bài toán "Chi phí ẩn" từ NAT Gateway tự động:** Khi thực hiện quy hoạch sơ đồ mạng lưới tại bài Lab 3 (VPC), trình cấu hình tự động thuật toán của AWS liên tục đưa ra khuyến nghị khởi tạo hệ thống bao gồm kèm theo 1 NAT Gateway để phục vụ mạng Private. Bằng việc phân tích sâu bảng chi phí hạ tầng, tôi nhận ra NAT Gateway được tính phí theo giờ chạy thực tế rất đắt đỏ ($0.045/hour) vượt ngoài phạm vi tài khoản học tập. Tôi đã chủ động chọn cấu hình mạng "None" cho mục này, đưa toàn bộ luồng kết nối đi trực tiếp qua Internet Gateway biên để giải quyết trọn vẹn mục tiêu bài học mà không làm phát sinh hóa đơn tiền tỷ cho tài khoản Sandbox.
* **Lỗi xung đột giao diện khóa menu phần cứng (RDS UI Bug Loop):** Thách thức lớn nhất tuần nằm ở bài Lab 6 khi giao diện tạo mới của AWS RDS liên tục bị đơ và khóa xám (Disable) toàn bộ menu chọn chip máy chủ, hiện lỗi đỏ kẹt vòng lặp tại mục ổ đĩa. Qua quá trình đào sâu tìm kiếm nguyên nhân, tôi phát hiện ra đây là một Bug UI khét tiếng trên bảng điều khiển mới khi tài khoản sử dụng các mật khẩu mạnh chứa ký tự `@` (Ví dụ: `DockerDB@2026`). Trình parse cú pháp của AWS RDS nhận diện nhầm ký tự `@` là một phần của chuỗi định tuyến phân giải tên miền nội bộ nên khóa toàn bộ tiến trình phía sau. Bằng việc làm sạch mật khẩu chuyển sang dấu chấm phân cách `DockerDB.2026` và chủ động ép chọn loại ổ đĩa gp3 trước, hệ thống đã lập tức mở khóa trở lại dòng máy chủ `db.t3.micro`.
* **Phân tích chiều sâu cơ chế an ninh lớp mạng (Stateless vs Stateful):** Tôi đã dành nhiều thời gian để mổ xẻ bản chất vận hành của hai lá chắn bảo mật trên mạng ảo AWS: Security Groups và Network ACLs (NACLs). Security Groups hoạt động ở cấp độ thực thể máy chủ ảo và mang tính chất **Stateful (Có nhớ trạng thái)**, giúp đơn giản hóa luồng cấu hình vì chỉ cần quan tâm mở cổng chiều vào. Ngược lại, Network ACLs hoạt động ở cấp độ bao bọc toàn bộ phân vùng Subnet và mang tính chất hoàn toàn **Stateless (Không nhớ trạng thái)** – nghĩa là nếu mở cổng chiều vào (Inbound), ta bắt buộc phải viết thêm một dòng luật thủ công mở chính xác cổng dải động (Ephemeral Ports 1024-65535) ở chiều phản hồi ra (Outbound) thì gói tin mới có thể lưu thông, nếu không hệ thống sẽ bị chặn đứng hoàn toàn.

---

### VI. Suy ngẫm nghề nghiệp (Professional Reflections)

Việc tự tay cấu hình thành công và nhìn thấy một gói tin dữ liệu di chuyển một cách tuần tự: từ môi trường internet công cộng bên ngoài, xuyên qua cổng router biên Internet Gateway, được dẫn hướng chính xác bởi các dòng luật định tuyến trong Route Table để tiếp cận vào đúng địa chỉ máy chủ ảo EC2 nằm sâu trong phân vùng Subnet, rồi từ đó thực thi các phiên kết nối truy vấn dữ liệu an toàn sang thực thể RDS Database là trải nghiệm công nghệ giá trị nhất mà tôi tích lũy được cho đến thời điểm hiện tại.

Kỹ nghệ kiến trúc điện toán đám mây (Cloud Engineering) hoàn toàn không phải là những hành động bấm chuột may rủi, ngẫu nhiên dựa trên giao diện đồ họa trực quan. Đó là một bộ môn khoa học đòi hỏi sự tư duy logic mạch lạc, tính toán dải địa chỉ chính xác tuyệt đối và thiết kế hạ tầng có chủ đích dựa trên các bộ quy tắc, tiêu chuẩn kiến trúc tối ưu (*AWS Well-Architected Framework*). Việc làm chủ hạ tầng core này là bệ phóng vững chắc để tôi tiếp tục tiến sâu vào các bài toán đóng gói ứng dụng container hóa tự động ở các giai đoạn thực tập tiếp theo.

---

### VII. Kế hoạch chiến lược & Lộ trình tối ưu cho tuần tiếp theo

Để chuẩn bị hành trang cho các giai đoạn chuyên sâu tiếp theo của dự án và tối ưu hóa năng lực kiến trúc hệ thống, lộ trình hành động trong tuần tới sẽ tập trung triển khai các mũi nhọn sau:

* **Mở rộng chuỗi bài Lab nâng cao:** Tiếp tục thiết kế và thực thi thực tế các bài Lab chuyên sâu tiếp theo trên nền tảng AWS Sandbox nhằm làm chủ các cơ chế tự động mở rộng (Auto Scaling), cân bằng tải (Elastic Load Balancing) và giám sát hệ thống (CloudWatch).
* **Nghiên cứu Module ứng dụng thực tế:** Khai thác sâu các nguồn tài nguyên học tập chất lượng cao trên nền tảng YouTube nhằm phân tích cấu trúc, sơ đồ kiến trúc lớp và cách thức tích hợp các module chức năng phức tạp vào hệ thống đám mây.
* **Tích lũy kiến thức chuyên sâu:** Dành thời gian nghiên cứu các bài giảng kỹ thuật, các chuỗi video hướng dẫn từ các chuyên gia giải pháp (Solutions Architects) trên YouTube để cập nhật tư duy thiết kế tối ưu, xử lý các bài toán thắt nút cổ chai (Bottleneck) về hiệu năng và chuẩn bị sẵn sàng cho việc đóng gói Container hóa ứng dụng.