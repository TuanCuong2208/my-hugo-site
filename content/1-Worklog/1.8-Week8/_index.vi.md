---
title: "Worklog Tuần 8"
date: 2026-06-09
weight: 8
chapter: false
pre: "<b> 1.8. </b> "
---

### I. Tóm tắt tổng quan (Executive Summary)

Sau khi hoàn thành bản thiết kế kiến trúc tổng thể của hệ thống trong tuần trước, nhóm tiếp tục bước sang giai đoạn hoàn thiện thiết kế kỹ thuật trước khi bắt đầu triển khai các chức năng đầu tiên của đồ án. Mục tiêu của tuần này là rà soát lại toàn bộ kiến trúc đã xây dựng, phân tích chi tiết hơn về các thành phần của hệ thống và xác định cách thức hiện thực hóa từng module trong quá trình phát triển.

Trong quá trình nghiên cứu, nhóm tiếp tục tham khảo tài liệu từ AWS Documentation, AWS Prescriptive Guidance và một số dự án Video-on-Demand mã nguồn mở nhằm đánh giá tính phù hợp của kiến trúc đã lựa chọn. Thông qua các buổi trao đổi nội bộ, nhóm tiến hành điều chỉnh một số thành phần trong kiến trúc để đảm bảo khả năng mở rộng, giảm sự phụ thuộc giữa các dịch vụ và thuận lợi hơn trong quá trình triển khai.

Song song với đó, nhóm bắt đầu thiết kế mô hình dữ liệu cho Amazon DynamoDB, xây dựng danh sách các API nghiệp vụ dự kiến triển khai thông qua Amazon API Gateway và AWS Lambda, đồng thời xác định quy trình xử lý dữ liệu giữa các thành phần trong hệ thống.

Kết thúc tuần làm việc, nhóm đã hoàn thiện các tài liệu thiết kế kỹ thuật ở mức cơ bản, tạo tiền đề để bước sang giai đoạn hiện thực hóa hệ thống trong tuần tiếp theo.

### II. Mục tiêu chiến lược trong tuần (Strategic Objectives)

Sau khi xác định được kiến trúc tổng thể, mục tiêu của tuần thứ 8 là cụ thể hóa các thành phần kỹ thuật nhằm chuẩn bị cho quá trình phát triển hệ thống.

Các mục tiêu chính bao gồm:

- Rà soát và hoàn thiện kiến trúc tổng thể dựa trên quá trình nghiên cứu và thảo luận nội bộ.
- Thiết kế mô hình dữ liệu cho Amazon DynamoDB.
- Xác định các API nghiệp vụ và phương thức giao tiếp giữa Frontend và Backend.
- Chuẩn bị cấu trúc dự án và phân chia hệ thống thành các module chức năng.
- Xây dựng kế hoạch triển khai chi tiết cho từng giai đoạn phát triển.
- Đảm bảo các quyết định thiết kế đáp ứng yêu cầu về khả năng mở rộng, hiệu năng và chi phí vận hành.

Thông qua các mục tiêu trên, nhóm hướng đến việc tạo ra một nền tảng kỹ thuật thống nhất trước khi bắt đầu phát triển các chức năng của hệ thống.

### III. Nhật ký hoạt động & Lộ trình phân bổ chi tiết (Từ 09/06/2026 đến 15/06/2026)

| Thời gian | Danh mục hoạt động | Chi tiết các tác vụ thực hiện chuyên sâu | Kết quả/Minh chứng đạt được |
| :--- | :--- | :--- | :--- |
| **Ngày 1** *(09/06)* | Rà soát kiến trúc | Đánh giá lại Architecture Draft V1, kiểm tra luồng dữ liệu và vai trò của từng dịch vụ AWS trong hệ thống. | Hoàn thiện phiên bản kiến trúc phục vụ giai đoạn thiết kế kỹ thuật. |
| **Ngày 2** *(10/06)* | Thiết kế cơ sở dữ liệu | Xây dựng mô hình dữ liệu trên Amazon DynamoDB, xác định Partition Key, Sort Key và các trường metadata của video. | Hoàn thiện bản thiết kế dữ liệu sơ bộ cho hệ thống. |
| **Ngày 3** *(11/06)* | Thiết kế API | Xác định các API cần triển khai, phương thức HTTP, Request/Response và quy trình xác thực thông qua Amazon Cognito. | Hoàn thành danh sách API phục vụ các chức năng chính. |
| **Ngày 4** *(12/06)* | Thiết kế quy trình xử lý | Phân tích luồng Upload Video, Video Processing và Video Streaming; xác định dữ liệu trao đổi giữa các dịch vụ. | Hoàn thiện luồng xử lý nghiệp vụ của hệ thống. |
| **Ngày 5** *(13/06)* | Chuẩn bị môi trường phát triển | Thiết lập cấu trúc dự án, tổ chức thư mục mã nguồn và chuẩn bị môi trường phát triển cho Backend và Frontend. | Hoàn thành cấu trúc ban đầu của dự án. |
| **Ngày 6** *(14/06)* | Lập kế hoạch triển khai | Phân chia hệ thống thành các module chức năng và xây dựng kế hoạch phát triển theo từng giai đoạn. | Hoàn thiện roadmap triển khai chi tiết. |
| **Ngày 7** *(15/06)* | Tổng kết thiết kế | Rà soát toàn bộ tài liệu kỹ thuật, thống nhất hướng triển khai và chuẩn bị bước sang giai đoạn lập trình. | Hoàn thiện bộ tài liệu thiết kế kỹ thuật cho hệ thống. |

