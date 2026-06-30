---
title: "Worklog Tuần 5"
date: 2026-05-19
weight: 5
chapter: false
pre: "<b> 1.5. </b> "
---

### I. Tóm tắt tổng quan (Executive Summary)
Tuần này đánh dấu một bước tiến quan trọng trong việc làm chủ hạ tầng đám mây với trọng tâm là quản trị danh tính và bảo mật dữ liệu cấp doanh nghiệp. Nội dung tập trung vào việc áp dụng nguyên tắc đặc quyền tối thiểu (Least Privilege) thông qua các tính năng IAM nâng cao như Permission Boundaries và Resource Tags. Bên cạnh đó, bài học bao gồm kỹ thuật vận hành lưu trữ tập tin doanh nghiệp với Amazon FSx và thực thi chiến lược mã hóa dữ liệu At-Rest bằng AWS KMS, đảm bảo tuân thủ các quy tắc bảo mật khắt khe nhất trong môi trường đám mây hiện đại.

### II. Mục tiêu chiến lược trong tuần (Strategic Objectives)
* **IAM Governance:** Nâng cao khả năng kiểm soát truy cập thông qua Permission Boundary và điều kiện (Conditions) gắn với Role/Policy.
* **Storage Security:** Triển khai hạ tầng lưu trữ tập tin có tính sẵn sàng cao và khả năng mở rộng với Amazon FSx cho Windows.
* **Data Protection:** Xây dựng quy trình mã hóa dữ liệu quan trọng trên S3 kết hợp với quản lý khóa tập trung bằng KMS và truy vết log qua CloudTrail.
* **Operational Efficiency:** Tối ưu hóa việc quản trị tài nguyên thông qua gắn thẻ (Resource Tags) và định nghĩa quyền hạn dựa trên ngữ cảnh.

### III. Nhật ký hoạt động & Lộ trình phân bổ chi tiết (Từ 19/05/2026 đến 25/05/2026)

| Thời gian | Danh mục hoạt động | Chi tiết các tác vụ thực hiện chuyên sâu | Kết quả/Minh chứng đạt được |
| :--- | :--- | :--- | :--- |
| **Ngày 1** *(19/05)* | Lưu trữ doanh nghiệp | Triển khai Lab 25: Cấu hình Amazon FSx cho Windows, thiết lập File Shares và kiểm tra hiệu năng. | Hệ thống lưu trữ tập tin sẵn sàng cho môi trường Active Directory. |
| **Ngày 2** *(20/05)* | Bảo mật S3 cơ bản | Triển khai Lab 57: Cấu hình Static Website hosting trên S3, thiết lập Policy công khai và CloudFront. | Website tĩnh được phân phối toàn cầu với độ trễ thấp. |
| **Ngày 3** *(21/05)* | Quản trị IAM & Tags | Triển khai Lab 28: Thiết lập chính sách truy cập dựa trên Resource Tags cho các dịch vụ EC2. | Quyền hạn được kiểm soát dựa trên định danh tài nguyên (Tags). |
| **Ngày 4** *(22/05)* | Giới hạn quyền hạn | Triển khai Lab 30: Cấu hình IAM Permission Boundary để cô lập phạm vi quản trị của người dùng. | Ngăn chặn hành vi leo thang đặc quyền ngoài phạm vi cho phép. |
| **Ngày 5** *(23/05)* | Mã hóa dữ liệu | Triển khai Lab 33: Cấu hình AWS KMS để mã hóa S3 Object, ghi log hoạt động qua CloudTrail/Athena. | Dữ liệu được bảo vệ an toàn với khóa quản lý tập trung. |
| **Ngày 6** *(24/05)* | IAM Nâng cao | Triển khai Lab 44: Cấu hình Role kèm điều kiện IP và thời gian (Conditions) để tăng cường bảo mật. | Tài khoản chỉ được phép truy cập trong phạm vi kiểm soát chặt chẽ. |
| **Ngày 7** *(25/05)* | Authorization & Role | Triển khai Lab 48: Loại bỏ Access Keys, chuyển đổi sang IAM Role cho các ứng dụng chạy trên EC2. | Đạt chuẩn an toàn trong việc cấp quyền cho ứng dụng chạy trên EC2. |

### IV. Thực thi kỹ thuật chuyên sâu & Phân tích chi tiết qua các bài Lab

