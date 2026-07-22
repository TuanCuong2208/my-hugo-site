---
title: "Worklog Tuần 11"
date: 2026-06-30
weight: 11
chapter: false
pre: "<b>1.11. </b>"
---

## I. Tóm tắt tổng quan

Sau khi hoàn thành Video Processing Pipeline, tuần thứ mười một tập trung vào việc phát triển và hoàn thiện ứng dụng Web nhằm kết nối người dùng với toàn bộ hệ thống Serverless Video-on-Demand Platform. Trong tuần này, nhóm triển khai giao diện đăng nhập, chức năng tải video, hiển thị danh sách video và phát video trực tuyến sau khi quá trình chuyển mã hoàn tất.

Song song với việc phát triển giao diện, nhóm tiến hành tích hợp ứng dụng với Amazon API Gateway, AWS Lambda, Amazon DynamoDB và Amazon S3 để tạo thành một quy trình xuyên suốt từ khi người dùng đăng nhập đến khi video được phát trên trình duyệt.

Ngoài ra, nhiều vòng kiểm thử cũng được thực hiện nhằm đánh giá khả năng đồng bộ dữ liệu giữa Frontend và Backend, đồng thời tối ưu trải nghiệm người dùng trước khi bước vào giai đoạn kiểm thử tổng thể.

---

## II. Mục tiêu chiến lược trong tuần

Các mục tiêu của tuần bao gồm:

- Hoàn thiện giao diện Web Application.
- Tích hợp chức năng đăng nhập người dùng.
- Kết nối Backend API với giao diện.
- Hoàn thiện chức năng Upload Video.
- Hiển thị danh sách video từ Amazon DynamoDB.
- Theo dõi trạng thái xử lý video.
- Xây dựng chức năng phát video HLS.
- Thiết kế Dashboard quản lý video.
- Kiểm thử luồng hoạt động của ứng dụng.
- Chuẩn bị cho giai đoạn kiểm thử toàn hệ thống.

---

## III. Nhật ký hoạt động & Lộ trình phân bổ chi tiết (Từ 30/06/2026 đến 06/07/2026)

| Thời gian | Danh mục hoạt động | Nội dung thực hiện | Kết quả |
|------------|--------------------|--------------------|----------|
| **Ngày 1 (30/06)** | Thiết kế giao diện | Hoàn thiện bố cục giao diện đăng nhập, trang Upload Video và trang quản lý video. Chuẩn hóa luồng thao tác của người dùng trên toàn bộ ứng dụng. | Giao diện cơ bản được hoàn thành. |
| **Ngày 2 (01/07)** | Tích hợp Backend API | Kết nối ứng dụng với Amazon API Gateway để gọi các API tạo Presigned URL, lưu metadata và truy vấn danh sách video. | Frontend giao tiếp thành công với Backend. |
| **Ngày 3 (02/07)** | Hoàn thiện Upload Video | Tích hợp chức năng Upload Video trực tiếp lên Amazon S3 thông qua Presigned URL và hiển thị tiến trình tải lên. | Video được tải thành công từ giao diện web. |
| **Ngày 4 (03/07)** | Hiển thị danh sách video | Truy vấn dữ liệu từ Amazon DynamoDB và hiển thị danh sách video cùng trạng thái xử lý trên giao diện. | Danh sách video được cập nhật chính xác. |
| **Ngày 5 (04/07)** | Phát video | Tích hợp trình phát HLS sử dụng dữ liệu đã xử lý trong Amazon S3 Processed Media Bucket thông qua Amazon CloudFront. | Video phát thành công trên trình duyệt. |
| **Ngày 6 (05/07)** | Dashboard hệ thống | Hoàn thiện Dashboard hiển thị thông tin video và trạng thái xử lý. Điều chỉnh bố cục để tăng khả năng quan sát. | Dashboard hoạt động ổn định. |
| **Ngày 7 (06/07)** | Kiểm thử tích hợp | Kiểm thử toàn bộ luồng từ đăng nhập, Upload, xử lý Pipeline đến phát video trên ứng dụng web. | Luồng xử lý hoạt động thông suốt. |

---

## IV. Thực thi kỹ thuật chuyên sâu & Phân tích chi tiết

Trong tuần này, nhóm tập trung vào việc tích hợp toàn bộ các dịch vụ AWS đã xây dựng ở các tuần trước vào một ứng dụng Web thống nhất. Mục tiêu không chỉ là hiển thị dữ liệu mà còn đảm bảo toàn bộ quy trình xử lý video có thể được người dùng thực hiện thông qua giao diện trực quan.

