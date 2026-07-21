---
title: "Worklog Tuần 9"
date: 2026-06-16
weight: 9
chapter: false
pre: "<b> 1.9. </b> "
---

# I. Tóm tắt tổng quan

Sau khi hoàn thành việc xây dựng nền tảng Backend cơ bản và cơ chế Upload Video sử dụng Presigned URL trong tuần trước, nhóm tiếp tục phát triển các thành phần cốt lõi phục vụ cho quy trình quản lý video của hệ thống. Trọng tâm của tuần này là hoàn thiện các API nghiệp vụ, xây dựng cơ chế quản lý metadata, tích hợp Amazon DynamoDB với các dịch vụ Backend và chuẩn bị hạ tầng cho Pipeline xử lý video theo kiến trúc Event-Driven ở giai đoạn tiếp theo.

Trong tuần làm việc này, nhóm tập trung phát triển các API trên Amazon API Gateway kết hợp với AWS Lambda để xử lý các chức năng như tạo thông tin video, truy vấn danh sách video, xem chi tiết metadata và cập nhật trạng thái xử lý. Đồng thời, Amazon DynamoDB được sử dụng làm cơ sở dữ liệu NoSQL lưu trữ toàn bộ metadata của video nhằm bảo đảm khả năng mở rộng và đáp ứng nhanh đối với các truy vấn có tần suất lớn.

Song song với việc phát triển Backend API, nhóm tiếp tục hoàn thiện quy trình Upload Video bằng Presigned URL. Sau khi người dùng gửi yêu cầu tải video, hệ thống sinh URL tạm thời để người dùng tải trực tiếp tệp lên Amazon S3 Raw Upload Bucket mà không cần truyền dữ liệu qua Backend. Cách tiếp cận này giúp giảm tải cho AWS Lambda, tiết kiệm tài nguyên tính toán và nâng cao hiệu năng của hệ thống.

Ngoài ra, nhóm cũng tiến hành chuẩn hóa cấu trúc metadata được lưu trong Amazon DynamoDB nhằm phục vụ cho việc theo dõi trạng thái xử lý video ở các giai đoạn tiếp theo. Các trường dữ liệu như Video ID, File Name, Upload Time, Processing Status, Output URL và User ID được thiết kế thống nhất để bảo đảm khả năng mở rộng khi tích hợp với Pipeline xử lý video trong tuần kế tiếp.

Đến cuối tuần, toàn bộ tầng Backend API và hệ thống quản lý metadata đã được hoàn thiện. Người dùng có thể tải video lên Amazon S3 thông qua Presigned URL, trong khi hệ thống có thể lưu trữ, truy vấn và quản lý đầy đủ thông tin của từng video, tạo nền tảng cho việc triển khai quy trình xử lý video bất đồng bộ theo kiến trúc Serverless.

# II. Mục tiêu chiến lược trong tuần

Sau khi hoàn thiện chức năng Upload Video, mục tiêu của tuần thứ 9 là xây dựng tầng quản lý dữ liệu và các API phục vụ toàn bộ quy trình nghiệp vụ của nền tảng Video-on-Demand.

Các mục tiêu chính bao gồm:

- Hoàn thiện hệ thống Backend API sử dụng Amazon API Gateway và AWS Lambda.
- Thiết kế cấu trúc metadata lưu trữ trên Amazon DynamoDB.
- Xây dựng API tạo mới và quản lý thông tin video.
- Phát triển API truy vấn danh sách và chi tiết video.
- Đồng bộ metadata với quá trình Upload Video.
- Kiểm thử quy trình Upload sử dụng Presigned URL.
- Tối ưu cấu hình IAM và CORS cho các API.
- Chuẩn bị dữ liệu phục vụ Pipeline xử lý video Event-Driven của tuần tiếp theo.

Thông qua các mục tiêu trên, nhóm hướng đến việc hoàn thiện tầng Backend của hệ thống, bảo đảm toàn bộ dữ liệu được quản lý tập trung và sẵn sàng cho giai đoạn xử lý video tự động.

# III. Nhật ký hoạt động & Lộ trình phân bổ chi tiết (Từ 16/06/2026 đến 22/06/2026)

