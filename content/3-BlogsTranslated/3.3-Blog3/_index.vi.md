---
title: "Blog 3"
date: 2026-07-10
weight: 3
chapter: false
pre: "<b> 3.3. </b>"
---

Khi xây dựng một hệ thống backend, **Authentication** (xác thực người dùng) và **Session Management** (quản lý phiên làm việc) gần như là hai thành phần không thể thiếu. Từ việc đăng ký tài khoản, đăng nhập, duy trì phiên làm việc cho đến đăng xuất hay thu hồi session, tất cả đều yêu cầu dữ liệu phải được xử lý chính xác và nhất quán.

Ở quy mô nhỏ, những chức năng này tương đối đơn giản. Tuy nhiên, khi hệ thống bắt đầu phục vụ hàng nghìn hoặc hàng triệu người dùng, các vấn đề như **replication lag**, quản lý nhiều database instance hay bảo mật thông tin kết nối sẽ khiến kiến trúc trở nên phức tạp hơn rất nhiều.

Trong bài viết này, mình sẽ cùng tìm hiểu cách AWS xây dựng một dịch vụ xác thực người dùng hiện đại bằng cách kết hợp **Amazon Aurora DSQL**, **Amazon ECS Express Mode chạy trên AWS Fargate** và **AWS IAM**. Kiến trúc này giúp đảm bảo dữ liệu luôn nhất quán, dễ dàng mở rộng và giảm đáng kể khối lượng công việc vận hành hạ tầng.

---

## Những Điểm Nổi Bật Của Kiến Trúc

Kiến trúc được AWS đề xuất tập trung vào việc tận dụng các dịch vụ managed/serverless để giảm tối đa công việc quản trị hệ thống.

### Amazon Aurora DSQL

Aurora DSQL là cơ sở dữ liệu serverless tương thích PostgreSQL và hỗ trợ **Strong Read-after-Write Consistency**. Điều này giúp dữ liệu vừa được ghi có thể được đọc lại ngay lập tức, rất phù hợp với các luồng như đăng ký tài khoản, đăng nhập hoặc kiểm tra trạng thái session.

Ngoài ra, Aurora DSQL còn tự động mở rộng theo workload mà không cần cấu hình database instance hay read replica như các mô hình truyền thống.

### Amazon ECS Express Mode và AWS Fargate

Ứng dụng backend được container hóa bằng Node.js/Express và triển khai trên Amazon ECS Express Mode sử dụng AWS Fargate.

Nhờ đó, nhóm phát triển không cần quản lý máy chủ, cài đặt hệ điều hành hay cấu hình Auto Scaling. AWS sẽ tự động xử lý việc triển khai, mở rộng và duy trì môi trường chạy ứng dụng.

### AWS IAM Authentication

Thay vì lưu thông tin đăng nhập database trong file cấu hình hoặc biến môi trường, ECS Task Role sẽ được cấp quyền truy cập trực tiếp đến Aurora DSQL thông qua **IAM Authentication**.

Cách tiếp cận này giúp hạn chế rủi ro lộ credential và đơn giản hóa việc quản lý quyền truy cập trong môi trường production.

---

## Thiết Kế Dữ Liệu Cho Authentication

Kiến trúc sử dụng hai bảng chính:

- **users**: lưu thông tin người dùng.
- **sessions**: lưu thông tin các phiên đăng nhập.

Mỗi session sẽ bao gồm:

- Session Token Hash
- Thời gian tạo
- Thời gian hết hạn
- Thời điểm bị thu hồi (nếu có)

Việc tách riêng thông tin người dùng và session giúp hệ thống dễ quản lý hơn, đồng thời hỗ trợ nhiều phiên đăng nhập trên các thiết bị khác nhau.

---

## Luồng Xác Thực Hoạt Động Như Thế Nào?

Quy trình xác thực diễn ra theo các bước sau:

