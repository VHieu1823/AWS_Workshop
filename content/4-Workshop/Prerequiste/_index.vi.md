---
title: "Chuẩn bị"
weight: 2
chapter: false
pre: " <b> 4.2 </b> "
---

Trước khi viết code, chúng ta cần chuẩn bị ba thứ: IAM role cho Lambda, DynamoDB table để lưu bài hát, và Cognito user pool để xác thực.

---

## 1. Tạo IAM Role cho Lambda

Lambda function cần quyền truy cập DynamoDB và ghi log vào CloudWatch.

1. Vào **IAM Console** → **Roles** → **Create role**
2. Chọn **AWS service** → **Lambda** → **Next**

![Tạo IAM role](/AWS_Workshop/images/img/LD3.png)

3. Tìm và gắn hai policy sau:
   - `AmazonDynamoDBFullAccess`
   - `CloudWatchLogsFullAccess`

4. Đặt tên role là `lambda-workshop-role` → **Create role**

{{% notice info %}}
Trong môi trường production thực tế, bạn nên dùng policy giới hạn quyền hơn. Với workshop này, các managed policy trên giúp đơn giản hóa các bước.
{{% /notice %}}

---

## 2. Tạo DynamoDB Table

Chúng ta cần một table để lưu dữ liệu bài hát.

### Table songs

1. Vào **DynamoDB Console** → **Tables** → **Create table**

![Tạo DynamoDB table](/AWS_Workshop/images/img/DB1.png)

2. Cấu hình:
   - **Table name:** `songs`
   - **Partition key:** `songId` (String)
   - **Settings:** Default settings

3. Nhấn **Create table**

![DynamoDB table đã tạo](/AWS_Workshop/images/img/DB2.png)

### Thêm dữ liệu mẫu

Sau khi tạo xong table, thêm vài item thủ công để `GET /songs` có dữ liệu trả về.

1. Nhấn vào table `songs` → **Explore table items** → **Create item**
2. Chuyển sang **JSON view** và dán vào:

```json
{
  "songId": { "S": "1" },
  "title": { "S": "Lạc Trôi" },
  "artist": { "S": "Sơn Tùng M-TP" },
  "genre": { "S": "vpop" }
}
```

3. Nhấn **Create item**. Lặp lại để thêm 1-2 bài hát nữa nếu muốn.

---

## 3. Tạo Cognito User Pool

1. Vào **Cognito Console** → **User pools** → **Create user pool**

![Tạo Cognito user pool](/AWS_Workshop/images/img/CG1.png)

2. Cấu hình đăng nhập:
   - **Sign-in options:** Email
   - Giữ các giá trị mặc định → **Next** qua các bước

3. Ở bước **App client**:
   - **App client name:** `workshop-client`
   - **Authentication flows:** tích chọn `ALLOW_USER_PASSWORD_AUTH` và `ALLOW_REFRESH_TOKEN_AUTH`
   - **Client secret:** chọn **Generate a client secret** (cần cho code Lambda)

4. Đặt tên user pool là `workshop-pool` → **Create user pool**

![Cognito user pool đã tạo](/AWS_Workshop/images/img/CG2.png)

5. Ghi lại các giá trị sau — sẽ cần dùng ở các bước tiếp theo:
   - **User Pool ID** (dạng: `us-east-1_XXXXXXX`)
   - **App client ID**
   - **App client secret**

### Tạo user để test

1. Trong user pool → **Users** → **Create user**
2. Cấu hình:
   - **Email:** `test@example.com`
   - **Temporary password:** `Test@12345`
   - Bỏ tích **Send an invitation**

3. User sẽ ở trạng thái **Force change password**. Đặt mật khẩu vĩnh viễn bằng AWS CLI:

```bash
aws cognito-idp admin-set-user-password \
  --user-pool-id <YOUR_USER_POOL_ID> \
  --username test@example.com \
  --password "Test@12345" \
  --permanent
```

User đã sẵn sàng để đăng nhập.
