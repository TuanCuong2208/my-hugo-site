---
title: "Sự kiện 1"
date: 2026-05-24
weight: 1
chapter: false
pre: "<b>4.1. </b>"
---

# BÀI THU HOẠCH "FCAJ COMMUNITY DAY WORKSHOP"

* **Thời gian:** 09:00 - 12:00, Thứ Bảy, ngày 23 tháng 05 năm 2026
* **Địa điểm:** Tầng 26, Tháp tài chính Bitexco, 02 Hải Triều, Bến Nghé, Quận 1, TP. Hồ Chí Minh
* **Vai trò:** Người tham dự (Attendee)
* **Người viết:** Nguyễn Tuấn Cường - Sinh viên năm cuối ngành Công nghệ Phần mềm (HUTECH)

---

### Mục Đích Của Sự Kiện
* Chia sẻ các giải pháp thực tiễn tốt nhất (Best practices) trong thiết kế và xây dựng kiến trúc ứng dụng hiện đại trên nền tảng AWS.
* Giới thiệu phương pháp thiết kế hướng tên miền (Domain-Driven Design - DDD) và kiến trúc hướng sự kiện (Event-Driven Architecture) trong môi trường doanh nghiệp.
* Hướng dẫn và tối ưu hóa quy trình lựa chọn các dịch vụ tính toán (Compute services) phù hợp với quy mô và chi phí hạ tầng.
* Giới thiệu các công cụ AI tiên tiến thế hệ mới hỗ trợ toàn diện vòng đời phát triển phần mềm (Software Development Lifecycle - SDLC).

### Danh Sách Diễn Giả
* **Chị Vy Lâm** - Senior Business Systems Analyst, VPBank
* **Chị Thảo Nguyễn** - GenAI Engineer, VIB
* **Chị Mai Nguyễn** - GenAI Engineer, VIB
* **Chị Uyên Lê** - GenAI Engineer, VIB
* **Anh Tinh Truong** - Platform Engineer, GoTymeX
* **Anh Thinh Nguyen** - DevOps Engineer, FCAJ
* **Anh Đức Đào** - Solutions Architect, Cloud Kinetics
* **Anh Phạm Ng. Hải Anh** - Cloud Consultant, G-AsiaPacific Vietnam

---

### Nội Dung Chi Tiết & Ghi Chép Chuyên Môn

#### 1. Context Is Everything - Đưa AI vào thực tế (Anh Tinh Truong - Platform Engineer, GoTymeX)
Bài trình bày tập trung vào việc tối ưu hóa hiệu quả của các mô hình ngôn ngữ lớn (LLM) thông qua kỹ nghệ ngữ cảnh (Context Engineering). Khi ứng dụng AI vào thực tế, mô hình thường trả về kết quả sai lệch hoặc ảo giác không phải do bản thân mô hình yếu, mà do ngữ cảnh cung cấp không đủ chặt chẽ.
* **Cấu trúc một Ngữ cảnh tốt:** Bao gồm 4 thành phần cốt lõi: Mục tiêu (Goal), Tình huống thực tế (Situation), Các ràng buộc hệ thống (Constraints) và Bằng chứng/Tài liệu kỹ thuật liên quan (Evidence).
* **3 sai lầm phổ biến trong doanh nghiệp:**
  1. *Internet Puller:* Nhồi nhét quá nhiều tài liệu, tệp PDF không lọc vào prompt gây nhiễu và lãng phí tài nguyên token.
  2. *Lặp lại tri thức mã nguồn:* Cung cấp lại các thông tin hiển nhiên mà mô hình đã biết thay vì tập trung vào các yêu cầu tái cấu trúc logic cụ thể.
  3. *Thiếu ràng buộc kỹ thuật:* Đưa ra câu lệnh quá chung chung khiến đầu ra mang tính công nghiệp, không thể tích hợp vào source code hiện tại.
* **Xu hướng tiến hóa:** Trải qua 3 giai đoạn chính từ Prompt (Câu lệnh đơn) -> Context (Ngữ cảnh động kèm tài liệu) -> Memory (Bộ nhớ cá nhân hóa dài hạn). Đây là tiền đề để xây dựng hệ thống "Second AI Brain" tích hợp S3 làm kho lưu trữ, Vector DB để trích xuất dữ liệu ngữ cảnh và Amazon Bedrock để xử lý tạo phản hồi.

