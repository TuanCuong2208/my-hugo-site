---
title: "Worklog Tuần 12"
date: 2026-07-07
weight: 12
chapter: false
pre: "<b> 1.12. </b> "
---

# I. Tóm tắt tổng quan

Tuần cuối của kỳ thực tập được dành cho giai đoạn kiểm thử tổng thể, giám sát hệ thống và tối ưu hiệu năng của nền tảng Serverless Video-on-Demand trên AWS. Sau khi toàn bộ các thành phần chức năng đã được tích hợp hoàn chỉnh ở tuần trước, nhóm tập trung đánh giá tính ổn định của hệ thống trong điều kiện vận hành thực tế, đồng thời rà soát lại toàn bộ kiến trúc nhằm bảo đảm nền tảng đáp ứng các yêu cầu về hiệu năng, khả năng mở rộng và bảo mật.

Trong tuần này, Amazon CloudWatch được sử dụng làm nền tảng giám sát trung tâm để thu thập log, theo dõi các chỉ số vận hành và phân tích hoạt động của các dịch vụ như Amazon API Gateway, AWS Lambda, AWS Step Functions, AWS Elemental MediaConvert và Amazon CloudFront. Thông qua các dữ liệu giám sát, nhóm đánh giá hiệu quả hoạt động của từng thành phần cũng như xác định các điểm cần tối ưu trong quy trình xử lý video.

Bên cạnh hoạt động giám sát, nhóm tiến hành rà soát cấu hình IAM nhằm kiểm tra quyền truy cập của từng dịch vụ theo nguyên tắc **Least Privilege**, đồng thời đánh giá các chính sách bảo mật đã triển khai trên AWS WAF và Amazon Cognito. Việc kiểm tra này giúp hạn chế các quyền không cần thiết, giảm thiểu rủi ro bảo mật và nâng cao mức độ an toàn của toàn bộ hệ thống.

Ngoài ra, nhóm thực hiện kiểm thử End-to-End đối với toàn bộ quy trình nghiệp vụ, từ xác thực người dùng, tải video, xử lý bất đồng bộ, cập nhật trạng thái trong Amazon DynamoDB đến phát video thông qua Amazon CloudFront. Các kịch bản kiểm thử được xây dựng nhằm đánh giá khả năng phối hợp giữa các dịch vụ AWS trong nhiều tình huống khác nhau.

Kết thúc tuần làm việc, nhóm hoàn thiện phiên bản MVP của hệ thống, tổng hợp kết quả triển khai, chuẩn bị tài liệu kỹ thuật và xây dựng nội dung trình diễn phục vụ báo cáo thực tập cũng như nghiệm thu đồ án.

# II. Mục tiêu chiến lược trong tuần

Mục tiêu chính của tuần cuối là đánh giá toàn diện chất lượng hệ thống sau khi hoàn thành toàn bộ các chức năng cốt lõi, đồng thời tối ưu các cấu hình trước khi kết thúc quá trình thực tập.

Các mục tiêu được đặt ra bao gồm:

- Thiết lập hệ thống giám sát bằng Amazon CloudWatch.
- Thu thập và phân tích log từ Amazon API Gateway, AWS Lambda và AWS Step Functions.
- Theo dõi tiến trình xử lý của AWS Elemental MediaConvert.
- Kiểm thử toàn bộ quy trình nghiệp vụ theo mô hình End-to-End.
- Rà soát quyền truy cập IAM theo nguyên tắc Least Privilege.
- Đánh giá hiệu quả của AWS WAF và Amazon Cognito.
- Tối ưu hiệu năng và chi phí vận hành của hệ thống.
- Hoàn thiện phiên bản MVP và chuẩn bị tài liệu nghiệm thu.

Thông qua các mục tiêu trên, nhóm hướng đến việc bảo đảm hệ thống hoạt động ổn định, an toàn và sẵn sàng cho quá trình trình diễn cũng như đánh giá kết quả thực tập.

# III. Nhật ký hoạt động & Lộ trình phân bổ chi tiết (Từ 07/07/2026 đến 13/07/2026)

