---
title: "Tạo Lambda Functions"
weight: 1
chapter: false
pre: " <b> 4.3.1 </b> "
---

Chúng ta cần hai Lambda function. Tạo từng cái một.

---

## Function 1: loginFunction

Function này nhận email và password, xác thực với Cognito và trả về JWT token.

### Tạo function

1. Vào **Lambda Console** → **Create function**
2. Cấu hình:
   - **Function name:** `loginFunction`
   - **Runtime:** Node.js 20.x
   - **Execution role:** Use existing role → `lambda-workshop-role`

![Tạo Lambda function](/AWS_Workshop/images/img/LD1.png)

3. Nhấn **Create function**

### Thêm biến môi trường

1. Vào tab **Configuration** → **Environment variables** → **Edit**
2. Thêm các biến sau:

| Key             | Value                         |
| --------------- | ----------------------------- |
| `CLIENT_ID`     | App client ID của Cognito     |
| `CLIENT_SECRET` | App client secret của Cognito |

![Lambda environment variables](/AWS_Workshop/images/img/LD4.png)

### Thêm code

1. Vào tab **Code**
2. Thay thế code mặc định bằng:

```javascript
import {
  CognitoIdentityProviderClient,
  InitiateAuthCommand,
} from "@aws-sdk/client-cognito-identity-provider";
import crypto from "crypto";

const CLIENT_ID = process.env.CLIENT_ID;
const CLIENT_SECRET = process.env.CLIENT_SECRET;

const cognito = new CognitoIdentityProviderClient({});

function generateSecretHash(username) {
  return crypto
    .createHmac("sha256", CLIENT_SECRET)
    .update(username + CLIENT_ID)
    .digest("base64");
}

export const handler = async (event) => {
  try {
    const body = JSON.parse(event.body || "{}");
    const { email, password } = body;

    if (!email || !password) {
      return {
        statusCode: 400,
        body: JSON.stringify({ message: "email và password là bắt buộc" }),
      };
    }

    const result = await cognito.send(
      new InitiateAuthCommand({
        AuthFlow: "USER_PASSWORD_AUTH",
        ClientId: CLIENT_ID,
        AuthParameters: {
          USERNAME: email,
          PASSWORD: password,
          SECRET_HASH: generateSecretHash(email),
        },
      }),
    );

    const tokens = result.AuthenticationResult;

    return {
      statusCode: 200,
      body: JSON.stringify({
        accessToken: tokens.AccessToken,
        idToken: tokens.IdToken,
        refreshToken: tokens.RefreshToken,
      }),
    };
  } catch (err) {
    if (err.name === "NotAuthorizedException") {
      return {
        statusCode: 401,
        body: JSON.stringify({ message: "Email hoặc mật khẩu không đúng" }),
      };
    }
    return {
      statusCode: 500,
      body: JSON.stringify({ message: "Lỗi server" }),
    };
  }
};
```

3. Nhấn **Deploy**

{{% notice info %}}
Chúng ta trả về `idToken` vì đây là token mà JWT Authorizer của API Gateway sẽ kiểm tra. `accessToken` dùng để gọi trực tiếp các dịch vụ AWS.
{{% /notice %}}

---

## Function 2: getSongsFunction

Function này đọc tất cả bài hát từ DynamoDB và trả về. Nó sẽ được bảo vệ bởi JWT Authorizer — bản thân Lambda không cần tự kiểm tra token.

### Tạo function

1. Vào **Lambda Console** → **Create function**
2. Cấu hình:
   - **Function name:** `getSongsFunction`
   - **Runtime:** Node.js 20.x
   - **Execution role:** Use existing role → `lambda-workshop-role`
3. Nhấn **Create function**

### Thêm biến môi trường

1. Vào tab **Configuration** → **Environment variables** → **Edit** (Tương tự như login)
2. Thêm:

| Key           | Value   |
| ------------- | ------- |
| `SONGS_TABLE` | `songs` |

### Thêm code

1. Vào tab **Code**
2. Thay thế code mặc định bằng:

```javascript
import { DynamoDBClient } from "@aws-sdk/client-dynamodb";
import { DynamoDBDocumentClient, ScanCommand } from "@aws-sdk/lib-dynamodb";

const docClient = DynamoDBDocumentClient.from(new DynamoDBClient({}));
const TABLE = process.env.SONGS_TABLE;

export const handler = async (event) => {
  try {
    const result = await docClient.send(
      new ScanCommand({
        TableName: TABLE,
      }),
    );

    return {
      statusCode: 200,
      body: JSON.stringify({
        songs: result.Items,
        count: result.Count,
      }),
    };
  } catch (err) {
    return {
      statusCode: 500,
      body: JSON.stringify({ message: "Lỗi server" }),
    };
  }
};
```

3. Nhấn **Deploy**

{{% notice info %}}
Chúng ta dùng `Scan` để đơn giản hóa. Trong ứng dụng thực tế với nhiều bài hát, bạn nên dùng `Query` với index thay thế.
{{% /notice %}}
