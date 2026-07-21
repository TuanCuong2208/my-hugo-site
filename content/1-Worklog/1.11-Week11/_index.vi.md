---
title: "Worklog Tuần 11"
date: 2026-06-30
weight: 11
chapter: false
pre: "<b> 1.11. </b> "
---

## I. Tóm tắt tổng quan

Sau khi hoàn thiện Pipeline xử lý video tự động theo kiến trúc Event-Driven trong tuần trước, nhóm tiếp tục triển khai tầng truy cập và phân phối nội dung của hệ thống. Mục tiêu của giai đoạn này là tích hợp toàn bộ các dịch vụ đã xây dựng thành một nền tảng Video-on-Demand hoàn chỉnh, cho phép người dùng xác thực, tải video, theo dõi trạng thái xử lý và phát nội dung trực tuyến thông qua hạ tầng AWS.

Trong tuần này, nhóm tập trung triển khai cơ chế xác thực người dùng bằng Amazon Cognito nhằm bảo vệ các API và kiểm soát quyền truy cập vào hệ thống. Đồng thời, giao diện Web được triển khai trên Amazon S3 Frontend Bucket và phân phối thông qua Amazon CloudFront nhằm tăng tốc độ truy cập, giảm độ trễ và nâng cao khả năng mở rộng khi phục vụ nhiều người dùng đồng thời.

Song song với việc triển khai tầng truy cập, nhóm tiến hành kết nối giao diện Web với Amazon API Gateway để thực hiện các chức năng như đăng nhập, tải video, truy vấn danh sách video và theo dõi trạng thái xử lý. Các API được tích hợp đồng bộ với Amazon DynamoDB để hiển thị thông tin metadata và trạng thái xử lý của từng video theo thời gian thực.

Ngoài ra, AWS WAF cũng được cấu hình phía trước CloudFront nhằm tăng cường khả năng bảo vệ hệ thống trước các truy cập bất thường và các cuộc tấn công phổ biến trên nền tảng Web. Việc bổ sung lớp bảo mật này giúp hoàn thiện kiến trúc nhiều tầng của hệ thống, đồng thời đáp ứng các yêu cầu cơ bản về an toàn thông tin đối với một nền tảng triển khai trên môi trường điện toán đám mây.

Kết thúc tuần làm việc, nhóm đã hoàn thành việc tích hợp tầng xác thực, tầng truy cập và tầng phân phối nội dung. Toàn bộ quy trình từ đăng nhập, tải video, xử lý bất đồng bộ đến phát video trực tuyến đã có thể hoạt động thống nhất trên cùng một hệ thống.

## II. Mục tiêu chiến lược trong tuần

Sau khi hoàn thiện Video Processing Pipeline, mục tiêu của tuần thứ 11 là triển khai tầng truy cập người dùng và tích hợp toàn bộ các thành phần của hệ thống thành một quy trình nghiệp vụ hoàn chỉnh.

Các mục tiêu chính bao gồm:

- Triển khai Amazon Cognito phục vụ xác thực người dùng.
- Tích hợp Amazon API Gateway với giao diện Web.
- Triển khai giao diện Web trên Amazon S3 Frontend Bucket.
- Phân phối giao diện và nội dung thông qua Amazon CloudFront.
- Cấu hình AWS WAF nhằm tăng cường bảo mật cho hệ thống.
- Đồng bộ dữ liệu metadata từ Amazon DynamoDB lên giao diện người dùng.
- Kiểm thử toàn bộ quy trình từ xác thực, tải video, xử lý và phát nội dung.
- Chuẩn bị nền tảng cho giai đoạn kiểm thử tổng thể và tối ưu hệ thống.

Thông qua các mục tiêu trên, nhóm hướng đến việc hoàn thiện phiên bản MVP với đầy đủ các chức năng cốt lõi của nền tảng Video-on-Demand.

## III. Nhật ký hoạt động & Lộ trình phân bổ chi tiết (Từ 30/06/2026 đến 06/07/2026)