| Thời gian | Danh mục hoạt động | Chi tiết các tác vụ thực hiện chuyên sâu | Kết quả/Minh chứng đạt được |
| :--- | :--- | :--- | :--- |
| **Ngày 1** *(16/06)* | Backend API Design | Thiết kế các API phục vụ Upload Video, quản lý metadata và truy vấn danh sách video thông qua Amazon API Gateway. | Hoàn thiện tài liệu thiết kế API của hệ thống. |
| **Ngày 2** *(17/06)* | Lambda Development | Xây dựng các AWS Lambda Function xử lý tạo metadata, truy vấn thông tin video và cập nhật dữ liệu trên Amazon DynamoDB. | Các Lambda Function hoạt động đúng theo yêu cầu nghiệp vụ. |
| **Ngày 3** *(18/06)* | DynamoDB Integration | Thiết kế bảng lưu trữ metadata và tích hợp Amazon DynamoDB với hệ thống Backend. | Metadata của video được lưu trữ và truy xuất thành công. |
| **Ngày 4** *(19/06)* | Upload Workflow | Hoàn thiện quy trình Upload Video bằng Presigned URL và đồng bộ metadata sau khi Upload thành công. | Quy trình Upload hoạt động ổn định và dữ liệu được cập nhật chính xác. |
| **Ngày 5** *(20/06)* | API Testing | Kiểm thử các API CRUD, truy vấn metadata và kiểm tra xử lý lỗi trong nhiều tình huống khác nhau. | Các API phản hồi chính xác và ổn định. |
| **Ngày 6** *(21/06)* | Security Configuration | Rà soát IAM Role, cấu hình CORS và kiểm tra quyền truy cập giữa Amazon API Gateway, AWS Lambda, Amazon DynamoDB và Amazon S3. | Hoàn thiện cấu hình bảo mật của tầng Backend. |
| **Ngày 7** *(22/06)* | Review & Preparation | Đánh giá kiến trúc Backend, rà soát metadata và chuẩn bị hạ tầng cho Event-Driven Processing Pipeline. | Sẵn sàng triển khai Pipeline xử lý video trong tuần tiếp theo. |

# IV. Thực thi kỹ thuật chuyên sâu & Phân tích chi tiết

Sau khi hoàn thành cơ chế tải video trực tiếp lên Amazon S3 thông qua Presigned URL ở tuần trước, nhóm tiếp tục tập trung xây dựng tầng Backend phục vụ việc quản lý dữ liệu và điều phối các chức năng nghiệp vụ của nền tảng Video-on-Demand. Mục tiêu chính trong giai đoạn này là chuẩn hóa luồng trao đổi dữ liệu giữa giao diện người dùng, Amazon API Gateway, AWS Lambda, Amazon DynamoDB và Amazon S3, đồng thời chuẩn bị đầy đủ dữ liệu đầu vào cho Pipeline xử lý video theo kiến trúc Event-Driven sẽ được triển khai trong tuần tiếp theo.

Công việc đầu tiên của nhóm là thiết kế các RESTful API trên Amazon API Gateway. Các API được phân chia theo từng nhóm chức năng riêng biệt bao gồm tạo thông tin video, truy vấn danh sách video, lấy thông tin chi tiết của từng video, cập nhật trạng thái xử lý và sinh Presigned URL phục vụ Upload Video. Việc tách biệt rõ ràng các API giúp kiến trúc hệ thống dễ bảo trì hơn, đồng thời tạo điều kiện thuận lợi cho việc mở rộng các chức năng trong tương lai mà không ảnh hưởng đến những thành phần đã triển khai.

Sau khi hoàn thiện thiết kế API, nhóm triển khai các AWS Lambda Function tương ứng để xử lý toàn bộ nghiệp vụ phía Backend. Mỗi Lambda Function đảm nhiệm một chức năng độc lập như tạo metadata mới, truy vấn dữ liệu từ Amazon DynamoDB hoặc trả về Presigned URL cho người dùng. Cách tổ chức này phù hợp với mô hình Microservices trên nền tảng Serverless, giúp từng thành phần có thể được phát triển, kiểm thử và cập nhật một cách độc lập.

