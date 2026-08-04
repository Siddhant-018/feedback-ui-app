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

---

## 🧠 Concepts Covered

- Cross-Origin Resource Sharing (CORS)
- Serverless architecture
- REST APIs via API Gateway
- Secure S3 file handling
- Email automation via SES
- CI/CD with GitHub Actions

---

