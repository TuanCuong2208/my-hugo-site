---
title: "Worklog Tuần 7"
date: 2026-06-02
weight: 7
chapter: false
pre: "<b> 1.7. </b> "
---

### I. Tóm tắt tổng quan (Executive Summary)

Tuần thứ 7 đánh dấu bước chuyển quan trọng trong quá trình thực tập khi nhóm hoàn thành giai đoạn học tập và thực hành các dịch vụ nền tảng của AWS Academy, đồng thời bắt đầu nghiên cứu và xây dựng định hướng triển khai đồ án thực tế. Thay vì tiếp tục thực hiện các bài Lab độc lập như các tuần trước, nhóm tập trung hệ thống hóa toàn bộ kiến thức đã tích lũy nhằm lựa chọn giải pháp phù hợp cho bài toán phát triển một hệ thống **Mini Video-on-Demand Platform using AWS Serverless**.

Trong tuần làm việc này, nhóm tiến hành phân tích yêu cầu nghiệp vụ của hệ thống, khảo sát các mô hình kiến trúc đang được áp dụng trên nền tảng AWS và đánh giá khả năng đáp ứng của từng dịch vụ đối với các thành phần trong hệ thống. Dựa trên kết quả nghiên cứu, nhóm thống nhất lựa chọn kiến trúc **Serverless** kết hợp mô hình **Event-Driven Architecture** nhằm tận dụng khả năng mở rộng linh hoạt, giảm chi phí vận hành và hạn chế việc quản trị hạ tầng.

Song song với quá trình nghiên cứu, nhóm cũng tiến hành xây dựng phiên bản đầu tiên của kiến trúc tổng thể, xác định vai trò của các dịch vụ như Amazon S3, Amazon API Gateway, AWS Lambda, Amazon Cognito, Amazon DynamoDB, Amazon CloudFront, Amazon SQS và AWS Elemental MediaConvert trong từng giai đoạn xử lý của hệ thống. Đây là cơ sở ban đầu để nhóm tiếp tục hiện thực hóa từng module chức năng trong các tuần tiếp theo.

Kết thúc tuần làm việc, nhóm đã hoàn thiện bản thiết kế kiến trúc sơ bộ, xác định được lộ trình triển khai cho từng giai đoạn phát triển và chuẩn bị các tài liệu cần thiết phục vụ quá trình xây dựng hệ thống trong thời gian tới.

### II. Mục tiêu chiến lược trong tuần (Strategic Objectives)

Sau khi hoàn thành chương trình AWS Academy, mục tiêu trọng tâm của tuần thứ 7 là chuyển đổi từ giai đoạn học tập sang giai đoạn nghiên cứu và thiết kế giải pháp cho đồ án thực tập. Nhóm tập trung xây dựng nền tảng kỹ thuật vững chắc trước khi bắt đầu quá trình hiện thực hóa hệ thống.

Các mục tiêu chính được đặt ra trong tuần bao gồm:

- Tổng hợp và hệ thống hóa toàn bộ kiến thức đã học từ chương trình AWS Academy để phục vụ việc thiết kế hệ thống.
- Phân tích yêu cầu nghiệp vụ của nền tảng Video-on-Demand và xác định các chức năng cốt lõi cần triển khai.
- Khảo sát các mô hình kiến trúc trên AWS, đánh giá ưu và nhược điểm của từng phương án trước khi lựa chọn mô hình Serverless.
- Xác định các dịch vụ AWS phù hợp cho từng thành phần của hệ thống như xác thực người dùng, xử lý nghiệp vụ, lưu trữ dữ liệu, xử lý video và phân phối nội dung.
- Xây dựng bản thiết kế kiến trúc tổng thể phiên bản đầu tiên (Architecture Draft V1) làm cơ sở cho việc triển khai trong các tuần tiếp theo.
- Lập kế hoạch phát triển dự án theo từng giai đoạn nhằm đảm bảo tiến độ và khả năng mở rộng của hệ thống.

Thông qua các mục tiêu trên, nhóm hướng đến việc hình thành một kiến trúc ban đầu có tính khả thi, đồng thời tạo tiền đề để từng bước triển khai các module chức năng trong giai đoạn phát triển của đồ án.

### III. Nhật ký hoạt động & Lộ trình phân bổ chi tiết (Từ 02/06/2026 đến 08/06/2026)