#### 2. Friendly AI Assistant với Amazon Q (Anh Phạm Ng. Hải Anh - Cloud Consultant, G-AsiaPacific Vietnam)
Giải quyết bài toán tối ưu hóa năng suất vận hành cho nhân sự phi kỹ thuật trong doanh nghiệp thông qua các tác vụ tự động hóa thông minh và bảo mật.
* **Cơ chế Agentic AI:** Giới thiệu Amazon Q với khả năng tích hợp hơn 40 cổng kết nối dữ liệu (Data connectors) từ S3, hệ quản trị cơ sở dữ liệu doanh nghiệp đến các công cụ tìm kiếm bên thứ ba, tạo thành một trợ lý AI Agent toàn diện.
* **Ứng dụng thực tế (Demo PM Assistant):** Mô phỏng quy trình tự động hóa chuỗi tác vụ của một Quản lý dự án (Project Manager): Tự động tổng hợp biên bản cuộc họp (Minutes of Meeting - MoM), phân tích insight, soạn và gửi email hành động đến các bên liên quan, đồng thời lên lịch tự động cho các phiên làm việc tiếp theo.
* **Tiêu chuẩn Enterprise:** Hệ thống được cấu hình chặt chẽ với tính năng Guardrails bảo vệ dữ liệu, thiết lập quyền kiểm soát truy cập (Access Controls) và tuân thủ các quy định pháp lý (Regulatory Compliance) nghiêm ngặt để tránh rò rỉ dữ liệu nội bộ.

#### 3. Tối Ưu Hóa Hiệu Năng và Bảo Mật với CloudFront (Anh Nguyễn Tuấn Thịnh - DevOps Engineer, FCAJ)
Phân tích sâu về giải pháp ngăn chặn biến động chi phí hạ tầng đột biến (Bill spikes) khi hệ thống gặp lượng truy cập tăng vọt hoặc bị tấn công từ chối dịch vụ (DDoS).
* **Gói giải pháp Fixed-Price CDN + Security:** Giới thiệu mô hình tính phí cố định mới gộp chung các dịch vụ CloudFront, AWS WAF, AWS Shield, Route53 và S3, giúp doanh nghiệp kiểm soát bài toán chi phí vận hành.
* **Kiến trúc Kỹ thuật nâng cao:**
  * *Bảo mật tại vùng biên:* Tận dụng hơn 700 Điểm hiện diện (Points of Presence - PoPs) toàn cầu của CloudFront để giảm thiểu và dập tắt các đợt tấn công mạng (như SYN flood) ngay tại Edge mạng, ngăn chặn lưu lượng xấu tràn vào server gốc (Origin).
  * *Origin Cloaking:* Ẩn hoàn toàn địa chỉ IP của server gốc khỏi internet công cộng bằng cách sử dụng VPC Origin kết hợp với chính sách cấu hình Origin Access Control (OAC).
  * *Tối ưu hóa giao thức:* Triển khai HTTP/3 trên nền tảng QUIC/UDP giúp tải tài nguyên song song (Multiplexing), giảm thiểu tình trạng nghẽn cổ chai. Áp dụng nén dữ liệu giúp tiết kiệm băng thông đến 82% và duy trì kết nối TCP liên tục (Persistent Connections) để triệt tiêu độ trễ bắt tay mạng (TCP handshake).
  * *Edge Computing:* Đẩy các logic điều hướng (URL rewrite), redirect hoặc giả lập API (API mocking) ra xử lý ngay tại vùng biên bằng CloudFront Functions và Lambda@Edge, giúp giảm tải CPU Utilization của server EC2 gốc từ 5% xuống 1%.

#### 4. UTMorpho - Từ ý tưởng đến sản phẩm trong 36 giờ (LotusHacks 2026 - Đội ngũ Kỹ sư VIB)
Phiên chia sẻ thực tế mang tính thực chiến cao về quá trình phát triển giải pháp công nghệ dưới áp lực thời gian cực đoan tại LotusHacks 2026.
* **Vấn đề và Giải pháp:** Nhận thấy sự lặp đi lặp lại gây lãng phí thời gian trong khâu thiết kế UI/UX, đội ngũ đã phát triển hệ thống giao diện neural mang tên UTMorpho. Hệ thống cho phép quét ảnh phác thảo wireframe sơ khởi (vẽ tay trên giấy hoặc iPad) và sử dụng mô hình Claude 4 Sonnet để biên dịch, tự động sinh mã nguồn giao diện hoàn chỉnh ngay lập tức.
* **Thách thức kỹ thuật tại Hackathon:** Đối mặt với hiện tượng AI Overgeneration (AI sinh mã nguồn thừa thãi, không tối ưu), chạm ngưỡng giới hạn Token của API, và trạng thái kiệt sức của đội ngũ (The 36-Hour Sprint).
* **Bài học kinh nghiệm:** Điểm then chốt để hoàn thành sản phẩm là chuyển dịch từ tư duy ôm đồm sang xây dựng một "Trải nghiệm chỉnh sửa tập trung" (Focused Editing Experience). Sự đồng bộ hóa vai trò trong đội ngũ (Team Sync) và việc chấp nhận tinh gọn ý tưởng là chìa khóa quyết định để đưa sản phẩm ra thực tế đúng hạn.