| Thời gian | Danh mục hoạt động | Chi tiết các tác vụ thực hiện chuyên sâu | Kết quả/Minh chứng đạt được |
| :--- | :--- | :--- | :--- |
| **Ngày 1** *(30/06)* | User Authentication | Triển khai Amazon Cognito User Pool, cấu hình xác thực người dùng và tích hợp cơ chế cấp phát JWT Token. | Hoàn thành hệ thống xác thực người dùng trên nền tảng AWS. |
| **Ngày 2** *(01/07)* | API Integration | Kết nối giao diện Web với Amazon API Gateway để thực hiện các chức năng Upload Video, truy vấn metadata và danh sách video. | Các API hoạt động ổn định sau khi tích hợp với giao diện Web. |
| **Ngày 3** *(02/07)* | Frontend Deployment | Triển khai giao diện Web lên Amazon S3 Frontend Bucket và cấu hình Static Website Hosting. | Giao diện Web được triển khai thành công trên Amazon S3. |
| **Ngày 4** *(03/07)* | Content Delivery | Cấu hình Amazon CloudFront phân phối giao diện và nội dung video từ các Amazon S3 Bucket. | Nội dung được truy cập thông qua CloudFront với tốc độ phản hồi được cải thiện. |
| **Ngày 5** *(04/07)* | Security Enhancement | Cấu hình AWS WAF trước CloudFront, xây dựng các Rule cơ bản nhằm kiểm soát lưu lượng truy cập đến hệ thống. | Hoàn thiện lớp bảo vệ cho ứng dụng Web. |
| **Ngày 6** *(05/07)* | Integration Testing | Kiểm thử toàn bộ quy trình từ xác thực người dùng, Upload Video, xử lý bất đồng bộ đến phát video trực tuyến. | Toàn bộ các thành phần hoạt động đồng bộ theo kiến trúc thiết kế. |
| **Ngày 7** *(06/07)* | Review & Optimization | Đánh giá hiệu năng của tầng truy cập, rà soát cấu hình bảo mật và chuẩn bị cho giai đoạn kiểm thử tổng thể. | Hoàn thành tầng truy cập và phân phối nội dung của hệ thống. |

## IV. Thực thi kỹ thuật chuyên sâu & Phân tích chi tiết

Sau khi hoàn thiện Pipeline xử lý video bất đồng bộ trong tuần trước, nhóm tiếp tục triển khai tầng truy cập của hệ thống nhằm kết nối người dùng với toàn bộ các dịch vụ đã xây dựng trên AWS. Trọng tâm của tuần này là hoàn thiện cơ chế xác thực, triển khai giao diện Web, cấu hình tầng phân phối nội dung và tích hợp các API thành một quy trình nghiệp vụ thống nhất. Đây là bước cuối cùng trước khi chuyển sang giai đoạn kiểm thử và tối ưu toàn bộ hệ thống.

Công việc đầu tiên được thực hiện là triển khai Amazon Cognito để xây dựng cơ chế xác thực người dùng. Nhóm cấu hình User Pool nhằm quản lý tài khoản, đồng thời thiết lập quy trình đăng nhập và cấp phát JWT Token sau khi người dùng được xác thực thành công. Việc sử dụng Amazon Cognito giúp loại bỏ nhu cầu tự xây dựng hệ thống quản lý tài khoản, đồng thời tận dụng các cơ chế bảo mật được AWS cung cấp sẵn như quản lý phiên đăng nhập, mã hóa thông tin xác thực và xác minh người dùng.

Sau khi hoàn thiện cơ chế xác thực, Amazon API Gateway được cấu hình sử dụng Cognito Authorizer để kiểm tra Access Token trước khi cho phép truy cập các API của hệ thống. Chỉ những yêu cầu mang Token hợp lệ mới được phép thực hiện các chức năng như tải video, truy vấn danh sách video hoặc xem thông tin metadata. Việc tích hợp trực tiếp Cognito với API Gateway giúp giảm tải cho tầng Backend, đồng thời tăng cường khả năng bảo mật cho toàn bộ hệ thống.

