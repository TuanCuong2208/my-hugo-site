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

## 5. Lab 5: Amazon S3 - Static Website Hosting

**Amazon S3 (Simple Storage Service)** là dịch vụ lưu trữ đối tượng dẫn đầu về khả năng mở rộng và độ sẵn sàng của dữ liệu. Bài lab này tập trung vào việc biến một S3 Bucket thành một trang web tĩnh (Static Website).

### Khái niệm cốt lõi:
* **S3 Bucket:** Thùng chứa đối tượng độc nhất trên toàn cầu.
* **Static Website Hosting:** Tính năng cho phép phục vụ các tệp HTML, CSS, JS trực tiếp từ S3.
* **Bucket Policy:** Cấu hình JSON để phân quyền truy cập (cho phép đọc công khai).

### Quá trình thực hiện:

#### Bước 1: Khởi tạo và Mở quyền Public
Tôi tạo bucket `cuong-static-website-2026` và bỏ tích chọn "Block all public access" để chuẩn bị cho việc public website.
![Step 7](/my-hugo-site/images/week3/anh7.png)

#### Bước 2: Kích hoạt Website Hosting
Trong tab Properties, tôi bật tính năng Static website hosting và thiết lập tệp mặc định là `index.html`.
![Step 8](/my-hugo-site/images/week3/anh8.png)

#### Bước 3: Cấu hình chính sách bảo mật (Bucket Policy)
Dán đoạn mã JSON để cấp quyền `s3:GetObject` cho mọi người dùng internet.
![Step 9](/my-hugo-site/images/week3/anh9.png)

#### Bước 4: Kiểm tra kết quả
Tải tệp `index.html` lên và truy cập thông qua Endpoint được AWS cấp.
![Step 10](/my-hugo-site/images/week3/anh10.png)
![Step 11](/my-hugo-site/images/week3/anh11.png)

---

## 6. Lab 6: Amazon RDS - Relational Database Service

**Amazon RDS** giúp đơn giản hóa việc thiết lập và vận hành các cơ sở dữ liệu quan hệ trên đám mây. Tôi đã triển khai một thực thể MySQL để phục vụ lưu trữ dữ liệu cho ứng dụng.

### Khái niệm cốt lõi:
* **DB Engine:** Hệ quản trị CSDL được chọn (MySQL).
* **Sandbox (Free Tier):** Gói cấu hình miễn phí dành cho việc học tập và thử nghiệm.
* **Endpoint:** Địa chỉ máy chủ CSDL dùng để kết nối từ các ứng dụng Backend.

### Quá trình thực hiện:

#### Bước 1: Lựa chọn Engine và Gói Sandbox
Tôi chọn MySQL và Template **Sandbox** để đảm bảo hệ thống nằm trong gói Free Tier của AWS.
![Step 12](/my-hugo-site/images/week3/anh12.png)

#### Bước 2: Khởi tạo thực thể DB
Thiết lập VPC và quyền truy cập công khai (Public Access), sau đó tiến hành khởi tạo máy chủ CSDL.
![Step 13](/my-hugo-site/images/week3/anh13.png)

#### Bước 3: Xác nhận trạng thái và Endpoint
Sau khi DB ở trạng thái **Available**, tôi lấy thông tin Endpoint để sử dụng cho việc kết nối sau này.
![Step 14](/my-hugo-site/images/week3/anh14.png)