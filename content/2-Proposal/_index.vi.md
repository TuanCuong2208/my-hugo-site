---
title: "Bản đề xuất"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 2. </b> "
---


# Giới thiệu

Trong bối cảnh nhu cầu học trực tuyến, đào tạo nội bộ và chia sẻ nội dung số ngày càng phát triển, các hệ thống phát video theo yêu cầu (Video-on-Demand - VoD) đóng vai trò quan trọng trong việc cung cấp nội dung đến người dùng một cách nhanh chóng và ổn định. Tuy nhiên, việc xây dựng một hệ thống VoD theo mô hình truyền thống thường yêu cầu máy chủ có cấu hình cao để xử lý video, lưu trữ dữ liệu và phục vụ nhiều người dùng đồng thời. Điều này làm tăng chi phí đầu tư cũng như chi phí vận hành.

Để giải quyết vấn đề trên, nhóm đề xuất xây dựng **Serverless Video-on-Demand Platform on AWS**, một nền tảng phát video theo yêu cầu sử dụng kiến trúc Serverless kết hợp các dịch vụ của Amazon Web Services. Hệ thống tập trung vào việc tự động hóa quy trình tải lên, xử lý, lưu trữ và phát video thông qua các dịch vụ được quản lý hoàn toàn bởi AWS.

Giải pháp hướng tới mục tiêu giảm thiểu việc quản lý hạ tầng, tối ưu chi phí sử dụng tài nguyên, đồng thời đảm bảo khả năng mở rộng và tính sẵn sàng của hệ thống khi số lượng video hoặc người dùng tăng lên.

---

# Vấn đề và giải pháp

## Bài toán đặt ra

Trong nhiều hệ thống hiện nay, quá trình xử lý video thường được thực hiện trực tiếp trên máy chủ ứng dụng. Khi số lượng video tăng lên, máy chủ phải đồng thời xử lý việc tải tệp, chuyển đổi định dạng, lưu trữ và cung cấp nội dung cho người dùng. Điều này làm tiêu tốn nhiều tài nguyên tính toán, gây ảnh hưởng đến hiệu năng của toàn bộ hệ thống và làm tăng chi phí vận hành.

Bên cạnh đó, việc mở rộng hệ thống theo mô hình truyền thống thường yêu cầu bổ sung máy chủ mới hoặc nâng cấp phần cứng, dẫn đến thời gian triển khai dài và chi phí đầu tư lớn.

## Giải pháp đề xuất

Nhóm đề xuất xây dựng nền tảng Video-on-Demand theo mô hình Serverless trên AWS. Video sau khi được tải lên sẽ được lưu trữ trên Amazon S3, sau đó kích hoạt quy trình xử lý tự động thông qua EventBridge, Amazon SQS và AWS Step Functions. AWS Elemental MediaConvert chịu trách nhiệm chuyển đổi video sang định dạng phù hợp để phát trực tuyến, trong khi Amazon CloudFront phân phối nội dung đến người dùng với độ trễ thấp.

Toàn bộ Backend được triển khai bằng Amazon API Gateway và AWS Lambda, kết hợp Amazon DynamoDB để lưu trữ metadata của video. Người dùng được xác thực thông qua Amazon Cognito trước khi sử dụng hệ thống.

Nhờ sử dụng kiến trúc hướng sự kiện (Event-Driven Architecture), hệ thống chỉ sử dụng tài nguyên khi phát sinh yêu cầu, từ đó tối ưu chi phí và tăng khả năng mở rộng.

---

# Kiến trúc đề xuất

Kiến trúc của hệ thống được xây dựng dựa trên các dịch vụ Serverless của Amazon Web Services. Mỗi thành phần đảm nhận một chức năng riêng biệt và giao tiếp với nhau thông qua API hoặc các sự kiện phát sinh trong hệ thống.

<img src="/images/2-Proposal/1.png" alt="Initial Serverless Video-on-Demand Architecture" style="max-width:100%; height:auto;" />

Quy trình hoạt động của hệ thống được mô tả như sau:

1. Người dùng đăng nhập thông qua Amazon Cognito.
2. Frontend gửi yêu cầu đến Amazon API Gateway.
3. AWS Lambda xử lý yêu cầu và tạo Pre-signed URL.
4. Video được tải trực tiếp lên Amazon S3 Raw Upload Bucket.
5. Amazon EventBridge phát hiện sự kiện tải lên và gửi thông tin vào Amazon SQS.
6. EventBridge Pipes kích hoạt AWS Step Functions.
7. AWS Step Functions điều phối AWS Elemental MediaConvert xử lý video.
8. Video sau khi xử lý được lưu vào Amazon S3 Processed Media Bucket.
9. Amazon DynamoDB cập nhật trạng thái xử lý của video.
10. Người dùng truy cập video thông qua Amazon CloudFront.

Các dịch vụ chính được sử dụng trong hệ thống gồm Amazon Cognito, Amazon API Gateway, AWS Lambda, Amazon DynamoDB, Amazon S3, Amazon EventBridge, Amazon SQS, EventBridge Pipes, AWS Step Functions, AWS Elemental MediaConvert, Amazon CloudFront và Amazon CloudWatch.