| Thời gian | Danh mục hoạt động | Chi tiết các tác vụ thực hiện chuyên sâu | Kết quả/Minh chứng đạt được |
| :--- | :--- | :--- | :--- |
| **Ngày 1** *(02/06)* | Tổng hợp kiến thức AWS | Rà soát và hệ thống hóa toàn bộ kiến thức đã học về Compute, Storage, Database, Networking, Security và Serverless trong chương trình AWS Academy nhằm chuẩn bị áp dụng vào đồ án thực tập. | Hoàn thiện tài liệu tổng hợp các dịch vụ AWS và định hướng lựa chọn công nghệ cho hệ thống. |
| **Ngày 2** *(03/06)* | Phân tích yêu cầu nghiệp vụ | Thảo luận yêu cầu của hệ thống Video-on-Demand, xác định các chức năng chính như quản lý người dùng, tải video, xử lý video và phát video trực tuyến. | Xây dựng tài liệu mô tả phạm vi chức năng và luồng nghiệp vụ của hệ thống. |
| **Ngày 3** *(04/06)* | Khảo sát giải pháp triển khai | Nghiên cứu các mô hình kiến trúc trên AWS, đánh giá khả năng áp dụng Serverless Architecture và Event-Driven Architecture đối với bài toán xử lý video. | Lựa chọn hướng triển khai Serverless làm nền tảng cho đồ án. |
| **Ngày 4** *(05/06)* | Thiết kế kiến trúc tổng thể | Xác định các thành phần chính của hệ thống, mối liên kết giữa Frontend, Backend, Data Layer và Video Processing Pipeline; xây dựng bản thiết kế kiến trúc đầu tiên. | Hoàn thành bản thiết kế kiến trúc tổng thể phiên bản đầu tiên của hệ thống. |
| **Ngày 5** *(06/06)* | Lựa chọn dịch vụ AWS | Đánh giá và lựa chọn các dịch vụ AWS như Amazon S3, API Gateway, Lambda, Cognito, DynamoDB, CloudFront, SQS và MediaConvert phù hợp với từng thành phần của hệ thống. | Hoàn thiện danh sách dịch vụ AWS dự kiến sử dụng trong đồ án. |
| **Ngày 6** *(07/06)* | Xây dựng lộ trình triển khai | Phân chia hệ thống thành các module chức năng và xây dựng kế hoạch phát triển theo từng giai đoạn để thuận tiện cho việc triển khai trong các tuần tiếp theo. | Hoàn thiện roadmap triển khai dự án theo từng giai đoạn phát triển. |
| **Ngày 7** *(08/06)* | Tổng kết và chuẩn bị triển khai | Rà soát toàn bộ kiến trúc, tổng hợp các tài liệu nghiên cứu và chuẩn bị môi trường cho giai đoạn hiện thực hóa hệ thống. | Hoàn thiện tài liệu nghiên cứu và sẵn sàng bước sang giai đoạn phát triển đồ án. |


### IV. Thực thi kỹ thuật chuyên sâu & Phân tích chi tiết

Sau khi hoàn thành chương trình AWS Academy, nhóm bước sang giai đoạn chuyển tiếp từ việc học tập các dịch vụ riêng lẻ sang xây dựng một hệ thống hoàn chỉnh phục vụ cho đồ án thực tập. Thay vì tiếp tục triển khai các bài Lab độc lập như trước, nhóm tập trung phân tích bài toán, nghiên cứu các mô hình kiến trúc và lựa chọn giải pháp phù hợp với yêu cầu của đề tài.

Qua quá trình thảo luận và đánh giá nhiều phương án khác nhau, nhóm quyết định lựa chọn đề tài **Mini Video-on-Demand Platform using AWS Serverless**. Mục tiêu của hệ thống là xây dựng một nền tảng cho phép quản trị viên tải video lên, hệ thống tự động xử lý, chuyển đổi nhiều chất lượng video khác nhau và phân phối đến người dùng thông qua mạng CDN. Đây là một bài toán phù hợp để vận dụng hầu hết các dịch vụ AWS đã học, đồng thời thể hiện được ưu điểm của mô hình Serverless trong việc tối ưu chi phí và khả năng mở rộng.

