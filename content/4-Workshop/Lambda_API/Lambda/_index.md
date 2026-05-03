---
title: "Create Lambda Functions"
weight: 1
chapter: false
pre: " <b> 4.3.1 </b> "
---

We need two Lambda functions. Create them one at a time.

---

## Function 1: loginFunction

This function receives email and password, authenticates against Cognito, and returns a JWT token.

### Create the function

1. Go to **Lambda Console** → **Create function**
2. Configure:
   - **Function name:** `loginFunction`
   - **Runtime:** Node.js 20.x
   - **Execution role:** Use existing role → `lambda-workshop-role`

![Create Lambda function](/AWS_Workshop/images/img/LD1.png)

3. Click **Create function**

### Add environment variables

1. Go to **Configuration** tab → **Environment variables** → **Edit**
2. Add these variables:

| Key             | Value                          |
| --------------- | ------------------------------ |
| `CLIENT_ID`     | Your Cognito App client ID     |
| `CLIENT_SECRET` | Your Cognito App client secret |

![Lambda environment variables](/AWS_Workshop/images/img/LD4.png)

### Add the code

1. Go to the **Code** tab
2. Replace the default code with:

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
        body: JSON.stringify({ message: "email and password are required" }),
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
        body: JSON.stringify({ message: "Incorrect email or password" }),
      };
    }
    return {
      statusCode: 500,
      body: JSON.stringify({ message: "Internal server error" }),
    };
  }
};
```

3. Click **Deploy**

{{% notice info %}}
We return `idToken` because that is the token API Gateway's JWT Authorizer will validate. The `accessToken` is for calling AWS services directly.
{{% /notice %}}

---

## Function 2: getSongsFunction

This function reads all songs from DynamoDB and returns them. It will be protected by a JWT Authorizer — Lambda itself does not need to verify the token.

### Create the function

1. Go to **Lambda Console** → **Create function**
2. Configure:
   - **Function name:** `getSongsFunction`
   - **Runtime:** Node.js 20.x
   - **Execution role:** Use existing role → `lambda-workshop-role`

3. Click **Create function**

### Add environment variable

1. Go to **Configuration** tab → **Environment variables** → **Edit** (same steps as loginFunction)
2. Add:

| Key           | Value   |
| ------------- | ------- |
| `SONGS_TABLE` | `songs` |

### Add the code

1. Go to the **Code** tab
2. Replace the default code with:

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
      body: JSON.stringify({ message: "Internal server error" }),
    };
  }
};
```

3. Click **Deploy**

{{% notice info %}}
We use `Scan` here to keep things simple. In a real app with many songs, you would use `Query` with an index instead.
{{% /notice %}}
