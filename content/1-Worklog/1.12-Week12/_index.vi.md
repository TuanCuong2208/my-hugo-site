---
title: "Worklog Tuần 12"
date: 2026-07-07
weight: 12
chapter: false
pre: "<b>1.12. </b>"
---

## I. Tóm tắt tổng quan

Tuần thứ mười hai là tuần cuối cùng của quá trình thực tập, tập trung vào việc kiểm thử tổng thể hệ thống, tối ưu các thành phần đã triển khai và hoàn thiện tài liệu dự án. Sau khi Backend, Video Processing Pipeline và Web Application được tích hợp thành công, nhóm tiến hành đánh giá toàn bộ quy trình hoạt động của hệ thống theo nhiều kịch bản sử dụng khác nhau.

Trong tuần này, các chức năng chính như đăng nhập, tải video, xử lý video, cập nhật metadata và phát video trực tuyến đều được kiểm thử nhiều lần nhằm đảm bảo tính ổn định trước khi nghiệm thu. Đồng thời, nhóm cũng rà soát lại cấu hình của các dịch vụ AWS, tối ưu quyền truy cập và chuẩn hóa tài liệu triển khai.

Bên cạnh công việc kỹ thuật, nhóm tổng hợp kết quả đạt được trong suốt quá trình thực tập, hoàn thiện báo cáo và chuẩn bị nội dung trình bày cho buổi nghiệm thu dự án.

---

## II. Mục tiêu chiến lược trong tuần

Các mục tiêu chính của tuần bao gồm:

- Kiểm thử toàn bộ hệ thống.
- Đánh giá tính ổn định của Backend.
- Kiểm tra Video Processing Pipeline.
- Kiểm thử giao diện Web Application.
- Rà soát cấu hình các dịch vụ AWS.
- Tối ưu hiệu năng và bảo mật.
- Chuẩn hóa tài liệu kỹ thuật.
- Hoàn thiện báo cáo thực tập.
- Chuẩn bị nội dung nghiệm thu dự án.
- Đánh giá kết quả triển khai.

---

## III. Nhật ký hoạt động & Lộ trình phân bổ chi tiết (Từ 07/07/2026 đến 13/07/2026)

| Thời gian | Danh mục hoạt động | Nội dung thực hiện | Kết quả |
|------------|--------------------|--------------------|----------|
| **Ngày 1 (07/07)** | Kiểm thử Backend | Kiểm tra toàn bộ API, xác nhận các chức năng tạo Presigned URL, lưu metadata và truy vấn danh sách video hoạt động ổn định. | Backend đáp ứng đầy đủ các yêu cầu nghiệp vụ. |
| **Ngày 2 (08/07)** | Kiểm thử Pipeline | Upload nhiều video với dung lượng và định dạng khác nhau để đánh giá khả năng hoạt động của Video Processing Pipeline. | Pipeline xử lý thành công các video thử nghiệm. |
| **Ngày 3 (09/07)** | Kiểm thử Web Application | Thực hiện kiểm thử chức năng đăng nhập, Upload Video, hiển thị danh sách video và phát video trên nhiều trình duyệt. | Ứng dụng hoạt động ổn định và phản hồi chính xác. |
| **Ngày 4 (10/07)** | Tối ưu hệ thống | Rà soát IAM Role, IAM Policy, cấu hình CloudFront và MediaConvert. Kiểm tra lại toàn bộ tài nguyên AWS được sử dụng trong dự án. | Hệ thống được tối ưu và đảm bảo cấu hình nhất quán. |
| **Ngày 5 (11/07)** | Khắc phục lỗi | Xử lý các lỗi nhỏ phát sinh trong quá trình kiểm thử, chuẩn hóa dữ liệu metadata và tối ưu giao diện người dùng. | Các lỗi được khắc phục hoàn toàn. |
| **Ngày 6 (12/07)** | Hoàn thiện tài liệu | Tổng hợp hình ảnh, cập nhật Workshop, Worklog và các nội dung kỹ thuật trong báo cáo thực tập. | Tài liệu dự án được hoàn thiện. |
| **Ngày 7 (13/07)** | Tổng kết dự án | Đánh giá toàn bộ kết quả đạt được, chuẩn bị nội dung trình bày và kiểm tra lại hệ thống trước khi nghiệm thu. | Dự án sẵn sàng cho giai đoạn báo cáo và nghiệm thu. |

---

## IV. Thực thi kỹ thuật chuyên sâu & Phân tích chi tiết

Tuần cuối cùng không tập trung phát triển thêm chức năng mới mà ưu tiên đánh giá chất lượng của toàn bộ hệ thống sau quá trình triển khai. Nhóm xây dựng nhiều kịch bản kiểm thử nhằm mô phỏng các thao tác thực tế của người dùng để xác nhận tất cả thành phần đều hoạt động đúng theo thiết kế.

Quá trình kiểm thử bắt đầu từ chức năng đăng nhập, sau đó tiếp tục với quy trình tải video thông qua Presigned URL. Sau khi video được lưu vào Amazon S3 Raw Upload Bucket, nhóm theo dõi toàn bộ Pipeline xử lý bằng Amazon EventBridge, Amazon SQS, EventBridge Pipes, AWS Step Functions và AWS Elemental MediaConvert.