| Thời gian | Danh mục hoạt động | Chi tiết các tác vụ thực hiện chuyên sâu | Kết quả/Minh chứng đạt được |
| :--- | :--- | :--- | :--- |
| **Ngày 1** *(07/07)* | System Monitoring | Cấu hình Amazon CloudWatch để thu thập log và chỉ số vận hành từ các dịch vụ AWS trong hệ thống. | Hoàn thành hệ thống giám sát tập trung. |
| **Ngày 2** *(08/07)* | Performance Analysis | Phân tích log của Amazon API Gateway, AWS Lambda và AWS Step Functions nhằm đánh giá hiệu năng xử lý. | Xác định các điểm cần tối ưu trong quy trình vận hành. |
| **Ngày 3** *(09/07)* | Security Review | Rà soát IAM Policy, đánh giá cấu hình Amazon Cognito và AWS WAF theo nguyên tắc Least Privilege. | Hoàn thiện cấu hình bảo mật của hệ thống. |
| **Ngày 4** *(10/07)* | End-to-End Testing | Kiểm thử toàn bộ quy trình từ đăng nhập, Upload Video, xử lý bất đồng bộ đến phát video trực tuyến. | Xác nhận toàn bộ quy trình hoạt động ổn định. |
| **Ngày 5** *(11/07)* | System Optimization | Tối ưu cấu hình CloudFront Cache, Lambda và Step Functions dựa trên kết quả giám sát. | Hiệu năng hệ thống được cải thiện. |
| **Ngày 6** *(12/07)* | Documentation | Hoàn thiện tài liệu kỹ thuật, cập nhật sơ đồ kiến trúc và tổng hợp kết quả triển khai. | Bộ tài liệu kỹ thuật được hoàn chỉnh. |
| **Ngày 7** *(13/07)* | Final Review | Tổng kết dự án, chuẩn bị nội dung Demo và đánh giá phiên bản MVP trước khi nghiệm thu. | Hoàn thành toàn bộ mục tiêu của kỳ thực tập. |

# IV. Thực thi kỹ thuật chuyên sâu & Phân tích chi tiết

Trong tuần cuối của kỳ thực tập, nhóm tập trung vào việc đánh giá tổng thể hệ thống sau khi toàn bộ các chức năng cốt lõi đã được triển khai hoàn chỉnh. Khác với các tuần trước chủ yếu tập trung vào phát triển và tích hợp từng thành phần, tuần này hướng đến việc kiểm chứng tính ổn định, khả năng mở rộng, mức độ bảo mật và hiệu năng vận hành của toàn bộ nền tảng Serverless Video-on-Demand trên AWS. Các hoạt động được thực hiện bao gồm giám sát hệ thống, phân tích log, kiểm thử toàn diện, rà soát cấu hình bảo mật và tối ưu tài nguyên nhằm chuẩn bị cho giai đoạn nghiệm thu và trình diễn sản phẩm.

Amazon CloudWatch được sử dụng làm trung tâm giám sát cho toàn bộ hệ thống. Nhóm cấu hình thu thập log và các chỉ số vận hành từ Amazon API Gateway, AWS Lambda, AWS Step Functions, AWS Elemental MediaConvert và Amazon CloudFront. Việc tập trung dữ liệu giám sát trên một nền tảng giúp quá trình theo dõi hoạt động của hệ thống trở nên thuận tiện hơn, đồng thời hỗ trợ nhanh chóng phát hiện các lỗi phát sinh hoặc các thành phần có dấu hiệu hoạt động không ổn định.

Đối với AWS Lambda, nhóm theo dõi các chỉ số như số lần thực thi, thời gian xử lý trung bình, tỷ lệ lỗi và số lượng lời gọi đồng thời nhằm đánh giá khả năng đáp ứng của các hàm Serverless khi hệ thống tiếp nhận nhiều yêu cầu Upload Video. Thông qua các dữ liệu thu thập được, nhóm xác nhận thời gian xử lý của Lambda luôn nằm trong giới hạn cho phép và không xuất hiện hiện tượng quá tải trong các kịch bản kiểm thử của đồ án.

Bên cạnh Lambda, nhóm tiếp tục theo dõi tiến trình thực thi của AWS Step Functions để đánh giá toàn bộ Pipeline xử lý video. Mỗi Workflow đều được kiểm tra về trạng thái thực thi, thời gian hoàn thành và khả năng xử lý lỗi khi một bước trong quy trình gặp sự cố. Việc quan sát trực tiếp từng trạng thái giúp nhóm dễ dàng xác định nguyên nhân nếu Pipeline bị gián đoạn, đồng thời nâng cao khả năng bảo trì của hệ thống trong tương lai.

