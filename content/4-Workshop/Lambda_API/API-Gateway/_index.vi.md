---
title: "Cài đặt API Gateway"
weight: 2
chapter: false
pre: " <b> 4.3.2 </b> "
---

Chúng ta tạo một REST API với hai route và gắn Cognito JWT Authorizer để bảo vệ `GET /songs`.

---

## 1. Tạo API

1. Vào **API Gateway Console** → **Create API**
2. Chọn **REST API** → **Build**

![Tạo API](/AWS_Workshop/images/img/AG1.png)

3. Cấu hình:
   - **API name:** `workshop-api`
   - **Endpoint type:** Regional

![Cấu hình API](/AWS_Workshop/images/img/AG2.png)

4. Nhấn **Create API**. Bạn sẽ thấy resource gốc `/`.

![Resource gốc](/AWS_Workshop/images/img/AG3.png)

---

## 2. Tạo resource và method

### Resource /login

1. Chọn root `/` → **Actions** → **Create Resource**
2. **Resource name:** `login` → **Create Resource**

![Tạo resource login](/AWS_Workshop/images/img/AG4.png)

3. Chọn `/login` → **Actions** → **Create Method** → **POST** → ✓
4. Cấu hình:
   - **Integration type:** Lambda Function
   - **Lambda proxy integration:** ✓ (tích chọn)
   - **Lambda function:** `loginFunction`

5. Nhấn **Save** → **OK** để cấp quyền

![Tạo POST /login](/AWS_Workshop/images/img/AG5.png)

### Resource /songs

1. Chọn root `/` → **Actions** → **Create Resource**
2. **Resource name:** `songs` → **Create Resource**
3. Chọn `/songs` → **Actions** → **Create Method** → **GET** → ✓
4. Cấu hình:
   - **Integration type:** Lambda Function
   - **Lambda proxy integration:** ✓ (tích chọn)
   - **Lambda function:** `getSongsFunction`

5. Nhấn **Save** → **OK**
   ![Tạo POST /login](/AWS_Workshop/images/img/getsongapi.png)

---

## 3. Tạo Cognito Authorizer

Authorizer này sẽ kiểm tra JWT token trên mỗi request đến `GET /songs`.

1. Ở sidebar bên trái → **Authorizers** → **Create New Authorizer**
2. Cấu hình:
   - **Name:** `CognitoAuthorizer`
   - **Type:** Cognito
   - **Cognito User Pool:** chọn `workshop-pool`
   - **Token source:** `Authorization`

![Tạo Cognito Authorizer](/AWS_Workshop/images/img/auth1.png)
![Tạo Cognito Authorizer](/AWS_Workshop/images/img/auth2.png)
![Tạo Cognito Authorizer](/AWS_Workshop/images/img/auth3.png)

3. Nhấn **Create**
4. Nhấn **Test** → nhập `idToken` từ một lần đăng nhập → kiểm tra trả về `200`

---

## 4. Gắn Authorizer vào GET /songs

1. Nhấn vào `/songs` → method **GET**
2. Nhấn **Method Request**
3. Ở mục **Authorization**, chọn `CognitoAuthorizer` từ dropdown
4. Nhấn dấu ✓ để lưu
   ![Tạo Cognito Authorizer](/AWS_Workshop/images/img/meth1.png)
   ![Tạo Cognito Authorizer](/AWS_Workshop/images/img/meth42.png)
   Bây giờ `GET /songs` yêu cầu JWT token hợp lệ. `POST /login` vẫn là public.

---

## 5. Bật CORS

Với mỗi resource (`/login` và `/songs`):

1. Chọn resource → **Actions** → **Enable CORS**
2. Giữ mặc định → **Enable CORS and replace existing CORS headers** → **Yes**
   ![Tạo Cognito Authorizer](/AWS_Workshop/images/img/cors1.png)
   ![Tạo Cognito Authorizer](/AWS_Workshop/images/img/cors2.png)

---

## 6. Deploy API

1. **Actions** → **Deploy API**
2. Cấu hình:
   - **Deployment stage:** [New Stage]
   - **Stage name:** `dev`

![Deploy API](/AWS_Workshop/images/img/AG7.png)

3. Nhấn **Deploy**
4. Sao chép **Invoke URL** — có dạng:
   `https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com/dev`

{{% notice info %}}
Lưu lại URL này. Bạn sẽ dùng nó ở phần Kiểm thử.
{{% /notice %}}
