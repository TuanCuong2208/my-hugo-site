---
title: "Các Bài Nghiên Cứu Của Nhóm"
date: 2026-06-30
weight: 3
chapter: true
pre: "<b>3.</b>"
---

<style>
.publication-page{
    text-align:left !important;
    width:100%;
}

.publication-page h1,
.publication-page h2,
.publication-page h3,
.publication-page h4,
.publication-page p,
.publication-page div,
.publication-page ul,
.publication-page ol,
.publication-page li{
    text-align:left !important;
}

.publication-page hr{
    margin:25px 0;
}
</style>

<div class="publication-page">


<h1 style="text-align:center !important;">Các Bài Nghiên Cứu Của Nhóm</h1>

Trong thời gian thực tập, tôi thường xuyên nghiên cứu các bài viết kỹ thuật được xuất bản bởi AWS và các nhóm kỹ thuật khác. Bên cạnh việc hoàn thành các bài lab của AWS Academy, tôi đã tóm tắt nhiều bài viết để hiểu rõ hơn về kiến trúc cloud-native, hệ thống phân tán, và các thực tiễn kỹ thuật tốt nhất.

Trang này tổng hợp các ghi chú nghiên cứu và bản tóm tắt bài viết mà tôi đã hoàn thành trong suốt kỳ thực tập.

## Danh Sách Các Bài Nghiên Cứu Chuyên Sâu

### Bài viết 1 - Mở Rộng 1 Triệu AWS Lambda Functions: Bài Học "Xương Máu" Về Kiến Trúc Serverless Quy Mô Lớn
[Xem chi tiết tại đây](./3.1-Blog1/)

**Tóm tắt nội dung:** Bài viết tập trung vào việc mở rộng hiệu năng và quản lý xử lý bất đồng bộ ở quy mô hàng triệu functions chạy đồng thời. Qua việc phân tích giới hạn dịch vụ (AWS Service Quotas), nhóm nghiên cứu làm rõ cách loại bỏ các anti-pattern truyền thống, chống nghẽn cổ chai và xây dựng hệ thống chịu lỗi chủ động (Fail-safe architecture).  
**Kiến trúc áp dụng:** Kiến trúc hướng sự kiện (Event-Driven Architecture) & Điều phối quy trình (Orchestration).  
**Dịch vụ AWS cốt lõi:** AWS Lambda | Amazon SQS | AWS Step Functions | AWS SAM | AWS CloudFormation

---

### Bài viết 2 - Từ Monolith đến Multi-Account: Hành Trình Tái Cấu Trúc Toàn Diện AWS Organizations Ở Quy Mô Lớn Của Pinterest
[Xem chi tiết tại đây](./3.2-Blog2/)

**Tóm tắt nội dung:** Bài viết phân tích những thách thức như giới hạn API, thu hẹp blast radius, và tăng cường độ an toàn hệ thống. Nhóm nghiên cứu giải thích cách thiết kế Organizational Units (OU), áp dụng chính sách kiểm soát tập trung để tối ưu chi phí, và quản trị định danh ở quy mô lớn.  
**Kiến trúc áp dụng:** Chiến lược đa tài khoản (Multi-Account Strategy) & Quản trị tập trung (Centralized Governance).  
**Dịch vụ AWS cốt lõi:** AWS Organizations | AWS Control Tower | IAM Identity Center | AWS Config | Amazon CloudTrail

---

### Bài viết 3 - Xây Dựng Dịch Vụ Authentication Và Session Management Với Amazon Aurora DSQL
[Xem chi tiết tại đây](./3.3-Blog3/)

**Tóm tắt nội dung:** Bài viết giới thiệu cách xây dựng dịch vụ Authentication và Session Management hiện đại bằng Amazon Aurora DSQL, Amazon ECS Express Mode, AWS Fargate và IAM Authentication. Nó nhấn mạnh tính nhất quán mạnh sau khi ghi (Strong Read-after-Write Consistency), bảo vệ session token, quản lý credential an toàn, và thiết kế backend có khả năng mở rộng bằng các dịch vụ managed/serverless.  
**Kiến trúc áp dụng:** Kiến trúc Backend Serverless & Dịch vụ Authentication.  
**Dịch vụ AWS cốt lõi:** Amazon Aurora DSQL | Amazon ECS Express Mode | AWS Fargate | AWS IAM | Amazon CloudWatch

</div>
