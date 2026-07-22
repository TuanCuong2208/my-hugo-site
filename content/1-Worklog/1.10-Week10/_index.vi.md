---
title: "Worklog Tuần 10"
date: 2026-06-23
weight: 10
chapter: false
pre: "<b>1.10. </b>"
---

## I. Tóm tắt tổng quan

Sau khi hoàn thiện Backend ở tuần trước, tuần thứ mười tập trung xây dựng **Video Processing Pipeline** theo kiến trúc hướng sự kiện (Event-driven Architecture). Mục tiêu của tuần là tự động hóa toàn bộ quy trình xử lý video sau khi người dùng tải tệp lên hệ thống mà không cần bất kỳ thao tác thủ công nào.

Nhóm triển khai lần lượt Amazon EventBridge, Amazon SQS, EventBridge Pipes, AWS Step Functions và AWS Elemental MediaConvert để tạo thành một Pipeline hoàn chỉnh. Mỗi dịch vụ đảm nhận một vai trò riêng và phối hợp với nhau thông qua các sự kiện phát sinh trong hệ thống.

Sau khi hoàn tất cấu hình, nhóm tiến hành kiểm thử bằng nhiều tệp video với kích thước khác nhau nhằm đánh giá tính ổn định của Pipeline. Kết quả cho thấy hệ thống có thể tự động tiếp nhận sự kiện Upload, kích hoạt Workflow xử lý video và tạo thành công các tệp HLS trong Amazon S3 Processed Media Bucket.

Tuần làm việc này đóng vai trò quan trọng vì đây là giai đoạn biến hệ thống từ một nền tảng chỉ lưu trữ video thành một nền tảng có khả năng xử lý và chuẩn bị nội dung phục vụ phát trực tuyến.

---

## II. Mục tiêu chiến lược trong tuần

Các mục tiêu được đặt ra trong tuần bao gồm:

- Triển khai kiến trúc xử lý video theo mô hình Event-driven.
- Tạo Dead Letter Queue phục vụ xử lý lỗi.
- Xây dựng Amazon SQS nhận sự kiện từ Amazon EventBridge.
- Kích hoạt EventBridge Notification cho Amazon S3.
- Cấu hình EventBridge Rule chuyển sự kiện sang Amazon SQS.
- Xây dựng AWS Step Functions điều phối Workflow.
- Tích hợp AWS Elemental MediaConvert.
- Thiết lập EventBridge Pipes.
- Kiểm thử Pipeline với nhiều video.
- Đánh giá hiệu năng và tính ổn định của quy trình xử lý.

---

## III. Nhật ký hoạt động & Lộ trình phân bổ chi tiết (Từ 23/06/2026 đến 29/06/2026)

| Thời gian | Danh mục hoạt động | Nội dung thực hiện | Kết quả |
|------------|--------------------|--------------------|----------|
| **Ngày 1 (23/06)** | Thiết kế Pipeline | Phân tích luồng xử lý video, xác định vai trò của Amazon EventBridge, Amazon SQS, EventBridge Pipes, AWS Step Functions và AWS Elemental MediaConvert trong toàn bộ hệ thống. | Hoàn thiện kiến trúc Video Processing Pipeline. |
| **Ngày 2 (24/06)** | Triển khai Amazon SQS | Tạo Processing Queue và Dead Letter Queue. Cấu hình Retry Policy và kiểm tra khả năng tiếp nhận thông điệp từ EventBridge. | Amazon SQS hoạt động ổn định. |
| **Ngày 3 (25/06)** | Cấu hình EventBridge | Bật EventBridge Notification trên Amazon S3 và tạo Rule chuyển sự kiện Object Created sang Amazon SQS. | Upload Video tạo ra Message trong Queue. |
| **Ngày 4 (26/06)** | Xây dựng Step Functions | Thiết kế State Machine và tích hợp AWS Elemental MediaConvert vào Workflow xử lý video. | Workflow được triển khai thành công. |
| **Ngày 5 (27/06)** | Cấu hình MediaConvert | Thiết lập Input, Output, Job Template và IAM Role cho AWS Elemental MediaConvert. | Job được tạo thành công sau khi Workflow thực thi. |
| **Ngày 6 (28/06)** | Tích hợp EventBridge Pipes | Kết nối Amazon SQS với AWS Step Functions để tự động kích hoạt Workflow khi Queue nhận được Message. | Pipeline hoạt động hoàn toàn tự động. |
| **Ngày 7 (29/06)** | Kiểm thử tổng thể | Upload nhiều video với dung lượng khác nhau, theo dõi Workflow, kiểm tra MediaConvert Job và xác nhận dữ liệu đầu ra trên Amazon S3. | Toàn bộ Pipeline hoạt động ổn định. |

---

## IV. Thực thi kỹ thuật chuyên sâu & Phân tích chi tiết

Điểm trọng tâm của tuần này là xây dựng một Pipeline xử lý video hoàn toàn tự động dựa trên kiến trúc hướng sự kiện. Thay vì để Backend trực tiếp xử lý toàn bộ quy trình chuyển mã, nhóm lựa chọn tách các thành phần thành nhiều dịch vụ độc lập nhằm tăng khả năng mở rộng và giảm mức độ phụ thuộc giữa các thành phần.

Ngay khi người dùng tải video lên Amazon S3 Raw Upload Bucket, Amazon EventBridge sẽ nhận sự kiện Object Created và phát sinh một Event tương ứng. Event này không được gửi trực tiếp đến Workflow mà được chuyển sang Amazon SQS nhằm tạo một lớp đệm giúp hệ thống xử lý tốt hơn trong trường hợp có nhiều video được tải lên cùng lúc.