Trong tuần này, nhóm chưa tập trung vào việc hiện thực hóa từng chức năng mà ưu tiên xây dựng **bản thiết kế kiến trúc tổng thể phiên bản đầu tiên (Architecture Draft V1)**. Kiến trúc này đóng vai trò định hướng cho toàn bộ quá trình phát triển hệ thống trong các tuần tiếp theo.

<img src="/images/week7/1.png" alt="Initial Serverless Video-on-Demand Architecture" style="max-width:100%; height:auto;" />

Quan sát kiến trúc trên, nhóm chia hệ thống thành nhiều lớp chức năng nhằm giảm sự phụ thuộc giữa các thành phần, đồng thời tận dụng tối đa các dịch vụ managed của AWS.

#### 1. Frontend Layer

Đối với tầng giao diện người dùng, nhóm lựa chọn **React/Next.js** để xây dựng ứng dụng Web do framework này hỗ trợ tốt cho việc phát triển giao diện hiện đại và có khả năng mở rộng trong tương lai.

Frontend dự kiến được triển khai dưới dạng **Static Website** trên **Amazon S3**, kết hợp với **Amazon CloudFront** để phân phối nội dung đến người dùng. Việc sử dụng CloudFront không chỉ giúp giảm độ trễ truy cập mà còn tăng khả năng chịu tải khi số lượng người dùng đồng thời tăng lên.

Đây cũng là mô hình triển khai phổ biến đối với các ứng dụng Serverless khi phần giao diện hoàn toàn tách biệt với Backend.

---

#### 2. API và Authentication Layer

Đối với lớp cung cấp dịch vụ API, nhóm lựa chọn **Amazon API Gateway** làm cổng giao tiếp giữa Frontend và Backend.

Các API dự kiến sẽ được xây dựng theo kiến trúc RESTful, chịu trách nhiệm tiếp nhận yêu cầu từ người dùng và chuyển tiếp đến các hàm xử lý nghiệp vụ trên AWS Lambda.

Song song đó, **Amazon Cognito** được lựa chọn để giải quyết bài toán xác thực và quản lý người dùng. Thay vì tự xây dựng hệ thống đăng nhập, Cognito cung cấp sẵn cơ chế quản lý User Pool, JWT Token và phân quyền, giúp giảm đáng kể thời gian phát triển đồng thời đảm bảo tính bảo mật.

Ở giai đoạn này, nhóm mới dừng lại ở việc xác định vai trò của Cognito trong kiến trúc tổng thể, chưa tiến hành cấu hình chi tiết các User Pool hay Authorization Flow.

---

#### 3. Business Logic Layer

Toàn bộ nghiệp vụ của hệ thống được định hướng triển khai bằng **AWS Lambda**.

Việc sử dụng Lambda giúp loại bỏ hoàn toàn việc quản lý máy chủ, đồng thời chỉ phát sinh chi phí khi có yêu cầu xử lý. Đây là lựa chọn phù hợp đối với hệ thống Video-on-Demand khi lưu lượng truy cập có thể thay đổi theo từng thời điểm.

Trong bản thiết kế ban đầu, nhóm xác định một số nhóm Lambda chính như:

- Xử lý API nghiệp vụ.
- Sinh Presigned URL phục vụ Upload.
- Cập nhật trạng thái xử lý video.
- Xử lý các sự kiện phát sinh từ Pipeline.

Các Lambda sẽ hoạt động độc lập, giao tiếp thông qua API Gateway hoặc EventBridge nhằm giảm sự phụ thuộc giữa các thành phần.

---

#### 4. Data Layer

Đối với tầng lưu trữ dữ liệu, nhóm lựa chọn **Amazon DynamoDB** để lưu metadata của video.

Các thông tin dự kiến lưu trữ bao gồm:

- Video ID.
- Tên video.
- Trạng thái xử lý.
- Đường dẫn lưu trữ.
- Thời gian tạo.
- Danh mục.
- Thông tin người tải lên.

Việc lựa chọn DynamoDB thay vì cơ sở dữ liệu quan hệ xuất phát từ khả năng mở rộng linh hoạt, hiệu năng cao và phù hợp với mô hình Serverless.

