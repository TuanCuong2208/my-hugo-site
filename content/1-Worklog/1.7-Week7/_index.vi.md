---
title: "Worklog Tuần 7"
date: 2026-06-02
weight: 7
chapter: false
pre: "<b>1.7. </b>"
---

### I. Tóm tắt tổng quan

Tuần thứ 7 đánh dấu giai đoạn chuyển tiếp quan trọng trong quá trình thực tập khi nhóm hoàn thành chương trình AWS Academy và bắt đầu nghiên cứu, thiết kế giải pháp cho đồ án thực tế. Thay vì tiếp tục thực hiện các bài thực hành riêng lẻ như những tuần trước, nhóm tập trung hệ thống hóa kiến thức đã học và phân tích yêu cầu của một hệ thống hoàn chỉnh trên nền tảng AWS.

Sau quá trình trao đổi và đánh giá nhiều hướng triển khai, nhóm thống nhất lựa chọn đề tài **Serverless Video-on-Demand Platform on AWS**. Mục tiêu của dự án là xây dựng một nền tảng cho phép người dùng đăng nhập, tải video lên, theo dõi trạng thái xử lý và phát video sau khi hệ thống hoàn tất quá trình chuyển mã.

Trong tuần làm việc này, nhóm tập trung khảo sát các mô hình kiến trúc Cloud, đánh giá khả năng áp dụng kiến trúc Serverless và Event-Driven Architecture đối với bài toán xử lý video. Đây là loại tác vụ có dung lượng dữ liệu lớn và thời gian xử lý dài, vì vậy hệ thống cần được thiết kế theo hướng bất đồng bộ để tránh làm gián đoạn trải nghiệm của người dùng.

Nhóm cũng phân tích vai trò của các dịch vụ AWS dự kiến sử dụng trong dự án, bao gồm Amazon S3, Amazon CloudFront, Amazon Cognito, Amazon API Gateway, AWS Lambda, Amazon DynamoDB, Amazon EventBridge, Amazon SQS, EventBridge Pipes, AWS Step Functions, AWS Elemental MediaConvert và Amazon CloudWatch.

Bên cạnh việc xác định các thành phần kỹ thuật, nhóm tiến hành phân chia hệ thống thành các lớp chính gồm Web Application, Backend API, Metadata Storage và Video Processing Pipeline. Việc phân chia này giúp giảm sự phụ thuộc giữa các thành phần, đồng thời tạo điều kiện thuận lợi cho quá trình triển khai và kiểm thử trong các tuần tiếp theo.

Kết thúc tuần làm việc, nhóm đã hoàn thiện tài liệu phân tích yêu cầu, xác định phạm vi MVP, thống nhất kiến trúc serverless làm định hướng phát triển và xây dựng lộ trình triển khai theo từng giai đoạn của dự án.

---

### II. Mục tiêu chiến lược trong tuần

Mục tiêu trọng tâm của tuần thứ 7 là chuyển từ giai đoạn học tập các dịch vụ AWS riêng lẻ sang giai đoạn nghiên cứu và thiết kế một hệ thống thực tế. Nhóm ưu tiên xây dựng nền tảng kỹ thuật rõ ràng trước khi bắt đầu triển khai hạ tầng và phát triển các chức năng.

Các mục tiêu chính trong tuần bao gồm:

- Tổng hợp và hệ thống hóa kiến thức đã học trong chương trình AWS Academy.
- Phân tích yêu cầu nghiệp vụ của nền tảng Video-on-Demand.
- Xác định phạm vi chức năng của phiên bản MVP.
- Khảo sát các mô hình kiến trúc phù hợp trên AWS.
- Đánh giá khả năng áp dụng Serverless Architecture và Event-Driven Architecture.
- Xác định vai trò của từng dịch vụ AWS trong hệ thống.
- Thiết kế luồng tải lên và xử lý video theo cơ chế bất đồng bộ.
- Phân chia dự án thành các module Backend, Video Processing Pipeline và Web Application.
- Xây dựng lộ trình triển khai cho các tuần tiếp theo.
- Chuẩn bị tài liệu kỹ thuật và môi trường phục vụ quá trình phát triển.

Thông qua các mục tiêu trên, nhóm hướng đến việc xây dựng một định hướng kiến trúc có tính khả thi, phù hợp với thời gian thực tập và có thể mở rộng khi cần thiết.

---

### III. Nhật ký hoạt động & Lộ trình phân bổ chi tiết

