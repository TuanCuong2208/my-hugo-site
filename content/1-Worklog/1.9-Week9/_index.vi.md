---
title: "Worklog Tuần 9"
date: 2026-06-16
weight: 9
chapter: false
pre: "<b>1.9. </b>"
---

## I. Tóm tắt tổng quan

Tuần thứ chín đánh dấu giai đoạn hoàn thiện Backend của hệ thống **Serverless Video-on-Demand Platform on AWS**. Trong tuần này, nhóm tập trung triển khai các dịch vụ cốt lõi bao gồm Amazon S3, Amazon DynamoDB, AWS Lambda và Amazon API Gateway nhằm xây dựng nền tảng phục vụ quá trình tải video.

Bên cạnh việc xây dựng hạ tầng, nhóm cũng hoàn thiện các API Backend để tạo Presigned URL, lưu metadata video và truy vấn dữ liệu phục vụ ứng dụng web. Sau khi hoàn thành các thành phần trên, toàn bộ quy trình tải video trực tiếp lên Amazon S3 đã được kiểm thử thành công và sẵn sàng cho việc triển khai Video Processing Pipeline ở tuần tiếp theo.

---

## II. Mục tiêu chiến lược trong tuần

Trong tuần này, nhóm đặt ra các mục tiêu sau:

- Triển khai hạ tầng Backend theo kiến trúc Serverless.
- Khởi tạo Amazon S3 Raw Upload Bucket và Processed Media Bucket.
- Thiết kế bảng Amazon DynamoDB quản lý metadata video.
- Xây dựng AWS Lambda xử lý các nghiệp vụ Backend.
- Tích hợp Amazon API Gateway với AWS Lambda.
- Tạo Presigned URL phục vụ Upload Video.
- Kiểm thử quy trình Upload và lưu metadata.
- Hoàn thiện Backend trước khi xây dựng Pipeline xử lý video.

---

## III. Nhật ký hoạt động & Lộ trình phân bổ chi tiết (Từ 16/06/2026 đến 22/06/2026)

| Thời gian | Danh mục hoạt động | Nội dung thực hiện | Kết quả |
|------------|--------------------|--------------------|----------|
| **Ngày 1 (16/06)** | Thiết kế Backend | Phân tích yêu cầu hệ thống, xây dựng kiến trúc Backend và xác định các API cần triển khai cho chức năng Upload Video, quản lý metadata và truy vấn danh sách video. Đồng thời xác định luồng giao tiếp giữa Web Application và các dịch vụ AWS. | Hoàn thành thiết kế Backend và danh sách API phục vụ hệ thống. |
| **Ngày 2 (17/06)** | Triển khai AWS Lambda | Xây dựng các AWS Lambda Functions đảm nhiệm việc tạo Presigned URL, lưu metadata vào Amazon DynamoDB và xử lý các yêu cầu từ Amazon API Gateway. Cấu hình Environment Variables và kiểm tra quá trình thực thi của từng Lambda Function. | AWS Lambda hoạt động ổn định và xử lý đúng các nghiệp vụ Backend. |
| **Ngày 3 (18/06)** | Triển khai Amazon DynamoDB | Tạo bảng Videos với Partition Key là `videoId`. Hoàn thiện cấu trúc metadata bao gồm tên video, trạng thái xử lý, thời gian tải lên và đường dẫn lưu trữ. Kết nối AWS Lambda với Amazon DynamoDB để thực hiện thao tác ghi và truy vấn dữ liệu. | Metadata video được lưu và truy xuất thành công. |
| **Ngày 4 (19/06)** | Hoàn thiện quy trình Upload | Xây dựng API tạo Presigned URL và kiểm thử quá trình tải video trực tiếp lên Amazon S3 Raw Upload Bucket. Kiểm tra việc cập nhật metadata sau khi Upload hoàn tất và đánh giá hiệu năng của quy trình tải lên. | Video được Upload thành công lên Amazon S3 và metadata được cập nhật chính xác. |
| **Ngày 5 (20/06)** | Kiểm thử API | Thực hiện kiểm thử các API của hệ thống bao gồm tạo Presigned URL, lưu metadata và truy vấn danh sách video. Kiểm tra các trường hợp hợp lệ và không hợp lệ để đánh giá tính ổn định của Backend. | Các API trả về dữ liệu chính xác và hoạt động ổn định. |
| **Ngày 6 (21/06)** | Kiểm tra bảo mật | Rà soát IAM Role, IAM Policy, cấu hình CORS và quyền truy cập giữa Amazon API Gateway, AWS Lambda, Amazon DynamoDB và Amazon S3. Điều chỉnh quyền tối thiểu cần thiết để đảm bảo an toàn cho hệ thống. | Hoàn thiện cấu hình bảo mật và loại bỏ các lỗi phân quyền. |
| **Ngày 7 (22/06)** | Đánh giá và tổng kết | Kiểm tra lại toàn bộ Backend, rà soát mã nguồn, đánh giá kết quả triển khai và chuẩn bị môi trường cho việc xây dựng Video Processing Pipeline trong tuần tiếp theo. | Backend được triển khai hoàn chỉnh và sẵn sàng tích hợp với Pipeline xử lý video. |

