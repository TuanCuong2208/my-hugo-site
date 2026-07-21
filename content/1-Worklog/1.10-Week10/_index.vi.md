---
title: "Worklog Tuần 10"
date: 2026-06-23
weight: 10
chapter: false
pre: "<b> 1.10. </b> "
---

## I. Tóm tắt tổng quan

Sau khi hoàn thiện hạ tầng Backend phục vụ chức năng tải video lên Amazon S3 trong tuần trước, nhóm tiếp tục triển khai giai đoạn quan trọng nhất của hệ thống là **xây dựng quy trình xử lý video tự động theo kiến trúc Event-Driven Serverless**. Mục tiêu của tuần này là đảm bảo mỗi video sau khi được tải lên sẽ tự động trải qua toàn bộ quá trình xử lý, chuyển mã và lưu trữ mà không cần bất kỳ thao tác thủ công nào từ phía người quản trị.

Để hiện thực hóa mục tiêu này, nhóm triển khai chuỗi dịch vụ bao gồm Amazon EventBridge, Amazon SQS, Amazon EventBridge Pipes, AWS Step Functions và AWS Elemental MediaConvert. Kiến trúc này giúp tách biệt hoàn toàn quá trình tiếp nhận sự kiện, điều phối luồng xử lý và thực hiện chuyển mã video, từ đó nâng cao khả năng mở rộng, tăng tính ổn định cũng như giảm sự phụ thuộc giữa các thành phần trong hệ thống.

Song song với việc triển khai Pipeline xử lý video, nhóm tiếp tục hoàn thiện cơ chế đồng bộ dữ liệu trên Amazon DynamoDB nhằm cập nhật trạng thái xử lý của từng video theo từng giai đoạn như **Uploaded**, **Queued**, **Processing**, **Completed** hoặc **Failed**. Điều này tạo tiền đề để giao diện người dùng có thể theo dõi tiến trình xử lý theo thời gian thực ở các giai đoạn tiếp theo của dự án.

Ngoài ra, nhóm cũng cấu hình AWS Elemental MediaConvert để chuyển đổi video sang định dạng **HTTP Live Streaming (HLS)** và lưu kết quả vào Amazon S3 Processed Media Bucket. Các tệp đầu ra được tổ chức theo cấu trúc thư mục thống nhất nhằm phục vụ việc phân phối nội dung sau này thông qua Amazon CloudFront.

Kết thúc tuần làm việc, nhóm đã xây dựng thành công Pipeline xử lý video hoàn toàn tự động theo kiến trúc Serverless, đánh dấu việc hoàn thiện tầng xử lý nghiệp vụ cốt lõi của nền tảng Video-on-Demand trên AWS.

## II. Mục tiêu chiến lược trong tuần

Sau khi hoàn thiện chức năng Upload Video, mục tiêu của tuần thứ 10 là triển khai kiến trúc xử lý video bất đồng bộ dựa trên các dịch vụ Serverless của AWS.

Các mục tiêu chính bao gồm:

- Xây dựng Event-Driven Video Processing Pipeline.
- Cấu hình Amazon EventBridge để tiếp nhận sự kiện từ Amazon S3.
- Triển khai Amazon SQS nhằm đệm và quản lý các yêu cầu xử lý video.
- Sử dụng Amazon EventBridge Pipes để chuyển tiếp thông điệp từ SQS đến AWS Step Functions.
- Thiết kế Workflow xử lý video bằng AWS Step Functions.
- Tích hợp AWS Elemental MediaConvert để chuyển mã video sang định dạng HLS.
- Đồng bộ trạng thái xử lý video với Amazon DynamoDB.
- Kiểm thử toàn bộ Pipeline từ Upload Video đến khi hoàn thành quá trình chuyển mã.

Thông qua các mục tiêu trên, nhóm hướng đến việc xây dựng một hệ thống xử lý video có khả năng mở rộng cao, hoạt động hoàn toàn tự động và đáp ứng đúng kiến trúc Serverless được đề xuất trong đồ án.

## III. Nhật ký hoạt động & Lộ trình phân bổ chi tiết (Từ 23/06/2026 đến 29/06/2026)