Trong giai đoạn nghiên cứu, nhóm cũng đề xuất xây dựng các Global Secondary Index (GSI) nhằm phục vụ việc truy vấn theo trạng thái và danh mục video, tuy nhiên cấu trúc chi tiết sẽ tiếp tục được hoàn thiện trong tuần kế tiếp.

---

#### 5. Video Processing Pipeline

Đây được xem là thành phần quan trọng nhất của toàn bộ hệ thống.

Nhóm định hướng xây dựng Pipeline xử lý video theo mô hình **Event-Driven Architecture** nhằm tách biệt hoàn toàn quá trình Upload và xử lý video.

Luồng xử lý dự kiến như sau:

- Quản trị viên yêu cầu tải video.
- Backend tạo Presigned URL.
- Video được tải trực tiếp lên Amazon S3 Raw Bucket.
- Sau khi Upload hoàn tất, hệ thống phát sinh sự kiện.
- Amazon SQS tiếp nhận yêu cầu xử lý.
- AWS Lambda khởi tạo Job trên AWS Elemental MediaConvert.
- MediaConvert chuyển đổi video sang nhiều độ phân giải khác nhau.
- Kết quả được lưu tại Processed Bucket.
- EventBridge gửi sự kiện hoàn thành.
- Lambda cập nhật trạng thái video trong DynamoDB.

Mô hình bất đồng bộ này giúp Backend không phải chờ quá trình chuyển đổi video hoàn tất, từ đó tăng khả năng mở rộng và cải thiện trải nghiệm người dùng.

---

#### 6. Content Delivery

Sau khi xử lý hoàn tất, video sẽ được phân phối thông qua **Amazon CloudFront**.

CloudFront đóng vai trò CDN giúp:

- Giảm độ trễ truy cập.
- Tăng tốc độ phát video.
- Giảm tải cho S3.
- Tận dụng cơ chế Cache của Edge Location.

Kiến trúc cũng dự kiến hỗ trợ phát video theo chuẩn **HLS Streaming**, cho phép người dùng xem video với nhiều mức chất lượng khác nhau tùy theo tốc độ mạng.

---

#### 7. Định hướng về bảo mật và giám sát

Bên cạnh các thành phần chức năng chính, nhóm cũng bước đầu xác định các dịch vụ hỗ trợ cần thiết nhằm đáp ứng yêu cầu vận hành hệ thống.

Một số dịch vụ được dự kiến sử dụng gồm:

- **AWS IAM** để quản lý quyền truy cập theo nguyên tắc Least Privilege.
- **AWS KMS** để mã hóa dữ liệu lưu trữ.
- **Amazon CloudWatch** phục vụ theo dõi log và giám sát hoạt động của hệ thống.
- **AWS CloudTrail** phục vụ ghi nhận lịch sử thao tác.
- **AWS WAF** nhằm tăng cường khả năng bảo vệ các API công khai.

Do đây mới là giai đoạn nghiên cứu ban đầu, nhóm chưa triển khai cấu hình chi tiết cho các dịch vụ trên mà mới xác định vai trò của từng thành phần trong kiến trúc tổng thể.

### V. Thách thức hạ tầng, Nhật ký xử lý lỗi & Góc nhìn chuyên gia (Infrastructure Challenges, Error Resolution Logs & Expert Perspectives)

Do tuần thứ 7 chủ yếu tập trung vào nghiên cứu và xây dựng kiến trúc ban đầu, nhóm chưa gặp nhiều lỗi triển khai thực tế như ở các tuần thực hành trước. Tuy nhiên, trong quá trình phân tích và thiết kế hệ thống, nhóm đã nhận thấy một số thách thức quan trọng cần được xem xét trước khi bước sang giai đoạn hiện thực hóa.

Thách thức đầu tiên liên quan đến việc lựa chọn kiến trúc phù hợp cho quy trình xử lý video. Video là loại dữ liệu có dung lượng lớn và thời gian xử lý dài, vì vậy nếu sử dụng mô hình xử lý đồng bộ thông qua API Gateway và Lambda thì rất dễ phát sinh tình trạng Timeout, tăng thời gian chờ và ảnh hưởng trực tiếp đến trải nghiệm người dùng. Để giải quyết vấn đề này, nhóm định hướng sử dụng cơ chế xử lý bất đồng bộ thông qua Amazon S3, Amazon SQS, AWS Lambda và AWS Elemental MediaConvert. Phương án này giúp tách biệt quá trình tải video và quá trình chuyển đổi video, đồng thời tăng khả năng chịu lỗi và mở rộng của hệ thống.

