---
title: "Các Bài Nghiên Cứu Của Nhóm"
date: 2026-06-30
weight: 3
chapter: false
pre: "<b>3. </b>"
---

<style>
.publication-page {
    width: 100% !important;
    max-width: none !important;
    margin: 0 !important;
    padding: 0 !important;
    text-align: left !important;
}

.publication-page .publication-title {
    width: 100%;
    margin: 20px 0 32px;
    text-align: center !important;
}

.publication-page h2,
.publication-page h3,
.publication-page h4,
.publication-page p,
.publication-page ul,
.publication-page ol,
.publication-page li {
    margin-left: 0 !important;
    text-align: left !important;
}

.publication-page h2 {
    margin-top: 34px;
}

.publication-page h3 {
    margin-top: 28px;
    line-height: 1.35;
}

.publication-page p {
    line-height: 1.7;
}

.publication-page hr {
    width: 100%;
    margin: 28px 0;
}
</style>

<div class="publication-page">

Trong thời gian thực tập, tôi thường xuyên nghiên cứu các bài viết kỹ thuật được xuất bản bởi AWS và các nhóm kỹ thuật khác. Bên cạnh việc hoàn thành các bài thực hành trong chương trình AWS Academy, tôi đã tìm hiểu và tóm tắt nhiều bài viết nhằm mở rộng kiến thức về kiến trúc cloud-native, hệ thống phân tán và các phương pháp triển khai kỹ thuật hiệu quả.

Trang này tổng hợp các ghi chú nghiên cứu và nội dung tóm tắt của những bài viết chuyên sâu mà tôi đã hoàn thành trong suốt kỳ thực tập.

## Danh Sách Các Bài Nghiên Cứu Chuyên Sâu

### Bài viết 1 – Mở Rộng Một Triệu AWS Lambda Functions: Bài Học Về Kiến Trúc Serverless Quy Mô Lớn

[Xem chi tiết tại đây](3.1-Blog1/)

**Tóm tắt nội dung:** Bài viết tập trung phân tích khả năng mở rộng và quản lý xử lý bất đồng bộ trong hệ thống có quy mô lên đến hàng triệu AWS Lambda functions hoạt động đồng thời. Thông qua việc xem xét AWS Service Quotas và các giới hạn vận hành, nội dung nghiên cứu làm rõ cách loại bỏ các anti-pattern truyền thống, hạn chế hiện tượng nghẽn cổ chai và xây dựng hệ thống có khả năng chịu lỗi chủ động.

**Kiến trúc áp dụng:** Kiến trúc hướng sự kiện (Event-Driven Architecture) và điều phối quy trình (Orchestration).

**Dịch vụ AWS cốt lõi:** AWS Lambda, Amazon SQS, AWS Step Functions, AWS SAM và AWS CloudFormation.

---

### Bài viết 2 – Từ Monolith Đến Multi-Account: Quá Trình Tái Cấu Trúc AWS Organizations Ở Quy Mô Lớn Của Pinterest

[Xem chi tiết tại đây](3.2-Blog2/)

**Tóm tắt nội dung:** Bài viết phân tích các thách thức trong quá trình chuyển đổi từ kiến trúc tài khoản đơn sang mô hình đa tài khoản, bao gồm giới hạn API, phạm vi ảnh hưởng của sự cố và yêu cầu tăng cường an toàn hệ thống. Nội dung nghiên cứu trình bày cách tổ chức Organizational Units, áp dụng chính sách kiểm soát tập trung, quản trị định danh và tối ưu hoạt động trên quy mô lớn.

**Kiến trúc áp dụng:** Chiến lược đa tài khoản (Multi-Account Strategy) và quản trị tập trung (Centralized Governance).

**Dịch vụ AWS cốt lõi:** AWS Organizations, AWS Control Tower, IAM Identity Center, AWS Config và Amazon CloudTrail.

---

### Bài viết 3 – Xây Dựng Dịch Vụ Authentication Và Session Management Với Amazon Aurora DSQL

[Xem chi tiết tại đây](3.3-Blog3/)

**Tóm tắt nội dung:** Bài viết trình bày phương pháp xây dựng dịch vụ xác thực và quản lý phiên hiện đại bằng Amazon Aurora DSQL, Amazon ECS Express Mode, AWS Fargate và IAM Authentication. Nội dung nhấn mạnh tính nhất quán mạnh sau khi ghi, bảo vệ session token, quản lý thông tin xác thực an toàn và thiết kế backend có khả năng mở rộng bằng các dịch vụ được AWS quản lý.

**Kiến trúc áp dụng:** Kiến trúc backend serverless và dịch vụ xác thực.

**Dịch vụ AWS cốt lõi:** Amazon Aurora DSQL, Amazon ECS Express Mode, AWS Fargate, AWS IAM và Amazon CloudWatch.

</div>