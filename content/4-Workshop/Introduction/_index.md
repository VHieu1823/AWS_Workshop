---
title: "Introduction"
weight: 1
chapter: false
pre: " <b> 4.1 </b> "
---

## What are we building?

A simple serverless API for a music app. Users can log in and retrieve a list of songs. The API runs entirely on AWS managed services — no servers to manage.

---

## Services used

### Amazon Cognito

Handles user accounts. Users register and log in through Cognito, which issues a **JWT token** (a signed string that proves who you are). We use this token to protect API routes.

### AWS Lambda

Runs your code without a server. Each API endpoint maps to one Lambda function. Lambda only runs when a request comes in, so you only pay for actual usage.

### Amazon API Gateway

The front door of your API. It receives HTTP requests from clients and routes them to the right Lambda function. It also validates JWT tokens before forwarding requests to Lambda.

### Amazon DynamoDB

A NoSQL database. Fast, serverless, and scales automatically. We use it to store song data.

![Architecture Diagram](/AWS_Workshop/images/img/workshop_architec.png)

---

## How a request flows

**Login (public):**

```
Client → POST /login → API Gateway → Lambda (login) → Cognito → return JWT token
```

**Get songs (protected):**

```
Client → GET /songs → API Gateway → [validate JWT] → Lambda (getSongs) → DynamoDB → return songs
```

If the JWT token is missing or invalid, API Gateway rejects the request with `401 Unauthorized` before it even reaches Lambda.

---

## What you will do step by step

1. Set up DynamoDB table and Cognito user pool
2. Write two Lambda functions: `login` and `getSongs`
3. Create an API Gateway with two routes
4. Attach a Cognito JWT Authorizer to protect `GET /songs`
5. Test everything end-to-end
6. Clean up all resources
