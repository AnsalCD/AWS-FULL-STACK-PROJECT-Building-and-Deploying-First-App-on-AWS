# AWS FULL STACK PROJECT | Building and Deploying First App on AWS

![AWS Full Stack Banner](https://raw.githubusercontent.com/aws-samples/aws-icons-for-architecture-diagrams/main/Architecture-Icons/AWS-Cloud.png)

🎉 **Event RSVP – AWS Full-Stack Tutorial**  
A simple yet production-style **AWS-powered full-stack application** that lists events, shows event details & statistics, and allows users to submit RSVPs in real time.

> This project is designed for beginners and intermediate developers who want hands-on exposure to **AWS services working together end-to-end**.


---

## 🧱 Architecture Overview

![AWS Architecture Diagram](https://raw.githubusercontent.com/aws-samples/aws-icons-for-architecture-diagrams/main/Architecture-Icons/Arch-Category_Compute/Arch_AWS-Lambda_64.png)

```
Frontend (HTML/CSS/JS)
        ↓
Amazon API Gateway
        ↓
AWS Lambda (Node.js)
        ↓
MySQL (RDS) + DynamoDB
        ↓
Amazon S3 + CloudFront
```

### 🔧 Services Used
- **Amazon S3** – Static website hosting
- **Amazon CloudFront** – CDN for fast global delivery
- **Amazon API Gateway** – REST APIs
- **AWS Lambda** – Serverless backend
- **Amazon RDS (MySQL)** – Event metadata storage
- **Amazon DynamoDB** – RSVP & statistics storage

---

## 📁 Project Structure

```text
.
├── index.html           # Main UI
├── style.css            # Styling
├── app.js               # Entry script (loads events)
├── events.js            # Event logic + modal + RSVP
├── utils.js             # API helpers & formatters
├── index.js             # Lambda backend handler
├── database-notes.txt   # SQL Commands
├── package.json
├── package-lock.json
├── .gitignore
```

### `.gitignore`
```text
node_modules/
.DS_Store
```

---

## 🚀 Backend Setup (AWS Lambda)

![Lambda Icon](https://raw.githubusercontent.com/aws-samples/aws-icons-for-architecture-diagrams/main/Architecture-Icons/Arch-Category_Compute/Arch_AWS-Lambda_64.png)

### 1️⃣ Environment Variables
Set the following variables in your **Lambda configuration**:

| Variable | Example | Description |
|--------|--------|-------------|
| REGION | ap-southeast-1 | AWS region |
| DB_HOST | mydb.xxxxx.ap-southeast-1.rds.amazonaws.com | MySQL host |
| DB_USER | admin | MySQL username |
| DB_PASS | ******** | MySQL password |
| DB_NAME | eventsdb | Database name |

---

### 2️⃣ Install Dependencies

```bash
npm install
```

---

## 🔌 API Summary

![API Gateway Icon](https://raw.githubusercontent.com/aws-samples/aws-icons-for-architecture-diagrams/main/Architecture-Icons/Arch-Category_Networking-Content-Delivery/Arch_Amazon-API-Gateway_64.png)

| Method | Path | Purpose |
|------|------|--------|
| GET | `/events` | Fetch all events |
| GET | `/event/{event_id}` | Fetch single event |
| GET | `/stats/{event_id}` | Get RSVP counts |
| GET | `/attendees/{event_id}` | Get attendee list |
| POST | `/rsvp` | Submit RSVP |

⚠️ **Important:** Ensure **CORS is enabled** in API Gateway for all methods.

---

## 🗄️ Database Layer

![Database Icon](https://raw.githubusercontent.com/aws-samples/aws-icons-for-architecture-diagrams/main/Architecture-Icons/Arch-Category_Database/Arch_Amazon-DynamoDB_64.png)

- **MySQL (RDS)**
  - Stores event metadata
  - Event ID, title, description, date, location

- **DynamoDB**
  - Stores RSVP counts
  - Tracks attendees efficiently

Refer to `database-notes.txt` for SQL table creation commands.

---

## 🌐 Hosting (S3 + CloudFront)

![S3 CloudFront](https://raw.githubusercontent.com/aws-samples/aws-icons-for-architecture-diagrams/main/Architecture-Icons/Arch-Category_Storage/Arch_Amazon-S3_64.png)

### Steps
1. Upload frontend files to **S3**:
   - `index.html`
   - `style.css`
   - `app.js`, `events.js`, `utils.js`

2. Create a **CloudFront distribution** pointing to the S3 bucket
3. Set **Default Root Object** to:
   ```
   index.html
   ```

---

## 🔁 Making Frontend Changes (Cache Busting)

CloudFront caches files aggressively. After updating frontend files:

### CloudFront Invalidation (Console)
1. Go to **CloudFront → Distribution → Invalidations**
2. Create a new invalidation:
   ```
   /*
   ```
3. Wait for status: **Completed**

### Hard Refresh Browser
- **Windows:** `Ctrl + F5`
- **Mac:** `Cmd + Shift + R`

---

## ✅ What You Will Learn

- How to design a **real-world AWS full-stack architecture**
- Building **serverless REST APIs**
- Integrating **MySQL + DynamoDB** together
- Hosting frontend apps using **S3 + CloudFront**
- Handling **CORS, caching, and deployments**

---

## 📌 Final Notes

This project is intentionally simple but mirrors **production AWS patterns**. You can extend it by adding:
- Authentication (Amazon Cognito)
- CI/CD (GitHub Actions + AWS)
- Monitoring (CloudWatch dashboards)

---

⭐ If this project helped you, consider starring the repository and sharing it with others learning AWS Full Stack development.

Happy Building on AWS 🚀
