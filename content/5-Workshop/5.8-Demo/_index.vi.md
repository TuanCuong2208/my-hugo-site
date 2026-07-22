---
title: "Demo hệ thống"
date: 2026-07-20
weight: 8
chapter: false
pre: "<b>5.8. </b>"
---

# Demo hệ thống

## Tổng quan

Sau khi hoàn thành quá trình triển khai và kiểm thử, hệ thống **Serverless Video-on-Demand Platform on AWS** đã đáp ứng đầy đủ các chức năng của phiên bản MVP. Video dưới đây minh họa toàn bộ quy trình hoạt động của hệ thống, từ khi người dùng tải video lên cho đến khi video được xử lý trên nền tảng AWS và sẵn sàng phát trên ứng dụng.

## Nội dung Demo

Video minh họa các chức năng chính của hệ thống theo đúng quy trình xử lý thực tế:

- Đăng nhập vào hệ thống.
- Upload video thông qua Web Application.
- Lưu video gốc vào Amazon S3 Raw Upload Bucket.
- Xử lý video bằng AWS Elemental MediaConvert.
- Lưu video sau xử lý vào Amazon S3 Processed Media Bucket.
- Cập nhật metadata trong Amazon DynamoDB.
- Phát video trực tiếp trên Website sau khi quá trình xử lý hoàn tất.

## Video Demo

<video width="100%" controls preload="metadata">
    <source src="/images/5-Workshop/Demo.mp4" type="video/mp4">
</video>

<p align="center">
<i><b>Video 5.1.</b> Minh họa quá trình hoạt động của Serverless Video-on-Demand Platform on AWS.</i>
</p>

## Kết quả

Video Demo xác nhận hệ thống hoạt động đúng theo kiến trúc Serverless đã thiết kế. Sau khi người dùng tải video lên, hệ thống tự động thực hiện toàn bộ quy trình xử lý, lưu trữ, cập nhật metadata và cung cấp video sẵn sàng để phát trên giao diện Web Application mà không cần bất kỳ thao tác xử lý thủ công nào.