#### 1. Lab 25: Amazon FSx for Windows File Server

**1. Tổng quan kỹ thuật (Technical Overview)**
Amazon FSx for Windows File Server cung cấp hệ thống lưu trữ tệp (file storage) được quản lý toàn phần (fully managed), tương thích hoàn toàn với giao thức SMB (Server Message Block). Kiến trúc của nó được xây dựng trên nền tảng Windows Server, hỗ trợ tích hợp Active Directory, NTFS và DFS (Distributed File System). Điều này giúp các ứng dụng Windows hiện có di chuyển lên đám mây mà không cần thay đổi code hay cấu hình. Hệ thống tự động sao lưu dữ liệu và duy trì tính sẵn sàng cao, giúp giảm thiểu rủi ro mất mát dữ liệu cho doanh nghiệp.

**2. Quá trình triển khai (Execution Process)**
* **Bước 1: Cấu hình File System:** Tôi thiết lập dung lượng lưu trữ (Storage capacity) là 32 GiB trên nền tảng SSD để đảm bảo hiệu suất đọc/ghi cao cho các tác vụ I/O nặng.
* **Bước 2: Quản trị mạng và bảo mật:** Việc gắn kết FSx vào VPC mặc định giúp cô lập tài nguyên. Tuy nhiên, hệ thống yêu cầu tích hợp với *AWS Managed Microsoft Active Directory* để xác thực người dùng và phân quyền truy cập tệp thông qua quyền NTFS truyền thống.
* **Bước 3: Tối ưu hóa:** Cấu hình tự động sao lưu hàng ngày (Daily backup) và bảo trì định kỳ là các bước thiết yếu để đảm bảo tính toàn vẹn của dữ liệu trong quá trình vận hành lâu dài.

**3. Minh chứng (Proofs)**
* **1:** Màn hình cấu hình thông số kỹ thuật, lựa chọn dung lượng SSD và yêu cầu tích hợp Active Directory trong bước thiết lập FSx.
<img src="/images/week5/1.png" alt="FSx configuration" style="max-width:100%; height:auto;" />

---

#### 2. Lab 57: Starting with Amazon S3

**1. Tổng quan kỹ thuật (Technical Overview)**
Amazon S3 là dịch vụ lưu trữ đối tượng (object storage) cung cấp khả năng mở rộng, tính sẵn sàng cao, bảo mật và hiệu suất vượt trội. Trong Lab này, tôi cấu hình S3 để đóng vai trò là một máy chủ website tĩnh (static website hosting), giúp phân phối nội dung web mà không cần quản lý hạ tầng máy chủ phức tạp.

**2. Quá trình triển khai (Execution Process)**
* **Bước 1: Thiết lập lưu trữ:** Khởi tạo Bucket S3 và gỡ bỏ các rào cản truy cập công khai (Public Access Block) để website có thể tiếp cận từ Internet.
* **Bước 2: Cấu hình Hosting:** Kích hoạt tính năng Static Website Hosting và định nghĩa file `index.html` làm trang chủ.
* **Bước 3: Quản trị bảo mật:** Áp dụng Bucket Policy cho phép `s3:GetObject` đối với mọi người dùng, đảm bảo website hiển thị đúng nội dung cần thiết.

**3. Minh chứng (Proofs)**
* **2:** Màn hình cấu hình Static website hosting đã kích hoạt thành công.
<img src="/images/week5/2.png" alt="Static website hosting" style="max-width:100%; height:auto;" />
* **3:** Bucket Policy cho phép truy cập công khai để hiển thị nội dung website.
<img src="/images/week5/3.png" alt="Bucket Policy" style="max-width:100%; height:auto;" />

---

#### 3. Lab 28: Quản trị truy cập EC2 thông qua Resource Tags bằng IAM

**1. Tổng quan kỹ thuật (Technical Overview)**
Lab này tập trung vào kỹ thuật phân quyền nâng cao trong AWS IAM bằng cách sử dụng các điều kiện (Conditions). Thay vì cấp quyền truy cập toàn diện, tôi triển khai cơ chế kiểm soát dựa trên định danh tài nguyên (Resource-based control) thông qua việc gắn thẻ (Resource Tags). Chỉ những tài nguyên EC2 có thẻ khớp với chính sách được chỉ định mới cho phép thực thi các hành động Start/Stop, giúp tăng cường bảo mật và cô lập tài nguyên theo từng bộ phận (Department-level isolation).