1. Người dùng gửi request HTTPS đến backend.
2. Ứng dụng Node.js/Express tiếp nhận request và xử lý nghiệp vụ.
3. Khi đăng ký, password sẽ được hash bằng **bcrypt**, sau đó tạo UUID cho người dùng và lưu vào Aurora DSQL.
4. Khi đăng nhập, hệ thống kiểm tra email và password. Nếu hợp lệ, một session token mới sẽ được tạo.
5. Session token được hash bằng **SHA-256** trước khi lưu vào bảng `sessions`, còn client chỉ nhận token gốc duy nhất một lần.
6. Với các request cần xác thực, backend sẽ hash lại token do client gửi lên, sau đó so sánh với dữ liệu trong database để kiểm tra tính hợp lệ của session.
7. Khi người dùng đăng xuất hoặc session bị thu hồi, trường `revoked_at` sẽ được cập nhật và session đó sẽ mất hiệu lực ngay lập tức.

---

## Vì Sao Aurora DSQL Phù Hợp Với Authentication?

Điểm đáng chú ý nhất của Aurora DSQL nằm ở khả năng **Strong Read-after-Write Consistency**.

Trong nhiều hệ thống phân tán, dữ liệu vừa ghi có thể mất một khoảng thời gian ngắn mới đồng bộ đến các node khác. Điều này dễ dẫn đến các tình huống như:

- Người dùng vừa đăng ký nhưng chưa thể đăng nhập.
- Session vừa tạo nhưng request tiếp theo lại báo không hợp lệ.
- Session đã bị revoke nhưng vẫn còn hiệu lực trong một khoảng thời gian.

Với Aurora DSQL, những vấn đề trên được hạn chế đáng kể vì dữ liệu luôn có thể được đọc lại ngay sau khi ghi thành công.

Ngoài ra, việc sử dụng IAM Authentication cũng giúp tăng cường bảo mật khi không còn phải quản lý database password theo cách truyền thống.

---

## Bài Học Rút Ra

Qua kiến trúc này có thể thấy rằng Authentication không chỉ đơn thuần là xây dựng API đăng ký hay đăng nhập. Một hệ thống xác thực tốt còn cần đảm bảo ba yếu tố quan trọng:

- **Consistency**: dữ liệu luôn nhất quán sau mỗi lần cập nhật.
- **Security**: bảo vệ password, session token và credential kết nối database.
- **Scalability**: có khả năng mở rộng khi số lượng người dùng tăng cao.

Việc kết hợp Amazon Aurora DSQL, Amazon ECS Express Mode, AWS Fargate và IAM Authentication giúp xây dựng một backend hiện đại với ít công việc vận hành hơn nhưng vẫn đảm bảo hiệu năng và tính bảo mật.

Đây cũng là một ví dụ điển hình về cách AWS khuyến khích sử dụng các dịch vụ managed để tách biệt rõ compute, database và security, từ đó giúp đội ngũ phát triển tập trung nhiều hơn vào business logic thay vì quản trị hạ tầng.

---

## Liên Kết Tham Khảo Và Thảo Luận Cộng Đồng

Nếu bạn muốn tìm hiểu chi tiết hơn về kiến trúc cũng như cách AWS xây dựng dịch vụ Authentication và Session Management với Amazon Aurora DSQL, hãy tham khảo các tài liệu bên dưới. Đồng thời, đừng quên ghé qua bài viết thảo luận trong cộng đồng AWS Study Group FCJ để xem thêm những góc nhìn và chia sẻ thực tế từ các thành viên.

* **Link bài viết gốc từ AWS Blog:** [User Authentication and Session Management with Amazon Aurora DSQL](https://aws.amazon.com/blogs/database/user-authentication-and-session-management-with-amazon-aurora-dsql/)

* **Link bài viết thảo luận trong nhóm AWS:** [AWS Study Group FCJ - Xác Thực Người Dùng Và Quản Lý Session Với Amazon Aurora DSQL](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2205379233560370/)