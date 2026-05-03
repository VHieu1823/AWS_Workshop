---
title: "Project Proposal"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

### Serverless API Deployment with API Gateway, Lambda, Cognito, and DynamoDB

### 📄 1. Executive Summary

This project focuses on building an online music streaming web system based on a serverless architecture, in which the core components include Amazon API Gateway, AWS Lambda, and Amazon Cognito. The system allows users to access and stream music online, manage playlists, and supports basic content management features.

In the proposed architecture, API Gateway acts as the entry point and routing layer for requests from the client to the corresponding Lambda functions. AWS Lambda is responsible for handling backend business logic and interacting with data storage services such as S3 and DynamoDB, while Amazon Cognito ensures user authentication and authorization through a token-based mechanism. This approach eliminates the need for traditional server infrastructure management while providing automatic scalability and resource optimization based on demand.

The adoption of a serverless model not only helps the system achieve high performance and scalability but also optimizes operational costs through a pay-as-you-go model. In addition, the architecture is designed with a clear separation between frontend and backend, improving maintainability, extensibility, and future integration capabilities.

---

### 📌 2. Problem Statement

#### Current Issues

In the context of increasing demand for sharing and accessing personal music content, existing platforms still do not fully meet user needs in terms of flexibility and personalization. In particular, independent artists face difficulties in uploading and managing content due to complex processes and limited control.

Furthermore, many current systems have complex architectures, high operational costs, and are difficult to scale as the number of users increases. Issues related to user authentication, API security, and access management are also major challenges in system development.

Therefore, it is necessary to build a simple and flexible web platform that allows users to easily interact with the system while ensuring scalability, security, and cost efficiency.

---

#### Solution

To address these issues, the system is built based on a serverless architecture with four main components:

- **Amazon API Gateway:** acts as a middleware gateway, receiving client requests and routing them to Lambda functions
- **AWS Lambda:** handles all system business logic
- **Amazon Cognito:** ensures user authentication and authorization using JWT tokens
- **DynamoDB:** stores system metadata

The system workflow is designed to be simple and efficient: the client sends a request to API Gateway, which is then authenticated via Cognito and forwarded to Lambda for processing. The result is returned to the client through API Gateway.

This solution helps the system:

- Improve automatic scalability
- Reduce operational costs
- Ensure security through centralized authentication
- Simplify system architecture

---

### 📌 3. Solution Architecture

The system architecture is built using a serverless model, focusing on API processing flow:

![ConnectPrivate](/AWS_Workshop/images/aws_architec.png)

- Users send requests from the frontend to API Gateway
- API Gateway uses a Cognito Authorizer to authenticate users
- After successful authentication, the request is forwarded to Lambda
- Lambda processes business logic, retrieves data from DynamoDB, and returns results to the client

Main components:

- **API Gateway:** manages APIs and routes requests
- **Lambda:** handles backend logic for each function
- **Cognito:** manages users, authentication, and authorization
- **DynamoDB:** stores system data

This architecture ensures scalability, security, and performance without the need for server management.

---

### 📌 4. Technical Implementation

#### Implementation Phases

The project is implemented through the following phases:

**Research and architecture design:**  
Study AWS services (API Gateway, Lambda, Cognito, DynamoDB) and design a suitable serverless architecture.

**Cost and feasibility assessment:**  
Estimate AWS Free Tier usage costs and evaluate system operability.

**Architecture optimization:**  
Design efficient Lambda functions, reduce unnecessary requests, and optimize processing flow.

**Development and testing:**  
Deploy API Gateway, Lambda functions, integrate Cognito, and perform system testing and refinement.

---

#### Technical Requirements

**Frontend:**

- Send requests to API Gateway via HTTP/REST API
- Handle Cognito tokens for user authentication

**Backend (Serverless):**

- Lambda processes business logic
- API Gateway routes requests

---

### 📌 5. AWS Cost Estimation

The system utilizes AWS Free Tier:

- **AWS Lambda:** 1 million requests/month → ~0 USD
- **API Gateway:** 1 million requests/month → ~0 USD
- **Amazon DynamoDB:** 25GB storage → ~0 USD

👉 Total cost is approximately **0 USD/month** in the initial stage

---

### 📌 6. Risk Assessment

- **Performance:** latency due to Lambda cold start
- **Cost:** increases when exceeding Free Tier limits
- **Security:** misconfiguration of Cognito or IAM
- **API design:** poor optimization leading to scalability issues

**Mitigation:**

- Optimize Lambda performance
- Use caching mechanisms
- Apply security best practices
- Monitor using CloudWatch

---

### 📌 7. Expected Outcomes

- Build a fully functional serverless API system
- Optimize operational costs
- Ensure easy scalability in the future

- Provide a foundation for larger systems such as:
  - Microservices
  - AI recommendation systems
  - Real-time processing systems