Trong mỗi lần kiểm thử, trạng thái xử lý được quan sát trên AWS Management Console để xác nhận từng dịch vụ đều thực hiện đúng vai trò của mình. Đồng thời, metadata trong Amazon DynamoDB cũng được kiểm tra nhằm đảm bảo dữ liệu được cập nhật đầy đủ sau khi MediaConvert hoàn thành.

Đối với giao diện Web Application, nhóm đánh giá khả năng hiển thị danh sách video, tốc độ phản hồi của các API và trải nghiệm phát video thông qua Amazon CloudFront. Các bài kiểm thử được thực hiện nhiều lần với các video có thời lượng và dung lượng khác nhau nhằm đánh giá tính ổn định của hệ thống.

Ngoài việc kiểm thử chức năng, nhóm còn rà soát toàn bộ cấu hình IAM Role và IAM Policy để đảm bảo các dịch vụ AWS chỉ được cấp quyền tối thiểu cần thiết. Điều này giúp tăng tính bảo mật và hạn chế các rủi ro trong quá trình vận hành.

Sau khi hoàn thành các bước kiểm thử, nhóm tiến hành chuẩn hóa tài liệu triển khai, bổ sung hình ảnh minh họa và cập nhật các kết quả thực nghiệm vào báo cáo thực tập.

Nhìn chung, hệ thống đáp ứng đầy đủ các mục tiêu đã đề ra và có thể vận hành ổn định theo đúng kiến trúc Serverless Video-on-Demand Platform.

---

## V. Thách thức hạ tầng, Nhật ký xử lý lỗi & Góc nhìn chuyên gia

Trong quá trình kiểm thử tổng thể, nhóm phát hiện một số lỗi nhỏ liên quan đến việc đồng bộ trạng thái giữa Pipeline xử lý video và giao diện Web. Một số trường hợp metadata chưa được cập nhật ngay sau khi MediaConvert hoàn thành khiến giao diện hiển thị chậm hơn so với thực tế.

Nhóm tiến hành rà soát lại quy trình cập nhật dữ liệu và điều chỉnh thời điểm truy vấn metadata để đảm bảo trạng thái hiển thị chính xác hơn.

Ngoài ra, việc kiểm thử với nhiều video có kích thước khác nhau cũng giúp nhóm đánh giá rõ hơn khả năng mở rộng của hệ thống. Kết quả cho thấy kiến trúc hướng sự kiện kết hợp với các dịch vụ Serverless có thể xử lý ổn định mà không cần can thiệp thủ công.

Thông qua các vòng kiểm thử cuối cùng, nhóm hiểu rõ hơn tầm quan trọng của việc đánh giá hệ thống sau khi triển khai, đặc biệt đối với các ứng dụng hoạt động trên nền tảng điện toán đám mây.

---

## VI. Đánh giá và Chiêm nghiệm chuyên môn

Sau mười hai tuần thực tập, nhóm đã hoàn thành mục tiêu xây dựng một nền tảng Video-on-Demand theo kiến trúc Serverless trên AWS.

Quá trình triển khai giúp nhóm tiếp cận thực tế với nhiều dịch vụ AWS như Amazon S3, Amazon API Gateway, AWS Lambda, Amazon DynamoDB, Amazon EventBridge, Amazon SQS, EventBridge Pipes, AWS Step Functions, AWS Elemental MediaConvert và Amazon CloudFront.

Bên cạnh kiến thức chuyên môn, nhóm cũng rèn luyện được kỹ năng phân tích yêu cầu, thiết kế hệ thống, xử lý lỗi, kiểm thử phần mềm và xây dựng tài liệu kỹ thuật. Đây là những kinh nghiệm quan trọng phục vụ cho quá trình học tập cũng như công việc trong tương lai.

Kết quả đạt được trong kỳ thực tập là nền tảng để tiếp tục nghiên cứu và phát triển các tính năng nâng cao cho hệ thống trong các giai đoạn tiếp theo.

---

## VII. Kế hoạch chiến lược & Định hướng phát triển

Sau khi hoàn thành kỳ thực tập, nhóm định hướng tiếp tục phát triển hệ thống theo hướng hoàn thiện hơn nhằm đáp ứng các nhu cầu thực tế.

Các hướng phát triển bao gồm:

- Bổ sung chức năng quản lý người dùng và phân quyền.
- Hỗ trợ nhiều chất lượng video khác nhau.
- Tự động tạo ảnh Thumbnail.
- Bổ sung thống kê lượt xem video.
- Triển khai thông báo sau khi xử lý hoàn tất.
- Tối ưu hiệu năng phát video trên nhiều thiết bị.
- Nâng cao khả năng giám sát thông qua Amazon CloudWatch.
- Mở rộng hệ thống để phục vụ số lượng người dùng lớn hơn.
- Tiếp tục tối ưu chi phí vận hành theo mô hình Serverless.
- Chuẩn bị triển khai hệ thống trong môi trường thực tế.