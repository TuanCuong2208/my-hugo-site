---
title: "Tuần 3: Triển khai Máy chủ và Lưu trữ đám mây"
date: 2026-05-05
weight: 3
chapter: false
pre: "<b>3. </b>"
---

Trong tuần này, tôi bắt đầu triển khai các thành phần chính của một hệ thống thực tế trên AWS, bao gồm máy chủ ảo (EC2), kho lưu trữ (S3) và cơ sở dữ liệu (RDS).

## 4. Lab 4: Amazon EC2 - Virtual Web Server

Dịch vụ **Amazon EC2 (Elastic Compute Cloud)** cho phép thuê các máy chủ ảo trên đám mây. Thay vì phải mua máy tính vật lý, tôi có thể khởi tạo một máy chủ Linux chỉ trong vài phút.

### Kiến thức cốt lõi:
* **AMI (Amazon Linux 2023):** Hệ điều hành tối ưu cho AWS.
* **Instance Type (t2.micro):** Cấu hình phần cứng thuộc gói miễn phí.
* **Security Group:** Tường lửa kiểm soát cổng 22 (quản lý) và cổng 80 (truy cập web).
* **User Data:** Đoạn script tự động cài đặt Apache Web Server khi máy vừa bật.

### Quá trình thực hiện:

#### Bước 1: Thiết lập tên và hệ điều hành
Tôi đặt tên cho máy chủ là `MyWebServer` và chọn Amazon Linux 2023.
![Bước 1](/my-hugo-site/images/week3/anh1.png)

#### Bước 2: Chọn cấu hình miễn phí và tạo khóa bảo mật
Sử dụng `t2.micro` để tối ưu chi phí và tạo file `my-key.pem` để đăng nhập an toàn.
![Bước 2](/my-hugo-site/images/week3/anh2.png)

#### Bước 3: Cấu hình mạng (VPC & Subnet)
Máy chủ được đặt vào `MyLabVPC` đã tạo từ trước, chọn Public Subnet và bật Public IP. Đồng thời cấu hình Security Group mở cổng 80.
![Bước 3](/my-hugo-site/images/week3/anh3.png)

#### Bước 4: Nhập Script tự động (User Data)
Dán đoạn mã script để máy chủ tự động cài đặt môi trường web khi khởi chạy.
![Bước 4](/my-hugo-site/images/week3/anh4.png)

#### Bước 5: Kiểm tra trạng thái máy chủ
Hệ thống xác nhận máy chủ đã sẵn sàng (Running) và vượt qua bài kiểm tra sức khỏe.
![Bước 5](/my-hugo-site/images/week3/anh5.png)

#### Bước 6: Truy cập thực tế qua IP Public
Sử dụng địa chỉ IP Public của máy chủ để truy cập trực tiếp từ trình duyệt cá nhân.
![Bước 6](/my-hugo-site/images/week3/anh6.png)

---
*Các nội dung tiếp theo về Lab 5 (S3) và Lab 6 (RDS) sẽ được cập nhật trong các buổi thực hành tới.*