Song song với đó, nhóm triển khai giao diện Web lên Amazon S3 Frontend Bucket dưới dạng Static Website. Việc lưu trữ giao diện trên Amazon S3 giúp đơn giản hóa quá trình triển khai, giảm chi phí vận hành và tận dụng khả năng mở rộng gần như không giới hạn của dịch vụ lưu trữ đối tượng. Sau khi triển khai thành công, toàn bộ nội dung giao diện được phân phối thông qua Amazon CloudFront nhằm giảm độ trễ khi người dùng truy cập từ nhiều vị trí địa lý khác nhau.

Amazon CloudFront cũng được cấu hình làm tầng phân phối nội dung cho các video đã được xử lý bởi AWS Elemental MediaConvert. Khi người dùng yêu cầu phát video, CloudFront ưu tiên phục vụ dữ liệu từ các Edge Location gần nhất. Trong trường hợp dữ liệu chưa tồn tại trong bộ nhớ đệm, CloudFront sẽ truy xuất nội dung từ Amazon S3 Processed Media Bucket trước khi lưu vào Cache để phục vụ cho các yêu cầu tiếp theo. Cơ chế này góp phần giảm tải cho dịch vụ lưu trữ và cải thiện đáng kể tốc độ phát video.

Để tăng cường mức độ an toàn cho hệ thống, nhóm triển khai AWS WAF phía trước Amazon CloudFront. Một số Rule cơ bản được cấu hình nhằm kiểm soát các truy cập bất thường, giới hạn lưu lượng từ các địa chỉ IP có dấu hiệu gửi quá nhiều yêu cầu trong thời gian ngắn và giảm nguy cơ khai thác các lỗ hổng phổ biến trên ứng dụng Web. Việc bổ sung AWS WAF giúp tăng thêm một lớp bảo vệ trước khi các yêu cầu được chuyển tiếp đến CloudFront và các dịch vụ Backend.

Sau khi tầng truy cập được hoàn thiện, nhóm tiến hành tích hợp giao diện Web với Amazon API Gateway để thực hiện toàn bộ quy trình nghiệp vụ. Khi người dùng tải video lên hệ thống, giao diện gửi yêu cầu lấy Presigned URL thông qua API Gateway. Sau khi tệp được tải trực tiếp lên Amazon S3 Raw Upload Bucket, trạng thái xử lý được cập nhật từ Amazon DynamoDB và hiển thị trên giao diện. Khi Pipeline xử lý hoàn tất và trạng thái chuyển sang **Completed**, người dùng có thể phát video thông qua đường dẫn được phân phối bởi Amazon CloudFront.

Để đánh giá khả năng hoạt động của hệ thống, nhóm thực hiện nhiều kịch bản kiểm thử bao gồm xác thực người dùng, tải video, xử lý bất đồng bộ, cập nhật trạng thái và phát video trực tuyến. Đồng thời, nhóm cũng kiểm tra khả năng xử lý khi nhiều người dùng thực hiện Upload đồng thời nhằm đánh giá hiệu quả của kiến trúc Serverless. Kết quả cho thấy các thành phần hoạt động đồng bộ, dữ liệu được cập nhật chính xác và toàn bộ quy trình nghiệp vụ diễn ra ổn định.

Đến cuối tuần, nhóm đã hoàn thành việc tích hợp tầng truy cập với toàn bộ hệ thống Backend. Người dùng có thể đăng nhập, tải video, theo dõi trạng thái xử lý và phát nội dung trực tuyến trên cùng một nền tảng. Đây là cột mốc quan trọng đánh dấu việc hoàn thiện phiên bản MVP của hệ thống về mặt chức năng.

## V. Thách thức hạ tầng, Nhật ký xử lý lỗi & Góc nhìn chuyên gia

Trong quá trình triển khai Amazon Cognito, nhóm gặp khó khăn khi cấu hình cơ chế xác thực giữa Cognito và Amazon API Gateway. Một số yêu cầu ban đầu bị từ chối do Access Token chưa được truyền đúng định dạng trong Header của HTTP Request. Sau khi rà soát cấu hình Cognito Authorizer và chuẩn hóa quy trình gửi Token, toàn bộ API đã được bảo vệ và hoạt động đúng theo cơ chế xác thực JWT.