Thách thức tiếp theo là vấn đề tải video có dung lượng lớn từ Frontend lên hệ thống. Nếu toàn bộ dữ liệu video phải đi qua Backend hoặc API Gateway thì sẽ làm tăng tải xử lý, chi phí truyền dữ liệu và nguy cơ vượt quá giới hạn kích thước request. Vì vậy, nhóm đề xuất sử dụng Presigned URL để cho phép Frontend tải video trực tiếp lên Amazon S3 Raw Bucket. Backend chỉ chịu trách nhiệm xác thực người dùng, tạo URL tạm thời và lưu metadata cần thiết.

Ngoài ra, việc tổ chức dữ liệu giữa Amazon S3 và Amazon DynamoDB cũng cần được thiết kế cẩn thận. Amazon S3 chịu trách nhiệm lưu trữ file video gốc và video đã xử lý, trong khi DynamoDB lưu metadata, trạng thái xử lý và thông tin phục vụ truy vấn. Nếu không thống nhất cách đặt Video ID, đường dẫn Object Key và trạng thái xử lý ngay từ đầu thì có thể dẫn đến dữ liệu không đồng bộ giữa hai dịch vụ. Nhóm dự kiến sử dụng một Video ID duy nhất làm khóa liên kết giữa DynamoDB, thư mục lưu trữ trên S3 và các Job xử lý trên MediaConvert.

Một vấn đề khác được thảo luận là khả năng xử lý sự kiện lặp lại. Trong kiến trúc hướng sự kiện, một thông điệp từ Amazon SQS hoặc EventBridge có thể được gửi lại khi quá trình xử lý gặp lỗi. Nếu Lambda không được thiết kế theo hướng Idempotent, cùng một video có thể bị tạo nhiều Job MediaConvert hoặc cập nhật trạng thái nhiều lần. Vì vậy, nhóm xác định cần kiểm tra trạng thái hiện tại trong DynamoDB trước khi thực hiện các thao tác quan trọng, đồng thời bổ sung cơ chế Dead-Letter Queue trong giai đoạn triển khai sau.

Về mặt bảo mật, nhóm nhận thấy kiến trúc ban đầu có nhiều thành phần giao tiếp với nhau và mỗi thành phần cần được cấp quyền phù hợp. Việc gán quyền quá rộng có thể tạo ra rủi ro truy cập trái phép, trong khi quyền quá hạn chế lại có thể khiến hệ thống không hoạt động. Giải pháp được định hướng là xây dựng IAM Role riêng cho từng Lambda, áp dụng nguyên tắc Least Privilege và giới hạn quyền truy cập theo Bucket, Table, Queue hoặc MediaConvert Job cụ thể.

Bên cạnh đó, việc phân phối video thông qua CloudFront cũng cần đảm bảo rằng S3 Processed Bucket không bị công khai trực tiếp. Nhóm dự kiến giữ toàn bộ Bucket ở trạng thái Private và chỉ cho phép CloudFront truy cập nội dung thông qua cơ chế Origin Access Control. Điều này giúp hạn chế người dùng truy cập trực tiếp vào Object URL của S3 và tăng khả năng kiểm soát luồng phân phối video.

Từ góc nhìn chuyên môn, nhóm nhận thấy rằng một kiến trúc Cloud tốt không chỉ cần đáp ứng chức năng mà còn phải cân bằng giữa hiệu năng, khả năng mở rộng, bảo mật, độ tin cậy và chi phí. Bản kiến trúc hiện tại mới là phiên bản đầu tiên nên một số thành phần như AWS WAF, KMS, SNS, SES, X-Ray và AWS Config vẫn đang được xem xét về mức độ cần thiết. Trong các tuần tiếp theo, nhóm sẽ ưu tiên triển khai các thành phần cốt lõi trước, sau đó mới bổ sung các dịch vụ hỗ trợ dựa trên nhu cầu thực tế và giới hạn ngân sách của đồ án.

### VI. Đánh giá và Chiêm nghiệm chuyên môn (Professional Reflections)