### IV. Thực thi kỹ thuật chuyên sâu & Phân tích chi tiết

Sau khi hoàn thành bản thiết kế kiến trúc tổng thể trong tuần trước, nhóm tiếp tục tập trung hoàn thiện các thành phần kỹ thuật ở mức thiết kế nhằm chuẩn bị cho giai đoạn triển khai hệ thống. Mục tiêu của tuần này không phải là phát triển chức năng mà là chuyển đổi bản kiến trúc tổng quan thành các tài liệu kỹ thuật có thể sử dụng trực tiếp trong quá trình lập trình.

Trong quá trình nghiên cứu, nhóm tiếp tục tham khảo tài liệu chính thức từ AWS Documentation, AWS Well-Architected Framework và một số dự án Video-on-Demand mã nguồn mở để đánh giá tính phù hợp của kiến trúc đã xây dựng. Thông qua việc đối chiếu nhiều cách triển khai khác nhau, nhóm tiến hành điều chỉnh một số thành phần nhằm đơn giản hóa luồng xử lý, giảm sự phụ thuộc giữa các dịch vụ và đảm bảo khả năng mở rộng trong tương lai.

Một trong những nội dung trọng tâm của tuần là thiết kế mô hình dữ liệu cho hệ thống. Sau khi phân tích các yêu cầu nghiệp vụ, nhóm quyết định tiếp tục sử dụng Amazon DynamoDB làm cơ sở dữ liệu chính để lưu trữ metadata của video. Các trường dữ liệu dự kiến bao gồm Video ID, Video Name, Upload Time, Processing Status, Owner, Category và đường dẫn đến các tệp video sau khi xử lý. Nhóm cũng bước đầu nghiên cứu phương án xây dựng Global Secondary Index (GSI) nhằm phục vụ các nhu cầu truy vấn theo trạng thái hoặc danh mục video.

Bên cạnh đó, nhóm tiến hành xác định danh sách các API sẽ được triển khai trong giai đoạn đầu của dự án. Các API được phân loại thành nhiều nhóm như Authentication, Video Management và Video Streaming. Đối với mỗi API, nhóm thống nhất phương thức HTTP, dữ liệu đầu vào, dữ liệu trả về cũng như cơ chế xác thực dự kiến thông qua Amazon Cognito.

Đối với quy trình xử lý video, nhóm tiếp tục phân tích chi tiết luồng dữ liệu giữa Amazon S3, Amazon SQS, AWS Lambda và AWS Elemental MediaConvert. Thay vì để Backend trực tiếp xử lý toàn bộ quá trình tải lên và chuyển đổi video, nhóm vẫn giữ định hướng xử lý bất đồng bộ nhằm giảm tải cho API và nâng cao khả năng mở rộng của hệ thống.

Ngoài việc thiết kế dữ liệu và API, nhóm cũng bắt đầu xây dựng cấu trúc thư mục của dự án nhằm tạo sự thống nhất giữa các thành viên. Backend và Frontend được tách thành hai phần độc lập, giúp việc phát triển và kiểm thử từng module trở nên thuận tiện hơn. Đồng thời, nhóm cũng xác định rõ ranh giới giữa các module như Authentication, Video Upload, Video Processing và Video Streaming để chuẩn bị cho giai đoạn hiện thực hóa.

Kết thúc tuần làm việc, mặc dù chưa bắt đầu lập trình các chức năng cụ thể, nhóm đã hoàn thiện phần lớn tài liệu thiết kế kỹ thuật cần thiết. Đây được xem là nền tảng quan trọng giúp giảm thiểu các thay đổi lớn trong quá trình phát triển và tạo điều kiện thuận lợi cho việc triển khai hệ thống ở các tuần tiếp theo.

### V. Thách thức hạ tầng, Nhật ký xử lý lỗi & Góc nhìn chuyên gia (Infrastructure Challenges, Error Resolution Logs & Expert Perspectives)

Trong quá trình hoàn thiện thiết kế kỹ thuật, nhóm nhận thấy rằng việc xây dựng một hệ thống Serverless không chỉ đơn thuần là lựa chọn các dịch vụ AWS mà còn cần xác định rõ ranh giới trách nhiệm giữa từng thành phần. Nếu không có một thiết kế thống nhất ngay từ đầu, việc phát triển độc lập từng module có thể dẫn đến sự không tương thích giữa Backend, Database và quy trình xử lý sự kiện.