Đối với AWS Elemental MediaConvert, nhóm theo dõi thời gian chuyển mã của nhiều tệp video có dung lượng khác nhau nhằm đánh giá hiệu năng của dịch vụ. Kết quả kiểm thử cho thấy thời gian xử lý phụ thuộc chủ yếu vào kích thước và độ phân giải của video đầu vào, trong khi quy trình xử lý vẫn được thực hiện ổn định nhờ cơ chế điều phối của AWS Step Functions. Sau khi hoàn tất chuyển mã, các tệp HLS được lưu vào Amazon S3 Processed Media Bucket và sẵn sàng phục vụ người dùng thông qua Amazon CloudFront.

Song song với việc giám sát hệ thống, nhóm tiến hành rà soát lại toàn bộ cấu hình IAM theo nguyên tắc **Least Privilege**. Quyền truy cập của từng dịch vụ được kiểm tra nhằm bảo đảm mỗi thành phần chỉ được phép thực hiện đúng các thao tác cần thiết. Các IAM Role của AWS Lambda, AWS Step Functions và AWS Elemental MediaConvert được đối chiếu với kiến trúc triển khai để loại bỏ các quyền không còn sử dụng, qua đó giảm thiểu nguy cơ phát sinh các lỗ hổng bảo mật.

Nhóm cũng đánh giá hiệu quả của AWS WAF sau quá trình tích hợp với Amazon CloudFront. Các Rule đã triển khai được kiểm tra thông qua nhiều kịch bản truy cập khác nhau nhằm xác nhận rằng các yêu cầu hợp lệ vẫn được xử lý bình thường, trong khi các lưu lượng bất thường được ghi nhận và kiểm soát theo đúng chính sách bảo mật đã thiết lập. Đồng thời, cơ chế xác thực của Amazon Cognito tiếp tục được kiểm thử nhằm bảo đảm chỉ những người dùng đã đăng nhập mới có thể truy cập các API được bảo vệ.

Một nội dung quan trọng khác trong tuần là kiểm thử End-to-End toàn bộ hệ thống. Nhóm xây dựng các kịch bản mô phỏng người dùng thực hiện đăng nhập, tải video lên Amazon S3 Raw Upload Bucket thông qua Presigned URL, theo dõi trạng thái xử lý trong Amazon DynamoDB và phát video sau khi quá trình chuyển mã hoàn tất. Tất cả các bước đều được thực hiện liên tục nhiều lần nhằm đánh giá mức độ ổn định của toàn bộ quy trình nghiệp vụ.

Sau khi hoàn thành các hoạt động kiểm thử, nhóm tiến hành tối ưu một số cấu hình của hệ thống. Amazon CloudFront được điều chỉnh chính sách Cache nhằm tăng tỷ lệ phục vụ nội dung từ Edge Location đối với các video đã được truy cập nhiều lần. Đồng thời, nhóm rà soát cấu hình của AWS Lambda và AWS Step Functions để loại bỏ các thiết lập chưa cần thiết, góp phần giảm chi phí vận hành mà vẫn duy trì hiệu năng của hệ thống.

Đến cuối tuần, nhóm hoàn tất việc kiểm thử, giám sát và tối ưu nền tảng Serverless Video-on-Demand. Phiên bản MVP đã đáp ứng đầy đủ các chức năng đặt ra ban đầu, bao gồm xác thực người dùng, tải video, xử lý bất đồng bộ, lưu trữ metadata và phát video trực tuyến thông qua hạ tầng AWS. Toàn bộ tài liệu kỹ thuật, sơ đồ kiến trúc và kết quả kiểm thử cũng được hoàn thiện nhằm phục vụ quá trình báo cáo và nghiệm thu đồ án.

# V. Thách thức hạ tầng, Nhật ký xử lý lỗi & Góc nhìn chuyên gia

Trong quá trình theo dõi hệ thống bằng Amazon CloudWatch, nhóm nhận thấy việc phân tích log từ nhiều dịch vụ khác nhau đòi hỏi phải hiểu rõ mối quan hệ giữa các thành phần trong kiến trúc Serverless. Do mỗi dịch vụ ghi nhận nhật ký theo định dạng riêng, nhóm đã xây dựng quy trình đối chiếu log giữa Amazon API Gateway, AWS Lambda và AWS Step Functions để xác định nhanh nguyên nhân khi một yêu cầu xử lý gặp lỗi.

