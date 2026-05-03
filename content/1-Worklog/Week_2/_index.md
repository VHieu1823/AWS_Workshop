---
title: "Worklog Week 2"
weight: 2
chapter: false
pre: " <b> 1.2 </b> "
---

### 📌 Objectives

- Understand core AWS services: S3, DynamoDB, API Gateway, Lambda, Cognito
- Design system architecture using a serverless model
- Design a NoSQL database suitable for the problem domain
- Analyze and model functional and non-functional requirements
- Select appropriate AWS services and configure resources, optimizing cost (Free Tier)

---

### 🛠 Tasks Performed

| Task                                                                           | Start Date | End Date   | References                             |
| ------------------------------------------------------------------------------ | ---------- | ---------- | -------------------------------------- |
| Study Amazon S3 (audio file storage, object storage mechanism, access control) | 16/03/2026 | 17/03/2026 | https://docs.aws.amazon.com/s3         |
| Study DynamoDB (NoSQL, partition key, sort key, table design)                  | 17/03/2026 | 18/03/2026 | https://docs.aws.amazon.com/dynamodb   |
| Study AWS Lambda and serverless architecture                                   | 18/03/2026 | 19/03/2026 | https://docs.aws.amazon.com/lambda     |
| Study API Gateway (REST API, request routing)                                  | 19/03/2026 | 19/03/2026 | https://docs.aws.amazon.com/apigateway |
| Study AWS Cognito (Authentication & Authorization)                             | 19/03/2026 | 20/03/2026 | https://docs.aws.amazon.com/cognito    |
| Analyze system requirements (User, Song, Playlist, Streaming)                  | 20/03/2026 | 20/03/2026 |                                        |
| Design Database Schema (User, Song, Playlist)                                  | 20/03/2026 | 20/03/2026 |                                        |
| Design system architecture (S3 + Lambda + API Gateway + DynamoDB + Cognito)    | 20/03/2026 | 20/03/2026 |                                        |
| Identify AWS resources suitable for Free Tier                                  | 20/03/2026 | 20/03/2026 |                                        |

---

### ✅ Achievements

- Gained understanding of core AWS services and their roles:
  - S3: stores audio files as objects and provides URL-based access
  - DynamoDB: high-performance NoSQL data storage
  - Lambda: serverless backend logic execution
  - API Gateway: handles client requests and routes them to Lambda
  - Cognito: user management, authentication, and authorization

- Understood serverless architecture model and its advantages:
  - No server management required
  - Automatic scaling
  - Cost optimization based on usage

- Designed overall system architecture:
  - Frontend → API Gateway → Lambda → DynamoDB
  - Audio files stored and retrieved from S3
  - Authentication handled by Cognito

- Built NoSQL database schema:
  - User table (userId, email, metadata)
  - Song table (songId, title, artist, fileUrl)
  - Playlist table (playlistId, userId, listSongIds)

- Learned query-first design approach in NoSQL systems

- Identified system requirements:
  - Functional: register, login, music streaming, playlist creation
  - Non-functional: performance, security, scalability

- Selected AWS Free Tier–suitable services:
  - S3 (free storage limit)
  - DynamoDB (free read/write capacity)
  - Lambda (free request quota)
  - API Gateway (free tier limits)

- Developed cloud system design mindset:
  - Separation of frontend and backend
  - Use of managed services
  - Early-stage cost optimization

---