Một trong những khó khăn được nhóm thảo luận là cách tổ chức dữ liệu trên Amazon DynamoDB. Khác với cơ sở dữ liệu quan hệ, DynamoDB yêu cầu thiết kế dựa trên nhu cầu truy vấn thay vì chuẩn hóa dữ liệu. Điều này khiến nhóm phải dành nhiều thời gian để xác định Partition Key, các thuộc tính cần đánh chỉ mục và phương án mở rộng dữ liệu trong tương lai.

Bên cạnh đó, việc xây dựng danh sách API cũng đặt ra nhiều câu hỏi liên quan đến tính nhất quán của giao diện lập trình. Nhóm thống nhất sử dụng RESTful API, đồng thời xây dựng quy ước đặt tên Endpoint, cấu trúc JSON Request/Response và mã trạng thái HTTP nhằm tạo sự thống nhất trước khi bắt đầu lập trình.

Ngoài các vấn đề về thiết kế, nhóm cũng chú trọng đến khả năng mở rộng của hệ thống trong tương lai. Thay vì thiết kế chỉ phục vụ các chức năng hiện tại, nhóm cố gắng xây dựng kiến trúc có thể bổ sung thêm các tính năng như Video Recommendation, Comment hoặc Playlist mà không cần thay đổi lớn đối với các thành phần đã có.

Thông qua quá trình nghiên cứu và thảo luận, nhóm nhận thấy rằng đầu tư thời gian cho giai đoạn thiết kế sẽ giúp giảm đáng kể các rủi ro kỹ thuật trong quá trình triển khai, đồng thời tạo ra nền tảng ổn định để phát triển các chức năng của hệ thống.

### VI. Đánh giá và Chiêm nghiệm chuyên môn (Professional Reflections)

Tuần thứ 8 giúp nhóm hiểu rõ hơn vai trò của giai đoạn thiết kế trong quy trình phát triển một hệ thống Cloud. Mặc dù chưa trực tiếp xây dựng các chức năng nghiệp vụ, việc phân tích dữ liệu, thiết kế API và xác định luồng xử lý giữa các dịch vụ AWS đã giúp nhóm hình dung rõ ràng hơn về cách các thành phần sẽ phối hợp với nhau trong quá trình triển khai.

Thông qua việc tham khảo tài liệu chính thức của AWS và các dự án thực tế, nhóm cũng nhận thấy rằng một kiến trúc tốt không chỉ đáp ứng yêu cầu hiện tại mà còn phải tạo điều kiện thuận lợi cho việc mở rộng và bảo trì về sau. Những quyết định được đưa ra trong giai đoạn thiết kế sẽ ảnh hưởng trực tiếp đến hiệu năng, chi phí vận hành và khả năng phát triển của hệ thống trong tương lai.

Ngoài ra, tuần làm việc này còn giúp nhóm nâng cao kỹ năng phân tích yêu cầu, thiết kế giải pháp và phối hợp trong quá trình xây dựng một dự án phần mềm. Việc thống nhất các quy ước kỹ thuật trước khi lập trình được đánh giá là cần thiết nhằm hạn chế các thay đổi lớn khi dự án bước vào giai đoạn phát triển.

Nhìn chung, mặc dù chưa tạo ra các chức năng cụ thể, nhóm đã xây dựng được một nền tảng thiết kế tương đối hoàn chỉnh và sẵn sàng chuyển sang giai đoạn triển khai các thành phần đầu tiên của hệ thống.

### VII. Kế hoạch chiến lược & Lộ trình tối ưu cho tuần tới (Strategic Planning & Optimization Roadmap for Next Week)

Trong tuần tiếp theo, nhóm dự kiến sẽ chính thức bắt đầu giai đoạn hiện thực hóa hệ thống dựa trên các tài liệu thiết kế đã xây dựng trong hai tuần vừa qua.

Trọng tâm của tuần kế tiếp sẽ là chuẩn bị hạ tầng AWS phục vụ cho quá trình phát triển, bao gồm cấu hình các dịch vụ cơ bản như Amazon Cognito, Amazon S3, Amazon DynamoDB, Amazon API Gateway và AWS Lambda. Đồng thời, nhóm sẽ xây dựng các module nền tảng đầu tiên của hệ thống như xác thực người dùng, kết nối cơ sở dữ liệu và các API cơ bản phục vụ quản lý video.

Song song với việc phát triển Backend, nhóm cũng sẽ tiến hành kiểm thử từng thành phần ngay sau khi hoàn thành nhằm đảm bảo tính ổn định trước khi tích hợp với các module khác. Việc triển khai theo từng bước nhỏ sẽ giúp nhóm dễ dàng phát hiện vấn đề và điều chỉnh kiến trúc khi cần thiết mà không ảnh hưởng đến toàn bộ hệ thống.

Mục tiêu của tuần tiếp theo là hoàn thành nền tảng kỹ thuật ban đầu của hệ thống, tạo tiền đề để phát triển quy trình Upload Video và Video Processing Pipeline trong các giai đoạn tiếp theo của đồ án.