---
title: "Demo hệ thống"
date: 2026-07-20
weight: 8
chapter: false
pre: "<b>5.8. </b>"
---


## Tổng quan

Sau khi hoàn thành quá trình triển khai và kiểm thử, hệ thống **Serverless Video-on-Demand Platform on AWS** đã đáp ứng đầy đủ các chức năng của phiên bản MVP. Video dưới đây minh họa toàn bộ quy trình hoạt động của hệ thống, từ khi người dùng tải video lên, xử lý trên nền tảng AWS cho đến khi video sẵn sàng để phát trên Website.

## Nội dung Demo

Video trình bày đầy đủ quy trình hoạt động của hệ thống theo đúng kiến trúc đã triển khai, bao gồm:

- Đăng nhập vào hệ thống.
- Upload video thông qua Web Application.
- Kiểm tra video trong Amazon S3 Raw Upload Bucket.
- Theo dõi quá trình xử lý bằng AWS Elemental MediaConvert.
- Kiểm tra video đầu ra trong Amazon S3 Processed Media Bucket.
- Xác nhận metadata được cập nhật trong Amazon DynamoDB.
- Phát video trực tiếp trên Website sau khi quá trình xử lý hoàn tất.

## Video Demo

👉 **Tài liệu đính kèm (Video Demo & Source Code):**

**https://drive.google.com/drive/folders/1xOeoWnbue5yN53ZRrLSrN_00S22ct_Rw**

Thư mục Google Drive bao gồm:

- 📄 Source code của Website Workshop.
- 📄 Source code của đồ án **Serverless Video-on-Demand Platform on AWS**.
- 🎥 Video minh họa toàn bộ quá trình triển khai và vận hành của hệ thống.

## Kết quả

Video Demo xác nhận hệ thống hoạt động đúng theo kiến trúc Serverless đã thiết kế. Sau khi người dùng tải video lên, hệ thống tự động thực hiện quá trình xử lý, lưu trữ video đầu ra, cập nhật metadata và cung cấp video sẵn sàng để phát trên Website. Kết quả này cho thấy các thành phần của hệ thống đã được tích hợp thành công và hoạt động xuyên suốt theo quy trình đã đề xuất.