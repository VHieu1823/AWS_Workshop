---
title: "Cleanup"
weight: 5
chapter: false
pre: " <b> 4.5 </b> "
---

{{% notice warning %}}
Delete all resources after completing the workshop to avoid unexpected charges on your AWS bill.
{{% /notice %}}

Delete resources in this order to avoid dependency errors.

---

## 1. Delete API Gateway

1. Go to **API Gateway Console** → **APIs**
2. Select `workshop-api` → **Actions** → **Delete**
3. Confirm deletion

---

## 2. Delete Lambda functions

1. Go to **Lambda Console** → **Functions**
2. Select `loginFunction` → **Actions** → **Delete** → confirm
3. Select `getSongsFunction` → **Actions** → **Delete** → confirm

---

## 3. Delete DynamoDB table

1. Go to **DynamoDB Console** → **Tables**
2. Select `songs` → **Delete** → type `confirm` → **Delete**

---

## 4. Delete Cognito User Pool

1. Go to **Cognito Console** → **User pools**
2. Select `workshop-pool` → **Delete** → type the pool name to confirm → **Delete**

---

## 5. Delete IAM Role

1. Go to **IAM Console** → **Roles**
2. Search for `lambda-workshop-role` → select it → **Delete** → confirm

---

## 6. Delete CloudWatch Log Groups (optional)

Lambda automatically creates log groups. They are low cost but you can clean them up:

1. Go to **CloudWatch Console** → **Log groups**
2. Search for `/aws/lambda/loginFunction` → select → **Actions** → **Delete log group**
3. Repeat for `/aws/lambda/getSongsFunction`

---

## Verify

After deleting, confirm in each console that the resources are gone:

- API Gateway → no `workshop-api`
- Lambda → no `loginFunction` or `getSongsFunction`
- DynamoDB → no `songs` table
- Cognito → no `workshop-pool`
- IAM → no `lambda-workshop-role`