#### 5. Tính Phi Quyết Định (Non-Determinism) của LLM (Anh Đức Đào - Solutions Architect, Cloud Kinetics)
Một bài trình bày chuyên sâu về khoa học máy tính, làm rõ bản chất hệ thống phần cứng ảnh hưởng đến tính ổn định của các ứng dụng AI sinh sản.
* **Đập tan lầm tưởng về Temperature = 0:** Cộng đồng lập trình viên thường nghĩ set giá trị Temperature bằng 0 sẽ khiến mô hình luôn chọn token có xác suất cao nhất (argmax), tạo ra kết quả tất định (deterministic) 100% giống nhau giữa các lần gọi API để sinh dữ liệu cấu trúc (JSON/YAML) hoặc chạy thử nghiệm hồi quy (Regression Testing).
* **Kết quả thực nghiệm chuyên sâu:** Kiểm thử trên 5 mô hình lớn (GPT-3.5, GPT-4o, Llama-3, Mixtral) qua 8 tác vụ xử lý ngôn ngữ tự nhiên (NLP) với 10 lần chạy lặp lại giữ nguyên tham số và seed. Kết quả cho thấy độ chính xác dao động lên tới 15% giữa các lần chạy, và tỷ lệ trùng khớp chuỗi tuyệt đối gần như bằng 0% đối với các bài toán logic phức tạp.
* **Nguyên nhân cốt lõi từ kiến trúc phần cứng:** Phép toán dấu phẩy động (floating-point arithmetic) xử lý song song trên các chip GPU không có tính kết hợp (non-associative) theo tiêu chuẩn IEEE 754. Sự thay đổi nhỏ trong thứ tự thực thi luồng xử lý song song của GPU tạo ra sai số làm tròn vi mô ở logits, từ đó làm thay đổi kết quả của hàm argmax. Ngoài ra, kỹ thuật gom cụm dữ liệu (Batching) trên server của nhà cung cấp dịch vụ AI cũng làm thay đổi môi trường tính toán.
* **Chiến lược giảm thiểu rủi ro:**
  * Áp dụng kỹ thuật bỏ phiếu số đông (Majority voting/Ensemble) qua nhiều lần chạy độc lập để đánh đổi chi phí lấy sự chính xác.
  * Ép buộc định dạng đầu ra nghiêm ngặt bằng cấu hình hệ thống (JSON Mode, Function Calling, Regex).
  * *Mẹo thực chiến:* Giá trị T=0 thường dễ khiến mô hình rơi vào các vòng lặp từ ngữ vô hạn (Repetitive loops). Điểm ngọt kỹ thuật tốt nhất trong thực tế là cài đặt **T=0.1** để vừa giữ được tính nhất quán vừa có đủ độ nhiễu giúp mô hình thoát kẹt logic.

