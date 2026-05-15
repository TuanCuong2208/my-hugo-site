---
title: "Tuần 2: Nền tảng Kiến trúc & Các dịch vụ lõi"
date: 2026-04-24
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

# Tuần 2: Làm chủ Hạ tầng AWS - Từ Định danh đến Mạng ảo

### I. Tóm tắt tổng quan
Tuần 2 đánh dấu bước chuyển mình quan trọng từ thiết lập tài khoản cơ bản sang kỹ thuật hạ tầng cốt lõi. Trọng tâm của tuần này gồm hai phần: thiết lập mô hình bảo mật "Zero Trust" bằng AWS IAM và thiết kế mạng ảo cách lập logic thông qua Amazon VPC. Đây là những thành phần tạo nên "nền móng" cho bất kỳ kiến trúc đám mây nào.

### II. Mục tiêu chiến lược trong tuần
* **Thắt chặt IAM:** Chuyển từ việc phụ thuộc vào Root-user sang một môi trường quản trị có cấu trúc, dựa trên các chính sách (Policies).
* **Ảo hóa mạng:** Xây dựng một Virtual Private Cloud (VPC) với các cân nhắc về tính sẵn sàng cao.
* **Vận hành tối ưu:** Duy trì môi trường sạch bằng cách triển khai vòng đời tài nguyên nghiêm ngặt (Tạo - Xác minh - Xóa) để tối ưu hóa chi phí.

### III. Thực thi kỹ thuật chuyên sâu

#### 1. Lab 1: Giới thiệu Hạ tầng Toàn cầu AWS
Trước khi thực hiện các bài lab kỹ thuật, tôi đã nghiên cứu sâu về cách AWS quản lý sự hiện diện vật lý của mình.
* **Regions (Vùng):** Các khu vực địa lý chứa nhiều Miền khả dụng. Tôi đã chọn `us-east-1` (N. Virginia) vì tính ổn định và sự đa dạng của các dịch vụ.
* **Availability Zones (AZs):** Các trung tâm dữ liệu riêng biệt với nguồn điện và mạng dự phòng. Tôi hiểu rằng thiết kế cho tính sẵn sàng cao đòi hỏi phải phân bổ tài nguyên trên nhiều AZ để tránh "điểm chết" duy nhất (SPOF).

#### 2. Lab 2: IAM Access Control - Phân tích sâu về Bảo mật
Mục tiêu là triển khai **Nguyên tắc quyền hạn tối thiểu (PoLP)**.
* **Mổ xẻ JSON Policy:** Tôi đã phân tích cấu trúc của các Chính sách IAM. Mỗi chính sách bao gồm các câu lệnh có: `Effect` (Cho phép/Từ chối), `Action` (Các lệnh gọi API như `s3:ListBucket`), và `Resource` (Định danh ARN cụ thể của tài sản).
* **Cấu hình Người dùng:** Khởi tạo User Admin chuyên dụng để đóng vai trò là người vận hành chính hàng ngày.
![Cấu hình User](/images/week2/iam-create-user-step1.png)
* **Dashboard Bảo mật:** Kích hoạt thành công MFA cho cả tài khoản Root và IAM. Dashboard hiện hiển thị sự tuân thủ 100% với các khuyến nghị bảo mật của AWS.
![IAM Dashboard](/images/week2/iam-dashboard.png)

#### 3. Lab 3: Virtual Private Cloud (VPC) - Khung xương mạng lưới
Xây dựng VPC giống như xây dựng một trung tâm dữ liệu riêng trên đám mây.
* **Chiến lược CIDR Block:** Tôi sử dụng dải mạng `10.0.0.0/16`, cung cấp 65,536 địa chỉ IP nội bộ. Điều này đảm bảo không gian đủ lớn cho việc mở rộng và phân chia subnet sau này.
* **Kiến trúc Public Subnet:** Tôi cấu hình 1 Public Subnet liên kết với một **Internet Gateway (IGW)**. IGW đóng vai trò là cầu nối giữa VPC và internet công cộng.
![Sơ đồ VPC](/images/week2/vpc-architecture.png)
* **Logic định tuyến:** Tôi đã cập nhật **Bảng định tuyến (Route Table)** để bao gồm một tuyến mặc định (`0.0.0.0/0`) trỏ đến IGW, cho phép các tài nguyên trong subnet có thể truy cập internet.
![VPC Thành công](/images/week2/vpc-create-success.png)

### IV. Thách thức, Xử lý lỗi & Góc nhìn chuyên gia
* **"Chi phí ẩn" của NAT Gateway:** Trong quá trình thiết lập, tôi nhận thấy AWS mặc định đề xuất tạo NAT Gateway. Tôi đã chủ động chọn "None" để tránh chi phí không cần thiết trong khi vẫn đạt được mục tiêu bài lab thông qua định tuyến IGW trực tiếp.
* **Stateless vs Stateful:** Tôi đã nghiên cứu sự khác biệt giữa Security Groups (Stateful - Có nhớ trạng thái) và NACLs (Stateless - Không nhớ trạng thái), quyết định tập trung vào Security Groups để bảo vệ cấp độ máy chủ trong giai đoạn tiếp theo.

### V. Suy ngẫm nghề nghiệp
Hiểu được cách một gói tin di chuyển từ Internet Gateway, qua Bảng định tuyến và vào một Subnet cụ thể là kỹ năng giá trị nhất tôi học được tuần này. Kỹ thuật đám mây không phải là "phép thuật" — đó là sự cấu hình chính xác và thiết kế có chủ đích.

### VI. Lộ trình cho Tuần 3: Dịch vụ cốt lõi & Tích hợp Cơ sở dữ liệu
Trong tuần tới, tôi sẽ tập trung vào việc triển khai các khối lượng công việc thực tế thông qua việc tích hợp các dịch vụ tính toán, lưu trữ và cơ sở dữ liệu:
* **Lab 4: Amazon EC2 (Elastic Compute Cloud):** Khởi chạy máy chủ Linux, quản lý Key Pairs và cấu hình Security Groups để cho phép truy cập web.
* **Lab 5: Amazon S3 (Simple Storage Service):** Khám phá lưu trữ đối tượng, lưu trữ trang web tĩnh và quản lý chính sách bucket.
* **Lab 6: Amazon RDS (Relational Database Service):** Triển khai cơ sở dữ liệu MySQL/PostgreSQL và thiết lập kết nối từ máy chủ EC2.