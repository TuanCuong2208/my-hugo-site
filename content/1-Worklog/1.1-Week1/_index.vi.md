---
title: "Worklog Tuần 1"
date: 2026-04-21
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---


### I. Tóm tắt tổng quan
Tuần đầu tiên của kỳ thực tập First Cloud AI Journey (FCJ) đóng vai trò là giai đoạn chuyển giao quan trọng. Mục tiêu trọng tâm của tôi là vượt qua mức nhận thức cơ bản về đám mây để thiết lập một môi trường phát triển chuẩn chuyên nghiệp. Điều này không chỉ bao gồm các cấu hình kỹ thuật mà còn là việc tuân thủ "AWS Well-Architected Framework" ngay từ ngày đầu tiên. Kết thúc tuần này, tôi đã bảo mật thành công phạm vi đám mây của mình và chứng minh năng lực kỹ thuật thông qua việc nhận $100 credit khuyến mãi.

### II. Nhật ký hoạt động & Lộ trình chi tiết

| Thời gian | Danh mục hoạt động | Chi tiết các tác vụ thực hiện | Kết quả/Minh chứng |
| :--- | :--- | :--- | :--- |
| **Ngày 1-2** | **Hòa nhập & Bảo mật** | Gia nhập không gian làm việc FCJ. Triển khai giao thức bảo mật cao cho tài khoản Root, bao gồm MFA ảo. | Tài khoản Root đã bảo mật |
| **Ngày 3** | **Nghiên cứu Hạ tầng** | Đi sâu vào Hạ tầng toàn cầu AWS. Phân tích mối quan hệ giữa Regions, Availability Zones (AZs) và Local Zones. | Sơ đồ tư duy hạ tầng |
| **Ngày 4** | **Thiết lập môi trường** | Cài đặt AWS CLI v2, Session Manager Plugin và cấu hình các profile cục bộ. Kiểm tra kết nối bằng STS. | Môi trường CLI sẵn sàng |
| **Ngày 5-6** | **Xác thực kỹ năng** | Tham gia các buổi workshop "Explore AWS" và thực hiện 5 bài lab về AI, Serverless và Database. | **Nhận $100 Credit** |
| **Ngày 7** | **Tài liệu hóa** | Xây dựng cấu trúc Portfolio thực tập trên nền tảng Hugo và kiểm tra các cấu hình chi phí ban đầu. | Portal Nhật ký công việc |

### III. Phân tích kỹ thuật chuyên sâu

#### 1. Quản trị định danh & Bảo mật (IAM)
Tôi đã triển khai một chiến lược IAM chặt chẽ để tránh các sai lầm phổ biến về việc cấp dư thừa quyền hạn:
* **IAM Admin User:** Tạo một người dùng quản trị riêng biệt, chuyển toàn bộ hoạt động hàng ngày ra khỏi tài khoản Root.
* **Triển khai MFA:** Bắt buộc xác thực đa yếu tố cho mọi nỗ lực đăng nhập để giảm thiểu rủi ro mất cắp thông tin xác thực.
* **Phân tích JSON Policies:** Nghiên cứu cấu trúc các chính sách IAM để hiểu cách các câu lệnh `Allow/Deny` tương tác với nhau.

#### 2. Khám phá dịch vụ & Cột mốc $100 Credit
Để nhận được $100 credit, tôi đã triển khai và quản lý thành công tài nguyên trên 5 lĩnh vực khác nhau:
* **Amazon Bedrock (AI/ML):** Đánh giá các Mô hình nền tảng (Foundation Models) khác nhau. Thực hành gọi mô hình qua playground để hiểu về token và độ trễ phản hồi.
* **AWS Lambda (Compute):** Phát triển một hàm serverless cơ bản. Điều này đã thay đổi quan điểm của tôi từ "quản lý máy chủ" sang "tập trung vào logic code".
* **Amazon RDS (Database):** Triển khai một cơ sở dữ liệu quan hệ. Tôi tập trung vào các tính năng "Automated Backup" và "Multi-AZ" để đảm bảo độ bền dữ liệu.
* **Amazon EC2 (Compute):** Khởi chạy một instance T3.micro, cấu hình Security Groups (Cổng 22/80) và truy cập qua SSH.
* **AWS Budgets (Quản trị):** Tạo cảnh báo ngân sách để đảm bảo luôn nằm trong giới hạn của gói Free Tier.

### IV. Thách thức, Xử lý lỗi & Bài học kinh nghiệm
* **Rào cản kỹ thuật:** Gặp lỗi `AccessDenied` khi cố gắng liệt kê các S3 bucket qua CLI.
* **Phân tích nguyên nhân:** User IAM thiếu quyền `s3:ListAllMyBuckets`.
* **Giải pháp:** Chỉnh sửa Inline Policy để cấp quyền S3 cụ thể, tuân thủ nguyên tắc "Quyền hạn tối thiểu". Đây là một bài học quan trọng về bảo mật đám mây.

### V. Suy ngẫm nghề nghiệp
Tuần đầu tiên đã mở ra cho tôi cái nhìn toàn cảnh về quy mô của AWS. Nó không chỉ đơn thuần là "nơi lưu trữ website"; đó là một hệ sinh thái có thể mở rộng, an toàn và tối ưu chi phí. Việc kiếm được $100 credit là một bài kiểm tra thực tế tuyệt vời về khả năng tuân thủ tài liệu kỹ thuật phức tạp dưới áp lực thời gian.

### VI. Lộ trình cho Tuần 2: Giai đoạn "Deep Dive"
Trong tuần tới, tôi sẽ tập trung vào các bài Lab cốt lõi sau:
1. **Lab 1:** IAM nâng cao và Đơn vị tổ chức (OU).
2. **Lab 2:** Virtual Private Cloud (VPC) - Thiết kế cấu trúc mạng tùy chỉnh.
3. **Lab 3:** Elastic Compute Cloud (EC2) - Auto Scaling và Load Balancing.
4. **Lab 4:** Amazon EC2 - Khởi tạo và cấu hình máy chủ ảo Windows/Linux.
5. **Lab 5:** Amazon Relational Database Service (Amazon RDS) - Triển khai và quản trị cơ sở dữ liệu quan hệ.
6. **Lab 6:** Deploying FCJ Management Application with Auto Scaling Group - Tự động co dãn và cân bằng tải hệ thống.