**2. Quá trình triển khai (Execution Process)**
* **Bước 1: Khởi tạo Policy chuyên biệt:** Xây dựng IAM Policy sử dụng JSON với thành phần `Condition` để ràng buộc quyền thực thi dựa trên `aws:ResourceTag/Department`.
* **Bước 2: Quản trị danh tính:** Tạo và cấu hình IAM Role/User, sau đó đính kèm (attach) Policy đã tạo để kiểm soát quyền thao tác trên các tài nguyên EC2.
* **Bước 3: Phân quyền thông minh:** Đảm bảo rằng chỉ những EC2 instance có gắn thẻ `Department: Finance` mới nằm trong phạm vi quản lý của Role này.

**3. Minh chứng (Proofs)**
* **4:** Màn hình cấu hình Policy JSON với điều kiện (Condition) `aws:ResourceTag/Department`.
<img src="/images/week5/4.png" alt="IAM Policy with Condition" style="max-width:100%; height:auto;" />
* **5:** Màn hình chi tiết của Role sau khi đã gán thành công Policy chuyên biệt.
<img src="/images/week5/5.png" alt="IAM Role details" style="max-width:100%; height:auto;" />

---

#### 4. Lab 30: Giới hạn quyền hạn người dùng với IAM Permission Boundary

**1. Tổng quan kỹ thuật (Technical Overview)**
Permission Boundary là một tính năng bảo mật nâng cao trong IAM, cho phép thiết lập "trần quyền hạn" tối đa cho một IAM entity (User hoặc Role). Ngay cả khi một User được cấp quyền AdministratorAccess, họ vẫn không thể thực hiện các hành động vượt quá giới hạn mà Boundary đã xác định. Đây là kỹ thuật cốt lõi trong việc thực thi nguyên tắc "Đặc quyền tối thiểu" (Least Privilege) tại quy mô doanh nghiệp.

**2. Quá trình triển khai (Execution Process)**
* **Bước 1: Định nghĩa giới hạn:** Tạo một chính sách (Policy) làm "Boundary", xác định phạm vi dịch vụ tối đa mà người dùng có thể tiếp cận (ví dụ: chỉ được phép quản lý S3).
* **Bước 2: Gán Boundary:** Thiết lập Permission Boundary cho một IAM User cụ thể, đảm bảo mọi quyền hạn sau này của User đó đều bị chặn bởi "trần" đã định sẵn.
* **Bước 3: Kiểm chứng:** Thử nghiệm việc cấp quyền vượt mức cho User để xác nhận rằng Boundary đã chặn thành công các hành động không mong muốn.

**3. Minh chứng (Proofs)**
* **6:** Cấu hình Policy đóng vai trò là "Permission Boundary" với các hạn chế quyền hạn cụ thể.
<img src="/images/week5/6.png" alt="Permission Boundary Policy" style="max-width:100%; height:auto;" />
* **7:** Màn hình User IAM đã được gán thành công Boundary.
<img src="/images/week5/7.png" alt="IAM User with Boundary" style="max-width:100%; height:auto;" />
---

#### 5. Lab 33: AWS Key Management Service (KMS)

**1. Tổng quan kỹ thuật (Technical Overview)**
AWS KMS là dịch vụ được quản lý giúp người dùng dễ dàng tạo và kiểm soát các khóa mã hóa được sử dụng để mã hóa dữ liệu. Trong bài Lab này, tôi tạo một Customer Managed Key (CMK) để thực hiện mã hóa và giải mã dữ liệu, đồng thời cấu hình quyền quản trị (admin) và quyền sử dụng (usage) tách biệt, đảm bảo nguyên tắc phân quyền trong quản lý khóa.

**2. Quá trình triển khai (Execution Process)**
* **Bước 1: Khởi tạo khóa:** Tạo khóa đối xứng (Symmetric Key) cho mục đích mã hóa/giải mã.
* **Bước 2: Cấu hình chính sách khóa:** Thiết lập IAM users/roles được phép quản trị khóa (Key Administrators) và người dùng được phép sử dụng khóa (Key Users).
* **Bước 3: Thực thi mã hóa:** Sử dụng khóa KMS để mã hóa dữ liệu mẫu, xác minh khả năng bảo mật của dịch vụ.