| Thời gian | Danh mục hoạt động | Nội dung thực hiện | Kết quả |
| :--- | :--- | :--- | :--- |
| **Ngày 1** *(02/06)* | Tổng hợp kiến thức AWS | Rà soát các nội dung đã học về Compute, Storage, Database, Networking, Security và Serverless trong chương trình AWS Academy. | Hoàn thiện tài liệu tổng hợp kiến thức và định hướng áp dụng vào đồ án. |
| **Ngày 2** *(03/06)* | Phân tích yêu cầu nghiệp vụ | Xác định đối tượng sử dụng, mục tiêu hệ thống và các chức năng chính như đăng nhập, tải video, quản lý metadata, theo dõi trạng thái và phát video. | Hoàn thiện phạm vi chức năng của phiên bản MVP. |
| **Ngày 3** *(04/06)* | Khảo sát mô hình kiến trúc | Nghiên cứu kiến trúc truyền thống, Serverless Architecture và Event-Driven Architecture để đánh giá mức độ phù hợp với bài toán xử lý video. | Thống nhất lựa chọn kiến trúc Serverless kết hợp mô hình hướng sự kiện. |
| **Ngày 4** *(05/06)* | Lựa chọn dịch vụ AWS | Phân tích vai trò của Amazon S3, CloudFront, Cognito, API Gateway, Lambda, DynamoDB, EventBridge, SQS, EventBridge Pipes, Step Functions và MediaConvert. | Hoàn thiện danh sách các dịch vụ AWS dự kiến sử dụng. |
| **Ngày 5** *(06/06)* | Thiết kế luồng xử lý | Xây dựng luồng từ khi người dùng yêu cầu tải video, nhận Presigned URL, tải lên S3 Raw Bucket, kích hoạt pipeline và lưu kết quả vào S3 Processed Bucket. | Hoàn thiện luồng nghiệp vụ tổng thể của hệ thống. |
| **Ngày 6** *(07/06)* | Phân chia module dự án | Chia hệ thống thành Web Application, Backend API, Metadata Storage và Video Processing Pipeline để thuận tiện cho triển khai. | Hoàn thiện kế hoạch phát triển theo từng module chức năng. |
| **Ngày 7** *(08/06)* | Tổng kết và chuẩn bị | Rà soát tài liệu nghiên cứu, thống nhất định hướng kỹ thuật và chuẩn bị nội dung cho giai đoạn thiết kế chi tiết. | Sẵn sàng chuyển sang tuần hoàn thiện thiết kế và chuẩn bị hạ tầng AWS. |

### IV. Thực thi kỹ thuật chuyên sâu & Phân tích chi tiết

Sau khi hoàn thành chương trình AWS Academy, nhóm bước sang giai đoạn nghiên cứu và xây dựng định hướng kỹ thuật cho đồ án. Thay vì triển khai ngay các dịch vụ trên AWS, nhóm ưu tiên phân tích yêu cầu nghiệp vụ, khảo sát các mô hình kiến trúc và lựa chọn giải pháp phù hợp với bài toán Video-on-Demand.

Qua quá trình nghiên cứu, nhóm thống nhất lựa chọn kiến trúc **Serverless** kết hợp với **Event-Driven Architecture** nhằm tận dụng khả năng mở rộng tự động của AWS, giảm chi phí vận hành và hạn chế việc quản lý hạ tầng. Đây cũng là mô hình phù hợp với hệ thống xử lý video do quá trình chuyển đổi định dạng thường mất nhiều thời gian và cần được thực hiện theo cơ chế bất đồng bộ.

Đối với tầng giao diện, nhóm dự kiến triển khai Website dưới dạng Static Web Hosting trên Amazon S3 kết hợp với Amazon CloudFront để tăng tốc độ truy cập và phân phối nội dung đến người dùng. Mô hình này giúp tách biệt Frontend với Backend, đồng thời đơn giản hóa quá trình triển khai và mở rộng hệ thống.

Đối với lớp xử lý nghiệp vụ, Amazon API Gateway được lựa chọn làm cổng tiếp nhận các yêu cầu từ phía người dùng. Các API sẽ được triển khai bằng AWS Lambda nhằm xử lý các chức năng như đăng nhập, tạo Presigned URL, quản lý metadata và truy vấn danh sách video. Cách tiếp cận này giúp hệ thống chỉ sử dụng tài nguyên khi có yêu cầu phát sinh, phù hợp với mô hình Serverless.

Đối với dữ liệu nghiệp vụ, nhóm lựa chọn Amazon DynamoDB để lưu trữ metadata của video. Các thông tin dự kiến bao gồm Video ID, tiêu đề, trạng thái xử lý, đường dẫn lưu trữ, thời gian tạo và thông tin người tải lên. Việc sử dụng DynamoDB giúp tăng khả năng mở rộng và đáp ứng tốt các yêu cầu truy vấn của hệ thống.

Thành phần quan trọng nhất của dự án là Video Processing Pipeline. Sau khi nghiên cứu nhiều phương án triển khai, nhóm quyết định xây dựng quy trình xử lý theo kiến trúc hướng sự kiện. Theo đó, sau khi người dùng tải video lên Amazon S3 Raw Upload Bucket thông qua Presigned URL, hệ thống sẽ phát sinh sự kiện để kích hoạt Pipeline xử lý.

