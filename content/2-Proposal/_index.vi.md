---
title: "Đề xuất dự án"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

### Triển khai API Serverless với API Gateway, Lambda, Cognito và DynamoDB

### 📄 1. Tóm tắt điều hành

Dự án này tập trung xây dựng một hệ thống web nghe nhạc trực tuyến dựa trên kiến trúc serverless, trong đó các thành phần cốt lõi bao gồm Amazon API Gateway, AWS Lambda và Amazon Cognito. Hệ thống cho phép người dùng truy cập và nghe nhạc trực tuyến, quản lý danh sách phát (playlist), đồng thời hỗ trợ các chức năng quản lý nội dung cơ bản.

Trong kiến trúc đề xuất, API Gateway đóng vai trò là điểm tiếp nhận và định tuyến các yêu cầu từ phía client đến các Lambda function tương ứng. AWS Lambda chịu trách nhiệm xử lý logic nghiệp vụ backend và thực hiện các hoạt động giao tiếp với kho lưu trữ dữ liệu S3 và DynamoDB, trong khi Amazon Cognito đảm bảo việc xác thực và phân quyền người dùng thông qua cơ chế token. Cách tiếp cận này giúp loại bỏ nhu cầu quản lý hạ tầng máy chủ truyền thống, đồng thời cung cấp khả năng mở rộng tự động và tối ưu hóa tài nguyên theo nhu cầu sử dụng.

Việc áp dụng mô hình serverless không chỉ giúp hệ thống đạt được hiệu năng và khả năng mở rộng cao mà còn tối ưu chi phí vận hành thông qua mô hình pay-as-you-go. Bên cạnh đó, kiến trúc được thiết kế theo hướng tách biệt rõ ràng giữa frontend và backend, góp phần nâng cao khả năng bảo trì, mở rộng và tích hợp trong tương lai.

---

### 📌 2. Tuyên bố vấn đề

#### Vấn đề hiện tại

Trong bối cảnh nhu cầu chia sẻ và tiếp cận các sản phẩm âm nhạc cá nhân ngày càng gia tăng, các nền tảng hiện có vẫn chưa đáp ứng tốt nhu cầu của người dùng về tính linh hoạt và khả năng cá nhân hóa. Đặc biệt, đối với các nghệ sĩ độc lập, việc đăng tải và quản lý nội dung còn gặp nhiều khó khăn do quy trình phức tạp và thiếu quyền kiểm soát.

Ngoài ra, nhiều hệ thống hiện tại có kiến trúc phức tạp, chi phí vận hành cao và khó mở rộng khi số lượng người dùng tăng. Các vấn đề liên quan đến xác thực người dùng, bảo mật API và quản lý truy cập cũng là những thách thức lớn trong quá trình xây dựng hệ thống.

Do đó, cần thiết phải xây dựng một nền tảng web đơn giản, linh hoạt, cho phép người dùng dễ dàng tương tác với hệ thống, đồng thời đảm bảo khả năng mở rộng, bảo mật và tối ưu chi phí.

---

#### Giải pháp

Để giải quyết các vấn đề trên, hệ thống được xây dựng dựa trên kiến trúc serverless với ba thành phần chính:

- **Amazon API Gateway:** đóng vai trò là gateway trung gian, tiếp nhận request từ client và định tuyến đến các Lambda function
- **AWS Lambda:** xử lý toàn bộ logic nghiệp vụ của hệ thống
- **Amazon Cognito:** đảm bảo xác thực và phân quyền người dùng thông qua JWT token
- **DynamoDB:** lưu trữ metadata của hệ thống.

Luồng xử lý của hệ thống được thiết kế đơn giản và hiệu quả: client gửi request đến API Gateway, sau đó request được xác thực thông qua Cognito và chuyển đến Lambda để xử lý. Kết quả được trả về client thông qua API Gateway.

Giải pháp này giúp hệ thống:

- Tăng khả năng mở rộng tự động
- Giảm chi phí vận hành
- Đảm bảo bảo mật thông qua cơ chế xác thực tập trung
- Đơn giản hóa kiến trúc hệ thống

---

### 📌 3. Kiến trúc giải pháp

Kiến trúc hệ thống được xây dựng theo mô hình serverless, tập trung vào luồng xử lý API:

![ConnectPrivate](/AWS_Workshop/images/aws_architec.png)

- Người dùng gửi request từ frontend đến API Gateway
- API Gateway sử dụng Cognito Authorizer để xác thực người dùng
- Sau khi xác thực thành công, request được chuyển đến Lambda
- Lambda xử lý logic nghiệp vụ lấy dữ liệu từ DynamoDB và trả kết quả về client

Các thành phần chính:

- **API Gateway:** quản lý API, định tuyến request
- **Lambda:** xử lý logic backend theo từng chức năng
- **Cognito:** quản lý user, authentication và authorization
- **DynamoDB:** lưu trữ dữ liệu cho hoạt động hệ thống.

Kiến trúc này giúp đảm bảo tính mở rộng, bảo mật và hiệu năng mà không cần quản lý server.

---

### 📌 4. Triển khai kỹ thuật

#### Các giai đoạn triển khai

Dự án được triển khai theo các giai đoạn sau:

**Nghiên cứu và thiết kế kiến trúc:**  
Tìm hiểu các dịch vụ AWS (API Gateway, Lambda, Cognito, DynamoDB) và thiết kế kiến trúc serverless phù hợp với hệ thống.

**Đánh giá chi phí và tính khả thi:**  
Ước tính chi phí sử dụng AWS Free Tier và đánh giá khả năng vận hành của hệ thống.

**Tối ưu kiến trúc:**  
Thiết kế Lambda function hợp lý, giảm số lượng request không cần thiết và tối ưu luồng xử lý.

**Phát triển và kiểm thử:**  
Triển khai API Gateway, Lambda function và tích hợp Cognito. Thực hiện kiểm thử và hoàn thiện hệ thống.

---

#### Yêu cầu kỹ thuật

**Frontend:**

- Gửi request đến API Gateway thông qua HTTP/REST API
- Xử lý token từ Cognito để xác thực người dùng

**Backend (Serverless):**

- Lambda xử lý logic nghiệp vụ
- API Gateway định tuyến request

---

### 📌 5. Ước tính chi phí AWS

Hệ thống tận dụng AWS Free Tier:

- **AWS Lambda:** 1 triệu request/tháng → ~0 USD
- **API Gateway:** 1 triệu request/tháng → ~0 USD
- **Amazon DynamoDB:** 25GB lưu trữ chi phí → ~0 USD

👉 Tổng chi phí gần như **0 USD/tháng** trong giai đoạn đầu

---

### 📌 6. Đánh giá rủi ro

- **Hiệu năng:** độ trễ nếu Lambda cold start
- **Chi phí:** tăng khi vượt Free Tier
- **Bảo mật:** cấu hình sai Cognito hoặc IAM
- **Thiết kế API:** không tối ưu dẫn đến khó mở rộng

**Giảm thiểu:**

- Tối ưu Lambda
- Sử dụng caching
- Áp dụng best practices bảo mật
- Monitoring qua CloudWatch

---

### 📌 7. Kết quả kỳ vọng

- Xây dựng hệ thống API serverless hoàn chỉnh
- Tối ưu chi phí vận hành
- Dễ dàng mở rộng trong tương lai

- Tạo nền tảng cho các hệ thống lớn hơn như:
  - Microservices
  - AI recommendation
  - Real-time processing
