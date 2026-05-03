---
title: "Testing"
weight: 4
chapter: false
pre: " <b> 4.4 </b> "
---

Now we test the full flow using real HTTP requests. You can use **Postman**, **curl**, or PowerShell.

Set your Invoke URL as a variable:

```
BASE_URL = https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com/dev
```

---

## Test 1: Login with correct credentials

**PowerShell:**

```powershell
Invoke-RestMethod -Method POST `
  -Uri "$BASE_URL/login" `
  -ContentType "application/json" `
  -Body (@{ email="test@example.com"; password="Test@12345" } | ConvertTo-Json)
```

**curl:**

```bash
curl -X POST "$BASE_URL/login" \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","password":"Test@12345"}'
```

Expected response:

```json
{
  "accessToken": "...",
  "idToken": "eyJraWQ...",
  "refreshToken": "..."
}
```

Copy the `idToken` — you will use it in the next tests.

![Login success](/images/img/RQ1.png)

---

## Test 2: Get songs with valid token

**PowerShell:**

```powershell
Invoke-RestMethod -Method GET `
  -Uri "$BASE_URL/songs" `
  -Headers @{ Authorization = "<paste idToken here>" }
```

**curl:**

```bash
curl -X GET "$BASE_URL/songs" \
  -H "Authorization: <paste idToken here>"
```

Expected response:

```json
{
  "songs": [
    {
      "songId": "1",
      "title": "Lạc Trôi",
      "artist": "Sơn Tùng M-TP",
      "genre": "vpop"
    }
  ],
  "count": 1
}
```

![Get songs success](/images/img/Result.png)

---

## Test 3: Get songs without token

**PowerShell:**

```powershell
Invoke-RestMethod -Method GET -Uri "$BASE_URL/songs"
```

Expected: `401 Unauthorized`

The request is rejected by API Gateway before it even reaches Lambda.

![Unauthorized](/images/img/Result2.png)

---

## Test 4: Login with wrong password

**PowerShell:**

```powershell
Invoke-RestMethod -Method POST `
  -Uri "$BASE_URL/login" `
  -ContentType "application/json" `
  -Body (@{ email="test@example.com"; password="wrongpassword" } | ConvertTo-Json)
```

Expected: `401` with message `"Incorrect email or password"`

![Wrong password](/images/img/Result3.png)

---

## Check CloudWatch logs

If something is not working as expected, check the Lambda logs:

1. Go to **CloudWatch Console** → **Log groups**
2. Find `/aws/lambda/loginFunction` or `/aws/lambda/getSongsFunction`
3. Open the latest log stream to see the error details