---

# Kế hoạch triển khai

Dự án được triển khai theo từng giai đoạn nhằm đảm bảo tiến độ phát triển, kiểm thử và triển khai hệ thống. Mỗi giai đoạn tập trung vào một nhóm chức năng cụ thể, giúp việc quản lý và đánh giá tiến độ trở nên thuận tiện hơn.

| Giai đoạn | Nội dung |
|------------|----------|
| Giai đoạn 1 | Khảo sát yêu cầu, nghiên cứu các dịch vụ AWS phù hợp |
| Giai đoạn 2 | Thiết kế kiến trúc hệ thống và cơ sở dữ liệu |
| Giai đoạn 3 | Xây dựng giao diện người dùng và Backend API |
| Giai đoạn 4 | Triển khai quy trình Upload Video và xử lý MediaConvert |
| Giai đoạn 5 | Tích hợp CloudFront, kiểm thử và triển khai Demo |

Trong quá trình thực hiện, hệ thống sẽ được kiểm thử sau mỗi giai đoạn nhằm phát hiện và xử lý sớm các lỗi phát sinh. Sau khi hoàn thành toàn bộ chức năng, nhóm tiến hành triển khai trên môi trường AWS để đánh giá hiệu năng và chuẩn bị cho buổi trình diễn sản phẩm.

---

# Chi phí dự kiến

Do hệ thống được xây dựng theo mô hình Serverless nên hầu hết các dịch vụ AWS đều áp dụng cơ chế **Pay-as-you-go**, chỉ tính phí khi có tài nguyên được sử dụng. Với phạm vi của đồ án, số lượng người dùng và video ở mức nhỏ nên tổng chi phí triển khai không đáng kể.

| Dịch vụ AWS | Mục đích sử dụng |
|--------------|------------------|
| Amazon S3 | Lưu trữ video |
| Amazon CloudFront | Phân phối nội dung |
| Amazon API Gateway | Cung cấp REST API |
| AWS Lambda | Xử lý nghiệp vụ |
| Amazon DynamoDB | Lưu metadata video |
| Amazon Cognito | Xác thực người dùng |
| Amazon EventBridge | Xử lý sự kiện |
| Amazon SQS | Hàng đợi xử lý |
| AWS Step Functions | Điều phối quy trình |
| AWS Elemental MediaConvert | Chuyển đổi video |
| Amazon CloudWatch | Giám sát hệ thống |

Với quy mô thử nghiệm khoảng 10–20 video và số lượng người dùng giới hạn, tổng chi phí triển khai được ước tính chỉ ở mức **5–10 USD**. Sau khi hoàn thành quá trình nghiệm thu và trình diễn, toàn bộ tài nguyên AWS sẽ được xóa để tránh phát sinh thêm chi phí.

---

# Kết quả mong đợi

Sau khi hoàn thành, hệ thống dự kiến đạt được các kết quả sau:

- Xây dựng thành công nền tảng phát video theo yêu cầu dựa trên kiến trúc Serverless.
- Tự động hóa quy trình tải lên, xử lý và phát video.
- Hỗ trợ chuyển đổi video sang định dạng HLS phục vụ phát trực tuyến.
- Phân phối video thông qua Amazon CloudFront nhằm nâng cao hiệu năng truy cập.
- Quản lý thông tin và trạng thái video bằng Amazon DynamoDB.
- Đảm bảo khả năng mở rộng, tính sẵn sàng và tối ưu chi phí nhờ sử dụng các dịch vụ được quản lý hoàn toàn bởi AWS.

Ngoài việc đáp ứng các chức năng cơ bản của một hệ thống Video-on-Demand, dự án còn giúp nhóm làm quen với mô hình kiến trúc Serverless, quy trình xử lý bất đồng bộ và cách tích hợp nhiều dịch vụ AWS trong cùng một giải pháp. Đây cũng là nền tảng để mở rộng thêm các tính năng như quản lý người dùng, thống kê lượt xem, tìm kiếm video hoặc tích hợp các dịch vụ AI của AWS trong tương lai.

---

# Kết luận

Serverless Video-on-Demand Platform on AWS là giải pháp tận dụng các dịch vụ Serverless của Amazon Web Services để xây dựng một hệ thống xử lý và phát video theo yêu cầu với chi phí hợp lý, khả năng mở rộng cao và giảm thiểu công tác quản trị hạ tầng.

Thông qua việc kết hợp Amazon S3, AWS Lambda, Amazon API Gateway, Amazon DynamoDB, AWS Elemental MediaConvert, Amazon CloudFront cùng các dịch vụ Event-Driven như Amazon EventBridge, Amazon SQS và AWS Step Functions, hệ thống có thể tự động hóa toàn bộ quy trình xử lý video từ khi tải lên đến khi sẵn sàng phục vụ người dùng.

Đề xuất này là cơ sở để nhóm triển khai, kiểm thử và hoàn thiện hệ thống trong các giai đoạn tiếp theo của đồ án.