**3. Minh chứng (Proofs)**
* **8:** Màn hình xác nhận khóa `Lab33-My-KMS-Key` đã được khởi tạo.
<img src="/images/week5/8.png" alt="KMS Key creation" style="max-width:100%; height:auto;" />
* **9:** Kết quả đầu ra là chuỗi văn bản đã được mã hóa bằng khóa KMS.
<img src="/images/week5/9.png" alt="KMS Encryption output" style="max-width:100%; height:auto;" />

---

### V. Thách thức hạ tầng, Nhật ký xử lý lỗi & Góc nhìn từ chuyên gia

* **Thách thức:** Rào cản lớn nhất của Lab 25 là yêu cầu bắt buộc phải có *AWS Managed Microsoft Active Directory*. Việc triển khai tốn chi phí và thời gian khởi tạo dịch vụ khá lâu, đòi hỏi tính kiên nhẫn và quy hoạch tài nguyên kỹ lưỡng.
* **Nhật ký xử lý lỗi:** Thông báo lỗi "*AWS Managed Microsoft Active Directory is required*" xuất hiện khi cố gắng khởi tạo FSx mà chưa có Domain Controller sẵn sàng. Giải pháp là phải thiết lập kết nối VPC và danh tính Directory trước khi cấu hình FSx.
* **Góc nhìn từ chuyên gia:** FSx cho Windows File Server không chỉ đơn thuần là lưu trữ, nó còn hỗ trợ cơ chế tự động mở rộng dung lượng (Automatic capacity scaling) và sao lưu dữ liệu thông qua AWS Backup, rất phù hợp với các doanh nghiệp cần sự ổn định.
* **Khuyến nghị:** Đối với hệ thống Linux, tôi khuyến nghị sử dụng **Amazon EFS** thay vì FSx. EFS cung cấp khả năng truy cập đồng thời hàng nghìn EC2 Instance với giao thức NFS, linh hoạt hơn và không yêu cầu hạ tầng Active Directory phức tạp, giúp giảm đáng kể chi phí vận hành (TCO).

---

### VI. Suy ngẫm nghề nghiệp (Professional Reflections)

Tuần học tập này đã mang lại sự chuyển dịch lớn trong tư duy về an ninh đám mây. Tôi nhận ra rằng việc cấp quyền "Administrator" chỉ là giải pháp tạm thời, còn mô hình "Đặc quyền tối thiểu" (Least Privilege) và "Phân tách nhiệm vụ" (Separation of Duties) mới là chìa khóa để vận hành hệ thống quy mô lớn. Việc nắm vững Permission Boundary và KMS không chỉ giúp tôi hiểu cách chặn đứng các rủi ro leo thang quyền hạn mà còn củng cố năng lực tư vấn giải pháp bảo mật dữ liệu, giúp doanh nghiệp an tâm trước các mối đe dọa nội bộ.

---

### VII. Kế hoạch chiến lược & Lộ trình tối ưu cho tuần tiếp theo

**Mục tiêu chiến lược:** Tăng tốc hoàn thiện kiến thức chuyên môn, tích lũy kinh nghiệm thực tế tại doanh nghiệp và khởi động dự án tốt nghiệp quan trọng.

**Lộ trình thực hiện:**
1.  **Chinh phục Module 6 & 7:** Hoàn thành các bài Lab thuộc module 6 và 7 để củng cố nền tảng kiến thức hệ thống chuyên sâu.
2.  **Học tập tại văn phòng:** Duy trì lịch trình học tập tại văn phòng AWS Vietnam, tận dụng tối đa cơ hội trao đổi trực tiếp với các chuyên gia và học hỏi quy trình vận hành thực tế.
3.  **Khởi động đồ án cuối kỳ:** Nghiên cứu và lên ý tưởng triển khai cho hệ thống "Website Đặt tour du lịch Việt Nam tích hợp Chatbot AI tư vấn thông minh", tập trung vào kiến trúc hệ thống và luồng dữ liệu.
4.  **Tối ưu hạ tầng:** Tiếp tục áp dụng các kỹ thuật bảo mật đã học vào đồ án, đặc biệt là việc sử dụng IAM Role và Permission Boundary để bảo vệ dữ liệu người dùng.
5.  **Nghiên cứu công nghệ bổ trợ:** Tìm hiểu sâu hơn về kiến trúc Microservices và các giải pháp AI-driven để tích hợp vào ứng dụng thực tế.