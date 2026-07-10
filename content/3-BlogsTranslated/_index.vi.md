---
title: "AWS Study Group - Các Bài Nghiên Cứu Của Nhóm"
date: 2026-06-30
weight: 3
chapter: true
pre: " <b> 3. </b> "
---

Chào mừng bạn đến với trang tổng hợp các kết quả học tập và bài viết nghiên cứu chuyên sâu về dịch vụ điện toán đám mây AWS của nhóm chúng tôi. Tại đây, các thành viên core-team sẽ liên tục cập nhật những phân tích kiến trúc thực chiến, giải pháp tối ưu chi phí và các bài học kinh nghiệm "xương máu" trong quá trình triển khai hệ thống quy mô lớn.

---

## 📚 Danh Sách Các Bài Nghiên Cứu Chuyên Sâu

### [Blog 1 - Mở Rộng 1 Triệu AWS Lambda Functions: Bài Học "Xương Máu" Về Kiến Trúc Serverless Quy Mô Khủng](./blog-1/)

* **Tóm tắt nội dung:** Bài viết tập trung mổ xẻ bài toán tối ưu hóa hiệu năng và quản lý dòng chảy dữ liệu bất đồng bộ diện rộng khi hệ thống chạm ngưỡng hàng triệu functions chạy đồng thời. Qua việc phân tích sâu các giới hạn mặc định (AWS Service Quotas), nhóm nghiên cứu làm rõ giải pháp kết hợp bộ ba core services nhằm loại bỏ hoàn toàn các anti-pattern truyền thống, chống nghẽn cổ chai và xây dựng hệ thống chịu lỗi chủ động (Fail-safe architecture).
* **Kiến trúc áp dụng:** Kiến trúc hướng sự kiện (Event-Driven Architecture) & Điều phối quy trình (Orchestration).
* **AWS Services cốt lõi:** `AWS Lambda` | `Amazon SQS` | `AWS Step Functions` | `AWS SAM` | `AWS CloudFormation`

---

### [Blog 2 - Từ Monolith đến Multi-Account: Hành Trình Tái Cấu Trúc Toàn Diện AWS Organizations Ở Quy Mô Khủng Của Pinterest](./blog-2/)

* **Tóm tắt nội dung:** Bài viết đi sâu mổ xẻ những "nỗi đau" của kiến trúc tài khoản đơn khối và hành trình lột xác hạ tầng của Pinterest nhằm giải quyết bài toán giới hạn API Limits, thu hẹp Blast Radius và tăng cường tính an toàn hệ thống. Nhóm nghiên cứu làm rõ phương pháp thiết kế, phân rã các đơn vị tổ chức (OU), đồng thời áp dụng các chính sách kiểm soát tối cao để tối ưu hóa chi phí (Cost Optimization) và quản trị định danh diện rộng.
* **Kiến trúc áp dụng:** Quản trị đa tài khoản (Multi-Account Strategy) & Quản trị tập trung (Centralized Governance).
* **AWS Services cốt lõi:** `AWS Organizations` | `AWS Control Tower` | `AWS IAM Identity Center` | `AWS Config` | `Amazon CloudTrail`

---

### 🛡️ [Blog 3 - Xây Dựng Dịch Vụ Authentication Và Session Management Với Amazon Aurora DSQL](./blog-3/)

* **Tóm tắt nội dung:** Bài viết giới thiệu cách AWS xây dựng dịch vụ Authentication và Session Management hiện đại bằng Amazon Aurora DSQL, Amazon ECS Express Mode, AWS Fargate và IAM Authentication. Nội dung tập trung phân tích bài toán Strong Read-after-Write Consistency, bảo vệ Session Token, quản lý Credential an toàn và thiết kế backend có khả năng mở rộng bằng các dịch vụ managed/serverless.

* **Kiến trúc áp dụng:** Kiến trúc Backend Serverless (Serverless Backend Architecture) & Authentication Service.

* **AWS Services cốt lõi:** `Amazon Aurora DSQL` | `Amazon ECS Express Mode` | `AWS Fargate` | `AWS IAM` | `Amazon CloudWatch`