| Thời gian | Danh mục hoạt động | Chi tiết các tác vụ thực hiện chuyên sâu | Kết quả/Minh chứng đạt được |
| :--- | :--- | :--- | :--- |
| **Ngày 1** *(23/06)* | Thiết kế kiến trúc xử lý | Phân tích luồng xử lý video theo mô hình Event-Driven, xác định vai trò của Amazon EventBridge, Amazon SQS, EventBridge Pipes và AWS Step Functions. | Hoàn thiện thiết kế Video Processing Pipeline theo kiến trúc Serverless. |
| **Ngày 2** *(24/06)* | Triển khai Event Layer | Cấu hình Amazon EventBridge tiếp nhận sự kiện Object Created từ Amazon S3 Raw Upload Bucket và gửi thông điệp đến Amazon SQS. | Sự kiện Upload Video được ghi nhận và chuyển vào hàng đợi thành công. |
| **Ngày 3** *(25/06)* | Workflow Orchestration | Cấu hình Amazon EventBridge Pipes đọc dữ liệu từ Amazon SQS và kích hoạt AWS Step Functions để điều phối quy trình xử lý video. | Hoàn thành cơ chế điều phối Pipeline bất đồng bộ. |
| **Ngày 4** *(26/06)* | Video Transcoding | Tích hợp AWS Elemental MediaConvert trong Step Functions, xây dựng cấu hình chuyển mã và xuất video theo chuẩn HLS. | Video được chuyển mã thành công và lưu vào Amazon S3 Processed Media Bucket. |
| **Ngày 5** *(27/06)* | Metadata Management | Đồng bộ trạng thái xử lý video với Amazon DynamoDB, cập nhật các trạng thái Queued, Processing, Completed và Failed. | Dữ liệu trạng thái phản ánh chính xác tiến trình xử lý của từng video. |
| **Ngày 6** *(28/06)* | Kiểm thử Pipeline | Thực hiện nhiều kịch bản Upload Video, theo dõi EventBridge, SQS, Step Functions và MediaConvert để đánh giá toàn bộ luồng xử lý. | Pipeline hoạt động ổn định trong các kịch bản kiểm thử khác nhau. |
| **Ngày 7** *(29/06)* | Đánh giá & Tối ưu | Rà soát kiến trúc xử lý, tối ưu Workflow, đánh giá khả năng mở rộng và chuẩn bị tích hợp tầng phân phối nội dung trong giai đoạn tiếp theo. | Hoàn thiện Video Processing Pipeline theo đúng kiến trúc thiết kế của hệ thống. |

## IV. Thực thi kỹ thuật chuyên sâu & Phân tích chi tiết

Sau khi hoàn thiện chức năng tải video trực tiếp lên Amazon S3 bằng Presigned URL ở tuần trước, nhóm chuyển sang triển khai tầng xử lý video tự động theo kiến trúc Event-Driven. Mục tiêu của giai đoạn này là xây dựng một Pipeline có khả năng tự động tiếp nhận sự kiện, điều phối quy trình xử lý và chuyển mã video mà không cần bất kỳ thao tác thủ công nào. Kiến trúc được thiết kế dựa trên việc kết hợp các dịch vụ Amazon EventBridge, Amazon SQS, Amazon EventBridge Pipes, AWS Step Functions và AWS Elemental MediaConvert nhằm đảm bảo tính mở rộng, khả năng chịu lỗi và tính độc lập giữa các thành phần.

Thành phần đầu tiên được triển khai là Amazon EventBridge. Sau khi người dùng tải video thành công lên Amazon S3 Raw Upload Bucket, sự kiện **Object Created** được phát sinh và tự động gửi đến EventBridge. Thay vì kích hoạt trực tiếp dịch vụ xử lý, EventBridge đóng vai trò tiếp nhận và định tuyến sự kiện, giúp tách biệt tầng tiếp nhận dữ liệu với tầng xử lý nghiệp vụ phía sau.

Để tăng khả năng chịu tải và tránh mất dữ liệu khi có nhiều video được tải lên cùng thời điểm, nhóm sử dụng Amazon SQS làm hàng đợi trung gian. Mỗi thông điệp chứa thông tin về video mới được đưa vào hàng đợi và chờ xử lý theo cơ chế bất đồng bộ. Việc sử dụng SQS giúp hệ thống tránh được tình trạng quá tải khi số lượng yêu cầu tăng đột biến, đồng thời bảo đảm các thông điệp được xử lý theo đúng trình tự.