#### 6. Hệ thống Multi-Agent cấp Doanh nghiệp trong chấm điểm Tín dụng (Chị Vy Lâm - Senior BSA, VPBank)
Mô hình kiến trúc phần mềm AI cao cấp được ứng dụng thực tế trong lĩnh vực tài chính - ngân hàng để giải quyết bài toán thẩm định và chấm điểm tín dụng cho các doanh nghiệp khởi nghiệp (Startups).
* **Bài toán thực tế:** Các doanh nghiệp startup thường có thời gian vận hành ngắn (6-18 tháng), không có đủ 3 năm báo cáo tài chính tài sản thế chấp truyền thống nhưng sở hữu tài sản trí tuệ (IP) và mô hình tăng trưởng phức tạp, đa chiều.
* **Kiến trúc Multi-Agent so với Single Agent:** Mô hình một Agent đơn lẻ (Single Agent) hoàn toàn thất bại trong bài toán này do bị giới hạn không gian ngữ cảnh (Context limits), dễ bị pha loãng chuyên môn và không có cơ chế đối soát chéo rủi ro. Giải pháp được đưa ra là thiết lập một **Hội đồng Tín dụng Ảo (Virtual Credit Committee)** sử dụng kiến trúc Multi-Agent bao gồm nhiều Agent chuyên biệt đảm nhận các vai trò song song: *Manager Agent, Financial Analyst Agent, Market Analyst Agent, Team Evaluator Agent,* và *Risk Assessor Agent*. Các Agent này tiến hành tranh luận chéo, tạo ra chuỗi vết kiểm toán minh bạch (Audit Trail) và tăng khả năng chịu lỗi (Fault Tolerance) cho hệ thống.
* **Trụ cột Kiến trúc Enterprise-Grade:** Để giải pháp AI vận hành thực tế trong ngân hàng, hệ thống phải đáp ứng toàn diện 6 trụ cột cốt lõi: Bảo mật dữ liệu chuyên sâu (IAM, KMS Secrets), Quản trị dữ liệu (Data Residency, ẩn danh thông tin định danh cá nhân PII), Cách ly mạng độc lập (VPC Isolation, AWS PrivateLink), Giám sát vận hành (Prometheus/Grafana, Auto-scaling), Sự kiểm soát của con người (Human-in-the-loop), và Tuân thủ các chứng chỉ bảo mật quốc tế nghiêm ngặt (SOC 2, GDPR, PCI DSS).
* **Cơ chế Hàng rào bảo vệ (Guardrails):** Thiết lập bộ lọc 3 lớp bao gồm *Input Guardrails* (Chống Prompt Injection), *Processing Guardrails* (Kiểm soát ngân sách token và thời gian timeout), và *Output Guardrails* (Rà soát và triệt tiêu lỗi ảo giác hệ thống).
* **Quy trình triển khai hạ tầng đám mây thực tế:** Mã nguồn phát triển local thông qua framework CrewAI -> Đóng gói mã nguồn thành Docker Image -> Đẩy lên AWS ECR -> Triển khai hạ tầng serverless qua Bedrock AgentCore phối hợp với AWS Lambda và phân phối API qua AWS API Gateway.
* **Hiệu quả đầu tư (ROI) thực tế:** Giảm thời gian xử lý thẩm định hồ sơ doanh nghiệp xuống 95% (từ 2-3 tuần xuống còn 2-4 giờ đồng hồ). Tỷ lệ duyệt hồ sơ chính xác tăng từ 35% lên 45%. Chi phí vận hành ra quyết định trên mỗi hồ sơ giảm mạnh từ ~100 triệu VNĐ xuống dưới mức 5 triệu VNĐ, giúp hoàn vốn đầu tư chỉ trong vòng 12 đến 15 tháng.

---

### Kết Luận & Định Hướng Học Tập Cá Nhân
Tham dự buổi AWS Community Day này thực sự là một "cú tát" tỉnh táo cho một sinh viên CNTT như tôi. Ở trường lớp, chúng tôi thường dừng lại ở mức "làm cho code chạy được" (Proof of Concept). Nhưng thực tế sản xuất (Production), đặc biệt là với hệ thống Cloud và AI, là một thế giới hoàn toàn khác.
Tôi nhận ra rằng:
1. Kiến thức căn bản cực kỳ quan trọng: Đừng nghĩ AI sẽ thay thế lập trình viên. Việc hiểu rõ cơ chế float-point của GPU (như anh Đức trình bày) hay giao thức HTTP/3, TCP Handshake (như anh Thịnh phân tích) là chìa khóa để làm chủ công nghệ chứ không phải là thợ gõ API.
2. Kỹ năng thiết kế hệ thống: Kiến trúc Multi-Agent của VPBank cho thấy xu hướng phần mềm tương lai sẽ giống như microservices, nhưng thay vì các service gọi nhau, các AI agents chuyên biệt sẽ cộng tác và kiểm soát lẫn nhau.
3. Bảo mật và Ngữ cảnh là Vua: Để AI thực sự ứng dụng được trong doanh nghiệp, kỹ năng Context Engineering và thiết lập các lớp Guardrails, VPC, OAC là bắt buộc để đảm bảo dữ liệu không bị rò rỉ.
Worklog hôm nay không chỉ là bản ghi chép, mà sẽ là định hướng cho đồ án tốt nghiệp sắp tới của tôi: Xây dựng một ứng dụng AI không chỉ "thông minh" mà còn phải "an toàn" và "tối ưu chi phí" theo tư duy Enterprise. Cảm ơn các speaker và AWS đã tổ chức một sự kiện quá chất lượng! Chắc chắn tôi sẽ tìm hiểu ngay về Model Context Protocol (MCP) và Terraform như bài tập thực hành chị Vy đã gợi ý
.