Ứng dụng giao tiếp với Backend thông qua Amazon API Gateway. Mỗi thao tác của người dùng như tải video hoặc truy vấn danh sách video đều được gửi đến các API tương ứng trên Backend, sau đó AWS Lambda xử lý và trả kết quả về ứng dụng.

Đối với chức năng Upload Video, ứng dụng không gửi trực tiếp tệp qua Backend mà trước tiên yêu cầu một Presigned URL. Sau khi nhận được URL, trình duyệt tải video trực tiếp lên Amazon S3 Raw Upload Bucket. Cách tiếp cận này giúp giảm tải đáng kể cho Backend và tăng tốc độ tải tệp.

Sau khi Pipeline xử lý hoàn tất, metadata trong Amazon DynamoDB được cập nhật. Ứng dụng định kỳ truy vấn dữ liệu để hiển thị trạng thái xử lý của từng video và cập nhật giao diện khi video sẵn sàng phát.

Đối với chức năng phát video, ứng dụng sử dụng đường dẫn HLS đã được MediaConvert tạo ra và phát thông qua Amazon CloudFront. Việc sử dụng CloudFront giúp giảm độ trễ, tăng tốc độ tải nội dung và cải thiện trải nghiệm xem video trên nhiều thiết bị.

Dashboard được xây dựng nhằm tổng hợp toàn bộ thông tin quan trọng của hệ thống trên một giao diện duy nhất. Người dùng có thể theo dõi danh sách video, trạng thái xử lý và kết quả chuyển mã mà không cần truy cập trực tiếp vào AWS Management Console.

Thông qua quá trình tích hợp, hệ thống đã đạt được đầy đủ các chức năng của một nền tảng Video-on-Demand cơ bản theo kiến trúc Serverless.

---

## V. Thách thức hạ tầng, Nhật ký xử lý lỗi & Góc nhìn chuyên gia

Trong quá trình tích hợp, nhóm gặp một số lỗi liên quan đến việc đồng bộ dữ liệu giữa Backend và giao diện Web.

Một số API ban đầu trả về dữ liệu chưa đúng định dạng khiến giao diện không thể hiển thị chính xác danh sách video. Sau khi chuẩn hóa cấu trúc dữ liệu trả về từ AWS Lambda, vấn đề đã được khắc phục.

Ngoài ra, việc phát video HLS cũng gặp khó khăn do đường dẫn đầu ra chưa được cập nhật sau khi MediaConvert hoàn thành. Nhóm tiến hành kiểm tra metadata trong Amazon DynamoDB và điều chỉnh cách lưu đường dẫn phát video.

Bên cạnh đó, nhóm tối ưu giao diện để hiển thị trạng thái xử lý theo thời gian thực, giúp người dùng dễ dàng theo dõi tiến trình xử lý video.

Những khó khăn này giúp nhóm hiểu rõ hơn về việc tích hợp giữa giao diện người dùng và các dịch vụ Backend trong môi trường Serverless.

---

## VI. Đánh giá và Chiêm nghiệm chuyên môn

Sau tuần làm việc này, toàn bộ hệ thống đã có thể vận hành từ góc nhìn của người dùng cuối.

Nhóm nhận thấy rằng việc tách riêng Frontend, Backend và Pipeline giúp quá trình phát triển trở nên rõ ràng hơn, đồng thời thuận lợi cho việc mở rộng hoặc thay thế từng thành phần trong tương lai.

Việc sử dụng Presigned URL và Amazon CloudFront không chỉ cải thiện hiệu năng mà còn giúp tối ưu chi phí vận hành khi triển khai trên AWS.

Thông qua quá trình tích hợp, nhóm tích lũy thêm kinh nghiệm về phát triển ứng dụng Web kết hợp với kiến trúc Serverless và quy trình xử lý video trên nền tảng đám mây.

---

## VII. Kế hoạch chiến lược & Lộ trình tối ưu cho tuần tới

Trong tuần cuối của kỳ thực tập, nhóm sẽ tập trung vào việc kiểm thử toàn bộ hệ thống và hoàn thiện tài liệu dự án.

Các công việc dự kiến bao gồm:

- Kiểm thử chức năng đăng nhập.
- Kiểm thử Upload Video.
- Kiểm thử Video Processing Pipeline.
- Kiểm thử phát video trên trình duyệt.
- Đánh giá hiệu năng toàn hệ thống.
- Khắc phục các lỗi còn tồn tại.
- Hoàn thiện tài liệu kỹ thuật.
- Chuẩn bị báo cáo và nghiệm thu dự án.