Sau khi thông điệp xuất hiện trong Amazon SQS, Amazon EventBridge Pipes được cấu hình để tự động đọc dữ liệu từ hàng đợi và chuyển tiếp đến AWS Step Functions. So với việc tự xây dựng một dịch vụ trung gian để đọc SQS, EventBridge Pipes giúp giảm đáng kể lượng mã nguồn cần phát triển, đồng thời đơn giản hóa việc tích hợp giữa các dịch vụ trong hệ sinh thái AWS.

AWS Step Functions được sử dụng làm trung tâm điều phối toàn bộ quy trình xử lý video. Nhóm thiết kế State Machine để quản lý từng bước của Pipeline, từ tiếp nhận thông tin video, kiểm tra dữ liệu đầu vào, khởi tạo tác vụ chuyển mã cho đến cập nhật trạng thái xử lý sau khi MediaConvert hoàn tất. Việc sử dụng Step Functions giúp toàn bộ Workflow được mô hình hóa rõ ràng, dễ theo dõi và thuận tiện cho việc mở rộng trong tương lai.

Trong bước chuyển mã, AWS Elemental MediaConvert được cấu hình để tiếp nhận video từ Amazon S3 Raw Upload Bucket và xuất kết quả sang Amazon S3 Processed Media Bucket. Nhóm lựa chọn chuẩn **HTTP Live Streaming (HLS)** làm định dạng đầu ra nhằm tối ưu cho việc phát video trực tuyến trên nhiều nền tảng khác nhau. Sau khi hoàn thành chuyển mã, MediaConvert tạo ra Playlist (.m3u8) cùng các tệp phân đoạn (.ts), phục vụ cho quá trình phân phối nội dung ở các giai đoạn tiếp theo.

Song song với quá trình chuyển mã, hệ thống liên tục đồng bộ thông tin xử lý lên Amazon DynamoDB. Mỗi video được quản lý thông qua các trạng thái như **Uploaded**, **Queued**, **Processing**, **Completed** và **Failed**. Việc lưu trữ trạng thái theo thời gian thực giúp các thành phần khác của hệ thống có thể dễ dàng truy vấn tiến độ xử lý mà không cần giao tiếp trực tiếp với MediaConvert.

Sau khi hoàn thành từng thành phần, nhóm tiến hành kiểm thử toàn bộ Pipeline bằng nhiều kịch bản khác nhau. Các trường hợp như tải đồng thời nhiều video, tải các tệp có dung lượng lớn hoặc thử nghiệm với nhiều định dạng đầu vào đều được thực hiện nhằm đánh giá khả năng hoạt động của hệ thống. Kết quả cho thấy Pipeline hoạt động ổn định, các sự kiện được xử lý theo đúng thứ tự và dữ liệu được đồng bộ chính xác giữa các dịch vụ.

Đến cuối tuần, nhóm đã hoàn thiện kiến trúc xử lý video bất đồng bộ theo đúng định hướng Serverless. Toàn bộ quy trình từ khi người dùng tải video lên Amazon S3 cho đến khi video được chuyển mã và lưu vào vùng lưu trữ đầu ra đều diễn ra hoàn toàn tự động, tạo nền tảng quan trọng cho việc triển khai tầng phân phối nội dung và giao diện người dùng trong giai đoạn tiếp theo.

## V. Thách thức hạ tầng, Nhật ký xử lý lỗi & Góc nhìn chuyên gia

Trong quá trình triển khai Pipeline xử lý video, nhóm gặp khó khăn đầu tiên khi cấu hình quyền truy cập giữa AWS Step Functions và AWS Elemental MediaConvert. Do IAM Role chưa được cấp đầy đủ quyền truy cập vào Amazon S3 và MediaConvert nên một số Workflow ban đầu không thể khởi tạo tác vụ chuyển mã. Sau khi rà soát lại IAM Policy và Principle of Least Privilege, nhóm đã điều chỉnh quyền phù hợp để bảo đảm các dịch vụ chỉ được phép truy cập đúng tài nguyên cần thiết.