---

## IV. Thực thi kỹ thuật chuyên sâu & Phân tích chi tiết

Trong tuần này, nhóm ưu tiên triển khai Backend theo kiến trúc Serverless nhằm tận dụng khả năng tự động mở rộng và giảm chi phí vận hành của AWS. Amazon API Gateway được sử dụng làm cổng tiếp nhận các yêu cầu từ ứng dụng web và chuyển tiếp đến AWS Lambda để xử lý nghiệp vụ.

AWS Lambda đảm nhận việc tạo Presigned URL, lưu metadata vào Amazon DynamoDB và trả kết quả về cho ứng dụng. Việc sử dụng Presigned URL giúp dữ liệu video được tải trực tiếp lên Amazon S3 mà không phải đi qua Backend, từ đó giảm tải cho Lambda và tối ưu hiệu năng hệ thống.

Amazon DynamoDB được lựa chọn để lưu trữ metadata do có khả năng truy xuất nhanh và tích hợp tốt với kiến trúc serverless. Sau khi video được tải lên, thông tin của video được lưu vào bảng Videos để phục vụ các bước xử lý tiếp theo.

Thông qua quá trình kiểm thử, nhóm xác nhận Backend hoạt động ổn định, các API phản hồi đúng dữ liệu và quy trình Upload Video diễn ra thành công.

---

## V. Thách thức hạ tầng, Nhật ký xử lý lỗi & Góc nhìn chuyên gia

Khó khăn lớn nhất trong tuần là cấu hình quyền truy cập giữa các dịch vụ AWS. Ban đầu, AWS Lambda chưa có đầy đủ quyền để tạo Presigned URL và truy cập Amazon S3, dẫn đến việc API trả về lỗi trong quá trình kiểm thử.

Ngoài ra, nhóm cũng gặp một số lỗi liên quan đến CORS khi ứng dụng web gửi yêu cầu đến Amazon API Gateway. Sau khi rà soát cấu hình API Gateway và IAM Policy, các lỗi được khắc phục và Backend hoạt động ổn định.

Qua quá trình triển khai, nhóm nhận thấy việc thiết kế quyền truy cập ngay từ đầu giúp giảm đáng kể thời gian xử lý lỗi và tăng tính bảo mật cho toàn bộ hệ thống.

---

## VI. Đánh giá và Chiêm nghiệm chuyên môn

Các mục tiêu đặt ra trong tuần đều được hoàn thành đúng tiến độ. Backend đã sẵn sàng phục vụ ứng dụng web với các chức năng tạo Presigned URL, lưu metadata và quản lý thông tin video.

Quá trình triển khai giúp nhóm hiểu rõ hơn cách kết hợp Amazon API Gateway, AWS Lambda, Amazon DynamoDB và Amazon S3 trong một kiến trúc Serverless. Đồng thời, nhóm cũng tích lũy thêm kinh nghiệm về quản lý IAM Role, IAM Policy và tối ưu quy trình Upload Video trên AWS.

Đây là nền tảng quan trọng để triển khai Video Processing Pipeline trong giai đoạn tiếp theo.

---

## VII. Kế hoạch chiến lược & Lộ trình tối ưu cho tuần tới

Trong tuần thứ mười, nhóm sẽ tập trung xây dựng **Video Processing Pipeline** theo kiến trúc hướng sự kiện.

Các công việc chính bao gồm:

- Triển khai Amazon SQS và Dead Letter Queue.
- Cấu hình Amazon EventBridge để nhận sự kiện từ Amazon S3.
- Thiết lập EventBridge Pipes kết nối Amazon SQS với AWS Step Functions.
- Xây dựng State Machine trên AWS Step Functions.
- Tích hợp AWS Elemental MediaConvert để chuyển mã video.
- Kiểm thử toàn bộ quy trình xử lý video tự động sau khi Upload.
- Chuẩn bị dữ liệu phục vụ chức năng phát video trên ứng dụng web.