# FitFlow High-Level Architecture

## 1. Architecture Overview

FitFlow uses a layered architecture with a Flutter client, NestJS backend, FastAPI AI service, PostgreSQL database, Redis caching/real-time layer, and AWS Cognito authentication.

## 2. Main Components

### Frontend
Flutter provides the FitFlow application for iOS, Android, and Web.

### API Gateway
The API Gateway provides a single entry point between the client applications and backend services.

### Backend
NestJS provides the main backend services:

- User and Profile Service
- Workout Service
- Social Service
- Nutrition Service
- Real-Time Gateway using WebSockets

### AI Service
FastAPI provides a separate AI/ML service for personalized workout recommendations and personalization processing.

### Data Layer

**PostgreSQL** is used as the primary database for application data.

**Redis** is used for caching and real-time/pub-sub requirements.

### Authentication

AWS Cognito is used for authentication and authorization.

---

## 3. Data Flow

### Personalized Workout Plans

Flutter App
→ API Gateway
→ NestJS Workout Service
→ FastAPI AI Service
→ PostgreSQL

The AI service processes relevant fitness information and provides personalized workout recommendations.

### Social Sharing

Flutter App
→ API Gateway
→ NestJS Social Service
→ PostgreSQL

Redis can support real-time communication where required.

### Nutrition Tracking

Flutter App
→ API Gateway
→ NestJS Nutrition Service
→ FastAPI AI Service
→ PostgreSQL

Nutrition-related information can be processed by the AI service when personalization is required.

---

## 4. Security Considerations

- AWS Cognito handles user authentication.
- Backend services validate authenticated requests.
- HTTPS should be used for communication between client and backend.
- Sensitive user information should be protected.
- Role-based authorization should be applied to protected backend operations.

---

## 5. Scalability Considerations

- Backend services are separated into logical modules.
- FastAPI AI processing is separated from the main backend.
- Redis can reduce repeated database requests through caching.
- PostgreSQL provides structured and reliable data storage.
- Services can be scaled independently when required.

---

## 6. Integration Considerations

The Flutter application communicates with the NestJS backend through REST APIs.

NestJS communicates with the FastAPI AI service for AI/ML processing.

NestJS services use PostgreSQL for persistent data storage and Redis for caching and real-time requirements.

AWS Cognito provides the authentication layer across the application.

---

## 7. Architecture Decision Record

### Decision

FitFlow will use Flutter, NestJS, FastAPI, PostgreSQL, Redis, and AWS Cognito as the main technology stack.

### Reasons

- Flutter supports iOS, Android, and Web development.
- NestJS provides a structured backend architecture.
- FastAPI is suitable for AI/ML processing.
- PostgreSQL provides structured data storage.
- Redis supports caching and real-time requirements.
- AWS Cognito provides authentication and authorization.
- Separating AI processing from the main backend improves integration and maintainability.

### Alternatives Considered

Alternative technologies were compared during the technology evaluation activities, including React Native, Kotlin Multiplatform, Swift/SwiftUI, FastAPI as a main backend, Go, MongoDB, Firebase, DynamoDB, Firebase Authentication, Auth0, and Supabase.

### Consequences

This architecture introduces multiple services that require integration and deployment management. However, it provides clear separation between the client, main backend, AI processing, authentication, and data layers.