Để lưu trữ thông tin của video, nhóm thiết kế bảng dữ liệu trên Amazon DynamoDB với khóa chính là **Video ID** nhằm bảo đảm mỗi video có một định danh duy nhất. Ngoài khóa chính, bảng còn lưu trữ nhiều thuộc tính quan trọng như tên tệp, thời điểm tải lên, người tải, trạng thái xử lý, vị trí lưu trữ tệp nguồn và vị trí của video sau khi xử lý. Cấu trúc dữ liệu này được xây dựng theo hướng mở rộng để có thể bổ sung thêm các trường thông tin mới mà không cần thay đổi kiến trúc cơ sở dữ liệu.

Sau khi người dùng yêu cầu tải video, giao diện Web gửi yêu cầu đến Amazon API Gateway để lấy Presigned URL. AWS Lambda tạo URL tạm thời dựa trên Amazon S3 SDK và trả kết quả về cho người dùng. Video sau đó được tải trực tiếp lên Amazon S3 Raw Upload Bucket mà không đi qua Backend. Đồng thời, hệ thống tạo bản ghi metadata trên Amazon DynamoDB với trạng thái ban đầu là **Uploaded**, tạo cơ sở để các dịch vụ xử lý video có thể tiếp tục theo dõi trong các giai đoạn tiếp theo.

Nhóm cũng xây dựng các API phục vụ truy vấn danh sách video và xem chi tiết từng video. Dữ liệu được lấy trực tiếp từ Amazon DynamoDB và trả về dưới dạng JSON thông qua Amazon API Gateway. Nhờ vậy, giao diện Web có thể hiển thị danh sách video đã tải lên cùng các thông tin liên quan như thời gian tải lên, trạng thái xử lý và thông tin người dùng mà không cần truy cập trực tiếp vào cơ sở dữ liệu.

Song song với việc phát triển chức năng nghiệp vụ, nhóm tiến hành cấu hình IAM Role cho từng dịch vụ nhằm bảo đảm AWS Lambda chỉ được phép truy cập vào các tài nguyên cần thiết. Các quyền truy cập đến Amazon S3, Amazon DynamoDB và Amazon API Gateway đều được kiểm tra cẩn thận để tuân thủ nguyên tắc **Least Privilege**, góp phần giảm thiểu các rủi ro bảo mật trong quá trình vận hành.

Sau khi hoàn thiện toàn bộ Backend API, nhóm thực hiện nhiều kịch bản kiểm thử khác nhau nhằm đánh giá tính ổn định của hệ thống. Các tình huống kiểm thử bao gồm tải video thành công, tải video thất bại, truy vấn metadata của video tồn tại hoặc không tồn tại, đồng thời kiểm tra khả năng phản hồi của các API khi nhiều yêu cầu được gửi liên tục. Kết quả cho thấy các Lambda Function hoạt động ổn định, dữ liệu trên Amazon DynamoDB được cập nhật chính xác và toàn bộ quy trình Upload diễn ra đúng như thiết kế.

Cuối tuần, nhóm tiến hành rà soát lại toàn bộ kiến trúc Backend nhằm chuẩn bị cho việc triển khai Pipeline xử lý video tự động ở tuần tiếp theo. Metadata đã được chuẩn hóa, quy trình Upload đã hoạt động ổn định và các API đã sẵn sàng để tích hợp với Amazon EventBridge, Amazon SQS, EventBridge Pipes, AWS Step Functions và AWS Elemental MediaConvert trong giai đoạn xử lý bất đồng bộ.

# V. Thách thức hạ tầng, Nhật ký xử lý lỗi & Góc nhìn chuyên gia

Trong quá trình xây dựng Backend API, nhóm gặp khó khăn khi đồng bộ dữ liệu giữa Amazon S3 và Amazon DynamoDB. Một số trường hợp người dùng hủy quá trình Upload trước khi hoàn tất dẫn đến việc metadata đã được tạo nhưng tệp video chưa xuất hiện trong Amazon S3 Raw Upload Bucket. Để xử lý tình huống này, nhóm bổ sung cơ chế kiểm tra trạng thái Upload trước khi các bước xử lý tiếp theo được thực hiện, giúp bảo đảm tính nhất quán giữa dữ liệu lưu trữ và metadata.

Một vấn đề khác xuất hiện trong quá trình cấu hình IAM Role cho AWS Lambda. Ban đầu một số quyền truy cập chưa được cấp đầy đủ khiến Lambda không thể ghi dữ liệu vào Amazon DynamoDB hoặc tạo Presigned URL cho Amazon S3. Sau khi rà soát chính sách IAM và điều chỉnh quyền theo từng dịch vụ, toàn bộ chức năng của Backend hoạt động ổn định và tuân thủ nguyên tắc phân quyền tối thiểu.