Pipeline dự kiến sử dụng Amazon EventBridge, Amazon SQS, EventBridge Pipes và AWS Step Functions để điều phối các bước xử lý trước khi khởi tạo MediaConvert Job. Sau khi AWS Elemental MediaConvert hoàn tất quá trình chuyển mã, video sẽ được lưu tại Amazon S3 Processed Media Bucket và trạng thái xử lý sẽ được cập nhật vào Amazon DynamoDB.

Bên cạnh các thành phần chính, nhóm cũng xác định Amazon Cognito sẽ được sử dụng cho chức năng xác thực người dùng, trong khi Amazon CloudWatch hỗ trợ theo dõi log và giám sát hoạt động của toàn bộ hệ thống. Đây đều là các dịch vụ cần thiết để xây dựng một nền tảng Video-on-Demand có khả năng mở rộng và dễ dàng vận hành trong thực tế.

---

### V. Thách thức hạ tầng, Nhật ký xử lý & Góc nhìn chuyên môn

Mặc dù tuần thứ 7 chưa triển khai hạ tầng thực tế, nhóm đã xác định một số thách thức quan trọng cần giải quyết trước khi bắt đầu phát triển hệ thống.

Thách thức đầu tiên là lựa chọn kiến trúc phù hợp cho quá trình xử lý video. Nếu toàn bộ quá trình upload và chuyển mã được thực hiện theo cơ chế đồng bộ, thời gian phản hồi sẽ tăng lên đáng kể và dễ vượt quá giới hạn của các dịch vụ Serverless. Vì vậy, nhóm quyết định áp dụng mô hình xử lý bất đồng bộ nhằm tách biệt quá trình tải video và xử lý video.

Một vấn đề khác là việc tải các tệp video có dung lượng lớn. Nhóm thống nhất sử dụng Presigned URL để người dùng tải trực tiếp video lên Amazon S3 thay vì truyền dữ liệu qua Backend. Cách tiếp cận này giúp giảm tải cho API Gateway và Lambda, đồng thời tối ưu chi phí truyền dữ liệu.

Bên cạnh đó, việc đồng bộ dữ liệu giữa Amazon S3 và Amazon DynamoDB cũng được xem là một nội dung cần được thiết kế cẩn thận. Nhóm dự kiến sử dụng một Video ID duy nhất để liên kết metadata trong DynamoDB với các đối tượng lưu trữ trên S3, giúp quá trình quản lý và truy vấn dữ liệu trở nên đơn giản hơn.

Ngoài ra, nhóm cũng nhận thấy việc phân quyền truy cập giữa các dịch vụ AWS cần được thực hiện theo nguyên tắc Least Privilege nhằm hạn chế các rủi ro về bảo mật khi hệ thống bắt đầu được triển khai.

---

### VI. Đánh giá và Chiêm nghiệm chuyên môn

Tuần thứ 7 không tập trung vào việc lập trình mà chủ yếu dành cho quá trình nghiên cứu, phân tích và thiết kế hệ thống. Đây là bước chuẩn bị quan trọng trước khi triển khai các thành phần kỹ thuật trong những tuần tiếp theo.

Thông qua việc khảo sát các dịch vụ AWS và phân tích yêu cầu của bài toán Video-on-Demand, nhóm hiểu rõ hơn cách phối hợp giữa Amazon S3, API Gateway, Lambda, DynamoDB, EventBridge, SQS, Step Functions và MediaConvert để xây dựng một hệ thống Serverless hoàn chỉnh.

Bên cạnh kiến thức kỹ thuật, nhóm cũng rèn luyện kỹ năng phân tích yêu cầu, đánh giá giải pháp và xây dựng lộ trình triển khai phù hợp với phạm vi của đồ án. Những kết quả đạt được trong tuần này sẽ là nền tảng quan trọng cho giai đoạn hiện thực hóa hệ thống ở các tuần tiếp theo.

---

### VII. Kế hoạch cho tuần tiếp theo

Sau khi hoàn thành giai đoạn nghiên cứu và thiết kế tổng thể, nhóm sẽ chuyển sang giai đoạn chuẩn bị triển khai hệ thống trên AWS.

Các công việc dự kiến bao gồm:

- Hoàn thiện thiết kế kỹ thuật của hệ thống.
- Chuẩn bị môi trường phát triển trên AWS.
- Thiết lập cấu trúc dự án và kho mã nguồn.
- Xây dựng Amazon S3 Bucket và Amazon DynamoDB.
- Thiết kế các API đầu tiên bằng Amazon API Gateway và AWS Lambda.
- Chuẩn bị nền tảng cho Video Processing Pipeline.
- Xây dựng Website phục vụ quá trình kiểm thử hệ thống.

Mục tiêu của tuần tiếp theo là hoàn thiện hạ tầng ban đầu và triển khai các thành phần cốt lõi để tạo nền tảng cho việc phát triển đầy đủ hệ thống **Serverless Video-on-Demand Platform on AWS** trong các giai đoạn sau.