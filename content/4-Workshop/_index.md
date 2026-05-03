---
title: "Workshop"
date: "`r Sys.Date()`"
weight: 4
chapter: false
pre: " <b> 4. </b> "
---

# Build a Serverless API with API Gateway, Lambda, and Cognito

## Overview

In this workshop, you will build a simple serverless REST API on AWS that handles user authentication and song management. Everything is done through the AWS Management Console — no code framework or CLI required beyond writing Lambda function code.

By the end, you will have a working API that:
- Authenticates users via **Amazon Cognito**
- Protects routes using a **JWT Authorizer** on API Gateway
- Stores and retrieves data from **DynamoDB**
- Runs business logic on **AWS Lambda**

---

## Architecture

```
Client → API Gateway → Cognito JWT Authorizer → Lambda → DynamoDB
```

- **Public route:** `POST /login` — anyone can call this
- **Protected route:** `GET /songs` — requires a valid JWT token

---

## Prerequisites

- AWS account (Free Tier is sufficient)
- Basic understanding of REST APIs (what is GET, POST, JSON)
- No prior AWS experience required

---

## Content

1. [Introduction](Introduction/)
2. [Preparation](Prerequiste/)
3. [Lambda & API Gateway](Lambda_API/)
4. [Testing](Testing/)
5. [Cleanup](Cleanup/)
