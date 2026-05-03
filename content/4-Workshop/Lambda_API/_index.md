---
title: "Lambda & API Gateway"
weight: 3
chapter: false
pre: " <b> 4.3 </b> "
---

In this section, we create the Lambda functions and wire them up to API Gateway.

## What we will build

| Route         | Lambda             | Auth required |
| ------------- | ------------------ | ------------- |
| `POST /login` | `loginFunction`    | No            |
| `GET /songs`  | `getSongsFunction` | Yes (JWT)     |

## Steps

1. [Create Lambda Functions](Lambda/)
2. [Set up API Gateway](API-Gateway/)
3. [Connect Lambda to API Gateway](API_Lambda/)