Một vấn đề khác xuất hiện trong quá trình truyền thông điệp giữa Amazon EventBridge và Amazon SQS. Ban đầu một số sự kiện chưa được chuyển tiếp đúng do cấu hình Event Pattern chưa phù hợp với sự kiện Object Created của Amazon S3. Sau khi kiểm tra lại Rule và thử nghiệm với nhiều tình huống khác nhau, nhóm đã hiệu chỉnh bộ lọc sự kiện để bảo đảm mọi video tải lên đều được đưa vào hàng đợi xử lý.

Trong quá trình tích hợp AWS Step Functions, nhóm nhận thấy việc chia Workflow thành nhiều trạng thái độc lập giúp việc theo dõi tiến trình xử lý trở nên trực quan hơn rất nhiều. Khi xảy ra lỗi tại bất kỳ bước nào, nhóm có thể nhanh chóng xác định vị trí phát sinh sự cố thay vì phải kiểm tra toàn bộ Pipeline như khi sử dụng một tiến trình xử lý đơn lẻ.

Ngoài ra, nhóm cũng đánh giá vai trò của Amazon SQS trong việc tăng tính ổn định của hệ thống. Việc bổ sung hàng đợi giúp các dịch vụ phía sau không bị ảnh hưởng khi lưu lượng Upload tăng cao, đồng thời tạo tiền đề để mở rộng quy mô xử lý trong tương lai mà không cần thay đổi kiến trúc tổng thể.

## VI. Đánh giá và Chiêm nghiệm chuyên môn

Tuần thứ 10 giúp nhóm hiểu rõ hơn về cách xây dựng một hệ thống xử lý bất đồng bộ trên nền tảng điện toán đám mây. Thay vì xây dựng các luồng xử lý đồng bộ như trong nhiều ứng dụng truyền thống, việc sử dụng EventBridge, Amazon SQS và AWS Step Functions giúp toàn bộ Pipeline trở nên linh hoạt, dễ mở rộng và có khả năng phục hồi cao hơn khi xảy ra lỗi.

Quá trình triển khai cũng giúp nhóm tiếp cận sâu hơn với các mô hình Event-Driven Architecture và Workflow Orchestration. Việc tách biệt rõ ràng giữa tầng tiếp nhận sự kiện, tầng điều phối và tầng xử lý nghiệp vụ giúp kiến trúc hệ thống trở nên mạch lạc, giảm sự phụ thuộc giữa các dịch vụ và thuận lợi cho quá trình bảo trì sau này.

Bên cạnh đó, nhóm nhận thấy AWS Elemental MediaConvert là dịch vụ phù hợp đối với các nền tảng Video-on-Demand nhờ khả năng xử lý đa định dạng, hỗ trợ HLS và tích hợp chặt chẽ với các dịch vụ lưu trữ của AWS. Những kiến thức và kinh nghiệm thu được trong tuần này đóng vai trò quan trọng đối với việc hoàn thiện toàn bộ hệ thống trong các giai đoạn tiếp theo.

Nhìn chung, toàn bộ mục tiêu đề ra trong tuần đã được hoàn thành. Pipeline xử lý video vận hành ổn định, các dịch vụ phối hợp đúng theo kiến trúc thiết kế và sẵn sàng cho giai đoạn triển khai tầng phân phối nội dung cũng như ứng dụng Web.

## VII. Kế hoạch chiến lược & Lộ trình tối ưu cho tuần tới

Trong tuần tiếp theo, nhóm sẽ tập trung triển khai tầng truy cập của hệ thống dựa trên Amazon Cognito, Amazon CloudFront và Amazon S3 Frontend Bucket. Đồng thời, nhóm sẽ tích hợp giao diện Web với Amazon API Gateway nhằm cho phép người dùng thực hiện các chức năng đăng nhập, tải video, theo dõi trạng thái xử lý và phát video trực tuyến.

Song song với quá trình tích hợp, nhóm sẽ kiểm thử toàn bộ luồng nghiệp vụ từ xác thực người dùng, tải video, xử lý bất đồng bộ cho đến phân phối nội dung nhằm chuẩn bị cho giai đoạn kiểm thử tổng thể và hoàn thiện phiên bản MVP của hệ thống.