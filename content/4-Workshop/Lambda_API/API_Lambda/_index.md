---
title: "Verify the Connection"
weight: 3
chapter: false
pre: " <b> 4.3.3 </b> "
---

At this point, both Lambda functions are connected to API Gateway. Let's do a quick check before moving to full testing.

---

## Check the integration

1. In API Gateway, click on `/login` → **POST** → **Integration Request**
2. Confirm **Lambda Function** shows `loginFunction`

3. Click on `/songs` → **GET** → **Integration Request**
4. Confirm **Lambda Function** shows `getSongsFunction`

5. Click on `/songs` → **GET** → **Method Request**
6. Confirm **Authorization** shows `CognitoAuthorizer`

![Check integration login](/AWS_Workshop/images/img/inter1.png)
![Check integration songs](/AWS_Workshop/images/img/inter2.png)
![Check authorizer](/AWS_Workshop/images/img/inter3.png)

---

## Quick test from the console

API Gateway has a built-in test tool.

### Test POST /login

1. Click `/login` → **POST** → **TEST** (lightning bolt icon)
2. In **Request Body**, paste:

```json
{
  "email": "test@example.com",
  "password": "Test@12345"
}
```

3. Click **Test**
4. Expected result: `Status: 200` with `idToken`, `accessToken`, `refreshToken` in the response body

### Test GET /songs without token

1. Click `/songs` → **GET** → **TEST**
2. Leave everything empty → **Test**
3. Expected result: `Status: 401` — the authorizer blocks the request

### Test GET /songs with token

1. First get a token from the login test above — copy the `idToken`
2. Click `/songs` → **GET** → **TEST**
3. In **Headers**, add:
   ```
   Authorization: <paste idToken here>
   ```
4. Click **Test**
5. Expected result: `Status: 200` with the songs list

If all three tests pass, the setup is correct. Proceed to the Testing section for end-to-end testing with a real HTTP client.