Một vấn đề khác xuất hiện trong quá trình triển khai Amazon CloudFront. Sau khi cập nhật giao diện Web lên Amazon S3 Frontend Bucket, một số thay đổi chưa được phản ánh ngay do nội dung cũ vẫn còn trong bộ nhớ đệm của CloudFront. Nhóm đã thực hiện CloudFront Invalidation để làm mới Cache và đồng thời xây dựng quy trình cập nhật nội dung phù hợp nhằm bảo đảm người dùng luôn truy cập được phiên bản mới nhất của ứng dụng.

Trong quá trình cấu hình AWS WAF, nhóm nghiên cứu các Rule mặc định và lựa chọn áp dụng các chính sách phù hợp với phạm vi của đồ án. Việc triển khai WAF không chỉ giúp tăng cường khả năng bảo vệ ứng dụng mà còn giúp nhóm hiểu rõ hơn về mô hình bảo mật nhiều lớp khi triển khai hệ thống trên nền tảng AWS.

Thông qua quá trình tích hợp, nhóm nhận thấy việc sử dụng các dịch vụ Managed Services của AWS giúp giảm đáng kể khối lượng quản trị hạ tầng. Thay vì tập trung vào việc vận hành máy chủ, nhóm có thể tập trung nhiều hơn vào thiết kế kiến trúc và tối ưu luồng nghiệp vụ của hệ thống.

## VI. Đánh giá và Chiêm nghiệm chuyên môn

Tuần thứ 11 đánh dấu thời điểm toàn bộ các thành phần của hệ thống được tích hợp thành một nền tảng Video-on-Demand hoàn chỉnh. Việc kết nối tầng xác thực, tầng xử lý, tầng lưu trữ và tầng phân phối nội dung giúp nhóm có cái nhìn toàn diện hơn về cách xây dựng một ứng dụng Cloud-Native trên AWS.

Quá trình triển khai Amazon Cognito và Amazon API Gateway giúp nhóm hiểu rõ hơn về các cơ chế xác thực hiện đại dựa trên JWT cũng như phương pháp bảo vệ API trong môi trường Serverless. Đồng thời, việc triển khai Amazon CloudFront và AWS WAF cũng giúp nhóm tiếp cận với các giải pháp tối ưu hiệu năng và bảo mật thường được áp dụng trong các hệ thống thực tế.

Bên cạnh đó, nhóm nhận thấy kiến trúc nhiều tầng của hệ thống giúp việc mở rộng và bảo trì trở nên thuận lợi hơn. Mỗi dịch vụ đảm nhiệm một vai trò độc lập, giao tiếp với nhau thông qua các giao diện chuẩn, từ đó giảm sự phụ thuộc giữa các thành phần và tăng khả năng mở rộng trong tương lai.

Nhìn chung, toàn bộ mục tiêu của tuần đã được hoàn thành đúng kế hoạch. Phiên bản MVP của hệ thống đã đáp ứng đầy đủ các chức năng cốt lõi và sẵn sàng bước sang giai đoạn kiểm thử tổng thể, giám sát và tối ưu hiệu năng.

## VII. Kế hoạch chiến lược & Lộ trình tối ưu cho tuần tới

Trong tuần cuối của quá trình thực tập, nhóm sẽ tập trung kiểm thử toàn bộ hệ thống theo hướng End-to-End nhằm đánh giá tính ổn định của từng dịch vụ cũng như khả năng phối hợp giữa các thành phần trong kiến trúc Serverless.

Song song với quá trình kiểm thử, nhóm sẽ sử dụng Amazon CloudWatch để theo dõi nhật ký hoạt động, giám sát hiệu năng của Amazon API Gateway, AWS Lambda, AWS Step Functions và AWS Elemental MediaConvert. Đồng thời, nhóm sẽ rà soát cấu hình IAM, đánh giá hiệu quả của AWS WAF và tối ưu các tham số cấu hình nhằm cải thiện hiệu năng cũng như chi phí vận hành.

Cuối cùng, nhóm sẽ hoàn thiện tài liệu kỹ thuật, tổng hợp kết quả triển khai, chuẩn bị nội dung trình diễn hệ thống và xây dựng kịch bản Demo phục vụ cho quá trình báo cáo đồ án cũng như nghiệm thu kết quả thực tập.