Trong quá trình kiểm thử API, nhóm cũng tiến hành đánh giá cấu hình CORS giữa giao diện Web và Amazon API Gateway. Một số yêu cầu HTTP bị trình duyệt từ chối do thiếu các Header cần thiết trong phản hồi của API. Sau khi bổ sung đầy đủ cấu hình CORS, toàn bộ các yêu cầu từ giao diện Web có thể thực hiện thành công mà vẫn bảo đảm các chính sách bảo mật của trình duyệt.

Thông qua các hoạt động triển khai và kiểm thử, nhóm nhận thấy rằng việc tách biệt hoàn toàn tầng Upload, tầng lưu trữ metadata và tầng xử lý video mang lại nhiều lợi ích về khả năng mở rộng. Kiến trúc này giúp mỗi thành phần có thể được phát triển và mở rộng độc lập, đồng thời tạo tiền đề để áp dụng mô hình Event-Driven Processing trong các giai đoạn tiếp theo.

# VI. Đánh giá và Chiêm nghiệm chuyên môn

Tuần thứ 9 giúp nhóm hiểu rõ hơn về vai trò của tầng Backend trong một hệ thống Serverless. Bên cạnh việc cung cấp các API phục vụ người dùng, Backend còn chịu trách nhiệm điều phối dữ liệu giữa nhiều dịch vụ AWS khác nhau, bảo đảm tính nhất quán của thông tin và tạo nền tảng cho các quy trình xử lý tự động phía sau.

Quá trình làm việc với Amazon API Gateway, AWS Lambda và Amazon DynamoDB giúp nhóm tích lũy thêm kinh nghiệm về thiết kế API, quản lý metadata và xây dựng các dịch vụ độc lập theo kiến trúc Serverless. Đồng thời, việc sử dụng Presigned URL để tải trực tiếp dữ liệu lên Amazon S3 cũng giúp giảm đáng kể tải xử lý cho Backend và tối ưu hiệu quả sử dụng tài nguyên trên nền tảng AWS.

Ngoài ra, nhóm nhận thấy rằng việc chuẩn hóa metadata ngay từ đầu đóng vai trò rất quan trọng đối với toàn bộ vòng đời của video. Khi dữ liệu được tổ chức hợp lý, việc tích hợp với Pipeline xử lý bất đồng bộ, hệ thống giám sát và giao diện người dùng ở các giai đoạn sau trở nên đơn giản và thuận lợi hơn.

Nhìn chung, toàn bộ mục tiêu của tuần đã được hoàn thành đúng kế hoạch. Tầng Backend và hệ thống quản lý metadata đã sẵn sàng để tích hợp với kiến trúc Event-Driven, đánh dấu bước chuyển từ giai đoạn quản lý dữ liệu sang giai đoạn tự động hóa quy trình xử lý video.

# VII. Kế hoạch chiến lược & Lộ trình tối ưu cho tuần tới

Trong tuần tiếp theo, nhóm sẽ triển khai **Event-Driven Video Processing Pipeline** nhằm tự động hóa toàn bộ quy trình xử lý video sau khi người dùng tải tệp lên Amazon S3 Raw Upload Bucket.

Các nội dung chính sẽ bao gồm tích hợp Amazon EventBridge để tiếp nhận sự kiện Upload Video, sử dụng Amazon SQS làm hàng đợi xử lý bất đồng bộ, cấu hình EventBridge Pipes để truyền dữ liệu giữa các dịch vụ và xây dựng Workflow bằng AWS Step Functions nhằm điều phối toàn bộ quy trình chuyển mã video.

Bên cạnh đó, AWS Elemental MediaConvert sẽ được tích hợp để chuyển đổi video sang định dạng HLS phục vụ phát trực tuyến, đồng thời cập nhật trạng thái xử lý vào Amazon DynamoDB sau mỗi giai đoạn của Pipeline. Kết quả cuối cùng sẽ được lưu trữ trong Amazon S3 Processed Media Bucket, tạo nền tảng cho việc phân phối nội dung thông qua Amazon CloudFront ở các tuần tiếp theo.