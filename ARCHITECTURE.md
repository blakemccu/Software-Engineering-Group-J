# MösFit System Architecture

## 📌 Overview
MösFit is a fitness tracking application that helps users log workouts, track calorie intake, and monitor their progress. The system is designed with a **frontend application**, a **backend API**, and a **database**.

## 🔧 Tech Stack
- **Frontend**: React Native (Mobile) & Next.js (Web)
- **Backend**: Node.js with Express
- **Database**: PostgreSQL (Hosted on AWS RDS)
- **Cloud Storage**: Firebase Storage (For user profile images & exercise videos)
- **Authentication**: JWT-based authentication
- **Wearable Integration**: Apple Health, Google Fit, Fitbit APIs

## 🏗️ System Architecture Diagram
![System Architecture](./assets/system_architecture.png)

## 🔄 Data Flow
1. **User interacts with the app** (logs workouts, enters meals, views progress).
2. **Frontend sends API requests** to the backend.
3. **Backend processes data** and interacts with the database.
4. **Results are sent back** to the frontend and displayed to the user.
5. **Wearable integrations sync** fitness data automatically.

---