Một khó khăn khác xuất hiện khi đánh giá quyền truy cập IAM. Một số IAM Policy ban đầu được cấp quyền rộng hơn mức cần thiết để thuận tiện trong quá trình phát triển. Trước khi hoàn thiện hệ thống, nhóm tiến hành rà soát và loại bỏ các quyền dư thừa nhằm tuân thủ nguyên tắc Least Privilege. Việc tối ưu quyền truy cập không chỉ nâng cao mức độ an toàn mà còn giúp kiến trúc phù hợp hơn với các khuyến nghị của AWS Well-Architected Framework.

Trong quá trình kiểm thử hiệu năng, nhóm cũng quan sát thấy Amazon CloudFront cải thiện đáng kể tốc độ truy cập đối với các video đã được lưu trong bộ nhớ đệm tại Edge Location. Điều này cho thấy việc sử dụng Content Delivery Network là giải pháp phù hợp đối với các hệ thống phân phối nội dung đa phương tiện có nhiều người dùng truy cập đồng thời.

Qua toàn bộ quá trình triển khai, nhóm nhận thấy rằng việc kết hợp các dịch vụ Managed Services của AWS giúp giảm đáng kể khối lượng công việc liên quan đến quản trị hạ tầng. Điều này cho phép nhóm tập trung vào thiết kế kiến trúc, tối ưu quy trình nghiệp vụ và nâng cao chất lượng của ứng dụng thay vì dành nhiều thời gian cho việc vận hành máy chủ.

# VI. Đánh giá và Chiêm nghiệm chuyên môn

Tuần cuối cùng đánh dấu việc hoàn thiện toàn bộ nền tảng Serverless Video-on-Demand theo đúng mục tiêu đề ra ban đầu. Thông qua quá trình kiểm thử, giám sát và tối ưu hệ thống, nhóm có cơ hội đánh giá toàn diện kiến trúc đã xây dựng cũng như hiểu rõ hơn về cách các dịch vụ AWS phối hợp để tạo thành một ứng dụng Cloud-Native hoàn chỉnh.

Việc sử dụng Amazon CloudWatch giúp nhóm nhận thức rõ vai trò của khả năng quan sát (Observability) trong quá trình vận hành hệ thống thực tế. Thay vì chỉ tập trung phát triển chức năng, một hệ thống triển khai trên môi trường Cloud còn cần được giám sát liên tục để phát hiện sớm các vấn đề về hiệu năng, bảo mật và độ tin cậy.

Thông qua việc rà soát IAM, đánh giá AWS WAF và kiểm thử toàn bộ Pipeline xử lý video, nhóm hiểu rõ hơn tầm quan trọng của việc cân bằng giữa hiệu năng, khả năng mở rộng và bảo mật trong quá trình thiết kế kiến trúc Serverless. Những kinh nghiệm này là nền tảng quan trọng để nhóm tiếp tục nghiên cứu và phát triển các hệ thống điện toán đám mây trong tương lai.

Nhìn chung, toàn bộ mục tiêu của kỳ thực tập đã được hoàn thành. Phiên bản MVP đáp ứng đầy đủ các yêu cầu chức năng, có kiến trúc rõ ràng, sử dụng hiệu quả các dịch vụ Managed Services của AWS và thể hiện được tính khả thi của mô hình Serverless trong việc xây dựng nền tảng Video-on-Demand.

# VII. Tổng kết kỳ thực tập

Kết thúc kỳ thực tập, nhóm đã xây dựng thành công một nền tảng **Serverless Video-on-Demand Platform on AWS** với đầy đủ các chức năng cốt lõi, bao gồm xác thực người dùng bằng Amazon Cognito, tải video trực tiếp lên Amazon S3 thông qua Presigned URL, xử lý video bất đồng bộ bằng Event-Driven Pipeline sử dụng Amazon EventBridge, Amazon SQS, EventBridge Pipes, AWS Step Functions và AWS Elemental MediaConvert, lưu trữ metadata trên Amazon DynamoDB, đồng thời phân phối nội dung thông qua Amazon CloudFront.

Quá trình thực hiện đồ án giúp nhóm không chỉ củng cố kiến thức về kiến trúc Serverless mà còn tích lũy kinh nghiệm thực tế trong việc thiết kế, triển khai, giám sát và tối ưu một hệ thống Cloud-Native trên nền tảng AWS. Đây là nền tảng quan trọng để nhóm tiếp tục nghiên cứu các mô hình kiến trúc hiện đại và ứng dụng điện toán đám mây trong các dự án thực tế sau này.