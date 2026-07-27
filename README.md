# 📦 Serverless Feedback Form on AWS

Build a **real-world, serverless AWS project** that lets users submit feedback with optional PDF uploads — and delivers admin alerts, secure storage, and auto-deployment. This project is perfect for your portfolio, AWS learning path, or production use case.

---

## ✅ Features

- Feedback form with **Name, Email, Message, and PDF Upload**
- Data stored securely in **DynamoDB**
- PDFs saved in **private S3 bucket**
- Email notification sent via **Amazon SES**
- **API Gateway + Lambda** as the backend
- **Frontend hosted with S3 + CloudFront**
- **CI/CD pipeline** using GitHub Actions

---

## 🧱 Architecture

```
User → CloudFront → S3 (index.html)
           ↓
   JavaScript Form Submit
           ↓
    API Gateway (POST /submit)
           ↓
         AWS Lambda
           ├── Save data to DynamoDB
           ├── Upload PDF to S3
           └── Send email via SES
```

CI/CD:
```
GitHub Push → GitHub Actions → S3 + CloudFront Invalidate
```

---

## 🛠 Technologies Used

- AWS Lambda (Python)
- Amazon API Gateway (REST)
- Amazon S3 (file storage & frontend hosting)
- Amazon CloudFront (CDN)
- Amazon DynamoDB (NoSQL database)
- Amazon SES (email sending)
- GitHub Actions (CI/CD)

---

## 📁 Project Structure

```
.
├── frontend/
│   ├── index.html
│   └── admin.html (optional)
├── lambda/
│   └── submit_feedback.py
├── .github/
│   └── workflows/
│       └── deploy.yml
```

---

## 🚀 How to Deploy

### 1️⃣ Create S3 Buckets
- One for **feedback PDFs**
- One for **frontend hosting**
- Block all public access

### 2️⃣ DynamoDB Table
- Table name: `Feedback-Kobina`
- Partition key: `feedback_id` (String)

### 3️⃣ SES Setup
- Verify your admin email in SES (us-east-1)

### 4️⃣ Lambda Function
- Handles feedback submission
- Uploads PDF to S3
- Sends email with SES

### 5️⃣ API Gateway
- REST API with POST `/submit`
- Lambda Proxy integration
- Enable CORS (POST, OPTIONS)

### 6️⃣ GitHub CI/CD
- Create an IAM user for deployment
- Add these GitHub secrets:
  - `AWS_ACCESS_KEY_ID`
  - `AWS_SECRET_ACCESS_KEY`
  - `AWS_REGION`
  - `S3_BUCKET`
  - `CLOUDFRONT_DIST_ID`

- GitHub Workflow (`.github/workflows/deploy.yml`):

```yaml
name: Deploy Frontend to S3 + CloudFront

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ secrets.AWS_REGION }}
      - run: aws s3 sync ./frontend s3://${{ secrets.S3_BUCKET }} --delete
      - if: env.CLOUDFRONT_DIST_ID != ''
        env:
          CLOUDFRONT_DIST_ID: ${{ secrets.CLOUDFRONT_DIST_ID }}
        run: |
          aws cloudfront create-invalidation \
            --distribution-id $CLOUDFRONT_DIST_ID \
            --paths "/*"
```

---

## 🧠 Concepts Covered

- Cross-Origin Resource Sharing (CORS)
- Serverless architecture
- REST APIs via API Gateway
- Secure S3 file handling
- Email automation via SES
- CI/CD with GitHub Actions

---