Tuần thứ 7 không tập trung vào việc triển khai kỹ thuật cụ thể mà đóng vai trò là giai đoạn chuyển tiếp từ quá trình học tập sang quá trình xây dựng một hệ thống thực tế. Mặc dù khối lượng lập trình chưa nhiều, đây lại là một trong những tuần quan trọng nhất vì các quyết định về kiến trúc sẽ ảnh hưởng trực tiếp đến toàn bộ quá trình phát triển của đồ án trong các tuần tiếp theo.

Thông qua quá trình tổng hợp kiến thức và phân tích yêu cầu nghiệp vụ, nhóm nhận thấy rằng việc lựa chọn kiến trúc phù hợp quan trọng không kém việc triển khai chức năng. Một kiến trúc được thiết kế rõ ràng sẽ giúp các thành viên có chung định hướng phát triển, hạn chế việc phải thay đổi quá nhiều khi dự án bước vào giai đoạn hiện thực hóa.

Bên cạnh đó, nhóm cũng có cơ hội nhìn nhận lại mối liên hệ giữa các dịch vụ AWS đã học trong suốt chương trình AWS Academy. Trước đây, mỗi dịch vụ được tiếp cận thông qua các bài Lab riêng biệt; tuy nhiên, khi xây dựng một hệ thống hoàn chỉnh, nhóm hiểu rõ hơn cách các dịch vụ như Amazon API Gateway, AWS Lambda, Amazon Cognito, Amazon S3, Amazon DynamoDB, Amazon SQS, Amazon CloudFront và AWS Elemental MediaConvert phối hợp với nhau để tạo thành một quy trình xử lý thống nhất.

Ngoài yếu tố kỹ thuật, tuần làm việc này cũng giúp nhóm nâng cao kỹ năng phân tích yêu cầu, trao đổi ý tưởng và đưa ra quyết định thiết kế dựa trên các tiêu chí về khả năng mở rộng, hiệu năng, tính bảo mật và chi phí vận hành. Đây là những kỹ năng quan trọng đối với quá trình phát triển các hệ thống Cloud trong thực tế.

Qua tuần làm việc, nhóm nhận thấy rằng việc đầu tư thời gian cho giai đoạn nghiên cứu và thiết kế kiến trúc sẽ tạo nền tảng vững chắc cho quá trình triển khai sau này, đồng thời giúp giảm thiểu các rủi ro phát sinh khi hệ thống ngày càng mở rộng.

---

### VII. Kế hoạch chiến lược & Lộ trình tối ưu cho tuần tới (Strategic Planning & Optimization Roadmap for Next Week)

Sau khi hoàn thành bản thiết kế kiến trúc tổng thể phiên bản đầu tiên, nhóm sẽ bước sang giai đoạn hoàn thiện thiết kế kỹ thuật và chuẩn bị triển khai các thành phần đầu tiên của hệ thống.

Trong tuần tiếp theo, nhóm dự kiến sẽ rà soát và hiệu chỉnh kiến trúc dựa trên các góp ý từ giảng viên hướng dẫn cũng như kết quả thảo luận nội bộ nhằm đảm bảo tính khả thi trước khi bắt đầu phát triển. Đồng thời, nhóm sẽ tiến hành thiết kế chi tiết hơn đối với các thành phần quan trọng như mô hình dữ liệu trên Amazon DynamoDB, cấu trúc Amazon S3 Bucket, quy trình xác thực người dùng bằng Amazon Cognito và các API nghiệp vụ được triển khai thông qua Amazon API Gateway và AWS Lambda.

Bên cạnh đó, nhóm cũng sẽ chuẩn bị môi trường phát triển, xây dựng cấu trúc dự án, thiết lập kho mã nguồn (Repository), phân chia nhiệm vụ giữa các thành viên và xây dựng lộ trình triển khai theo từng module chức năng. Đây sẽ là bước chuẩn bị quan trọng trước khi bắt đầu hiện thực hóa hệ thống trong các tuần kế tiếp.

Mục tiêu của tuần tiếp theo không chỉ là hoàn thiện bản thiết kế kỹ thuật mà còn tạo ra nền tảng phát triển thống nhất, giúp quá trình triển khai các chức năng như Authentication, Video Upload, Video Processing Pipeline và Video Streaming được thực hiện một cách hiệu quả, hạn chế thay đổi lớn trong suốt vòng đời của dự án.