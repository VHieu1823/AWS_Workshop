---
title: "Preparation"
weight: 2
chapter: false
pre: " <b> 4.2 </b> "
---

Before writing any code, we need to set up three things: an IAM role for Lambda, a DynamoDB table to store songs, and a Cognito user pool for authentication.

---

## 1. Create IAM Role for Lambda

Lambda functions need permission to access DynamoDB and write logs to CloudWatch.

1. Go to **IAM Console** → **Roles** → **Create role**
2. Select **AWS service** → **Lambda** → **Next**

![Create IAM role](/AWS_Workshop/images/img/LD3.png)

3. Search and attach these two policies:
   - `AmazonDynamoDBFullAccess`
   - `CloudWatchLogsFullAccess`

4. Name the role `lambda-workshop-role` → **Create role**

{{% notice info %}}
In a real production environment, you would use a more restrictive policy. For this workshop, these managed policies keep things simple.
{{% /notice %}}

---

## 2. Create DynamoDB Table

We need two tables: one for users and one for songs.

### Songs table

1. Go to **DynamoDB Console** → **Tables** → **Create table**

![DynamoDB create table](/AWS_Workshop/images/img/DB1.png)

2. Configure:
   - **Table name:** `songs`
   - **Partition key:** `songId` (String)
   - **Settings:** Default settings

3. Click **Create table**

![DynamoDB table created](/AWS_Workshop/images/img/DB2.png)

### Seed some song data

Once the table is created, add a few items manually so `GET /songs` has data to return.

1. Click on the `songs` table → **Explore table items** → **Create item**
2. Switch to **JSON view** and paste:

```json
{
  "songId": { "S": "1" },
  "title": { "S": "Lạc Trôi" },
  "artist": { "S": "Sơn Tùng M-TP" },
  "genre": { "S": "vpop" }
}
```

3. Click **Create item**. Repeat for 1-2 more songs if you want.

---

## 3. Create Cognito User Pool

1. Go to **Cognito Console** → **User pools** → **Create user pool**

![Cognito create user pool](/AWS_Workshop/images/img/CG1.png)

2. Configure sign-in:
   - **Sign-in options:** Email
   - Keep other defaults → **Next** through all steps

3. On the **App client** step:
   - **App client name:** `workshop-client`
   - **Authentication flows:** check `ALLOW_USER_PASSWORD_AUTH` and `ALLOW_REFRESH_TOKEN_AUTH`
   - **Client secret:** select **Generate a client secret** (we need this for the Lambda code)

4. Name the user pool `workshop-pool` → **Create user pool**

![Cognito user pool created](/AWS_Workshop/images/img/CG2.png)

5. Note down these values — you will need them later:
   - **User Pool ID** (format: `us-east-1_XXXXXXX`)
   - **App client ID**
   - **App client secret**

### Create a test user

1. In your user pool → **Users** → **Create user**
2. Configure:
   - **Email:** `test@example.com`
   - **Temporary password:** `Test@12345`
   - Uncheck **Send an invitation**

3. The user will be in **Force change password** state. Set a permanent password via AWS CLI:

```bash
aws cognito-idp admin-set-user-password \
  --user-pool-id <YOUR_USER_POOL_ID> \
  --username test@example.com \
  --password "Test@12345" \
  --permanent
```

The user is now ready to log in.