Amazon SQS đóng vai trò lưu trữ tạm thời các thông điệp, hạn chế nguy cơ mất dữ liệu khi một dịch vụ phía sau gặp lỗi hoặc đang xử lý quá tải. Đồng thời, Dead Letter Queue được cấu hình để lưu lại các thông điệp xử lý thất bại sau nhiều lần Retry, giúp việc theo dõi và khắc phục lỗi trở nên dễ dàng hơn.

Sau khi Message xuất hiện trong Queue, EventBridge Pipes sẽ tự động đọc nội dung và truyền sang AWS Step Functions. Việc sử dụng EventBridge Pipes giúp giảm đáng kể khối lượng mã nguồn cần xây dựng vì không cần thêm AWS Lambda trung gian chỉ để chuyển tiếp dữ liệu.

AWS Step Functions được sử dụng để điều phối toàn bộ Workflow xử lý video. Trong State Machine, nhóm cấu hình bước gọi AWS Elemental MediaConvert để tạo Job chuyển mã. Cách tiếp cận này giúp Workflow dễ mở rộng trong tương lai nếu cần bổ sung thêm các bước như kiểm tra định dạng video, tạo thumbnail hoặc gửi thông báo đến người dùng.

AWS Elemental MediaConvert đảm nhận việc chuyển đổi video sang định dạng HLS. Đây là định dạng phù hợp cho việc phát trực tuyến vì có thể chia video thành nhiều Segment nhỏ, hỗ trợ Adaptive Streaming và tối ưu trải nghiệm xem trên nhiều thiết bị khác nhau.

Sau khi Job hoàn tất, các tệp đầu ra được lưu trong Amazon S3 Processed Media Bucket. Kết quả kiểm thử cho thấy toàn bộ quy trình được kích hoạt hoàn toàn tự động chỉ bằng thao tác Upload Video của người dùng.

Thông qua tuần làm việc này, nhóm đã xây dựng thành công nền tảng xử lý video có khả năng mở rộng, dễ bảo trì và phù hợp với định hướng Serverless trên AWS.

---

## V. Thách thức hạ tầng, Nhật ký xử lý lỗi & Góc nhìn chuyên gia

Trong quá trình triển khai Pipeline, nhóm gặp nhiều lỗi liên quan đến việc truyền sự kiện giữa các dịch vụ AWS.

Ban đầu, EventBridge Rule chưa nhận được sự kiện từ Amazon S3 do Bucket chưa bật EventBridge Notification. Sau khi kiểm tra lại phần Properties của Bucket và kích hoạt tính năng này, sự kiện bắt đầu được gửi đúng đến EventBridge.

Tiếp theo, AWS Step Functions chưa thể tạo MediaConvert Job vì IAM Role chưa được cấp quyền đầy đủ. Nhóm tiến hành bổ sung quyền cần thiết cho MediaConvert và cập nhật Trust Policy để dịch vụ có thể hoạt động bình thường.

Ngoài ra, một số Message trong Amazon SQS chưa được xử lý do cấu hình EventBridge Pipes chưa đúng Source Mapping. Sau khi điều chỉnh lại cấu hình và kiểm thử nhiều lần, toàn bộ Pipeline đã hoạt động ổn định.

Qua quá trình xử lý lỗi, nhóm nhận thấy việc chia nhỏ Pipeline thành nhiều dịch vụ giúp việc xác định vị trí lỗi nhanh hơn và giảm ảnh hưởng đến toàn bộ hệ thống.

---

## VI. Đánh giá và Chiêm nghiệm chuyên môn

Tuần làm việc này giúp nhóm hiểu rõ hơn cách các dịch vụ AWS phối hợp với nhau trong một kiến trúc hướng sự kiện.

Thay vì xây dựng một ứng dụng xử lý tập trung, từng dịch vụ chỉ đảm nhận một nhiệm vụ riêng, từ đó tăng khả năng mở rộng và giảm mức độ phụ thuộc giữa các thành phần.

Việc sử dụng Amazon SQS giúp Pipeline có khả năng xử lý bất đồng bộ, trong khi AWS Step Functions hỗ trợ xây dựng Workflow rõ ràng và dễ theo dõi. AWS Elemental MediaConvert đảm nhiệm phần chuyển mã video với hiệu năng cao mà không cần tự quản lý hạ tầng.

Những kiến thức thu được trong tuần này là nền tảng quan trọng để phát triển các hệ thống xử lý dữ liệu quy mô lớn trên nền tảng AWS.

---

## VII. Kế hoạch chiến lược & Lộ trình tối ưu cho tuần tới

Trong tuần tiếp theo, nhóm sẽ tập trung phát triển ứng dụng Web và tích hợp toàn bộ Backend với Pipeline xử lý video.

Các công việc dự kiến bao gồm:

- Xây dựng giao diện đăng nhập.
- Hoàn thiện chức năng Upload Video.
- Hiển thị danh sách video từ Amazon DynamoDB.
- Phát video HLS thông qua Amazon CloudFront.
- Thiết kế Dashboard theo dõi trạng thái xử lý.
- Kiểm thử luồng hoạt động từ Upload đến Playback.
- Tối ưu giao diện và trải nghiệm người dùng.
- Chuẩn bị kiểm thử toàn bộ hệ thống trước khi hoàn thiện báo cáo.