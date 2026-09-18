# FitFlow High-Level Architecture

## 1. Architecture Overview

FitFlow uses a layered architecture with a Flutter client, NestJS backend, FastAPI AI service, PostgreSQL database, Redis caching and real-time layer, and AWS Cognito authentication.

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

- AWS Cognito is used for user authentication and authorization.
- Secure communication should be used between the frontend and backend services.
- JWT-based authentication can be used for protected API requests.
- Backend APIs should validate user input.
- Sensitive user and fitness data should be protected.
- Access to user information should be controlled based on user roles and permissions.

---

## 5. Scalability Considerations

- The NestJS backend can be scaled horizontally when user traffic increases.
- Redis can reduce repeated database queries through caching.
- The FastAPI AI service can be scaled independently based on AI processing requirements.
- PostgreSQL provides centralized storage for application data.
- An API Gateway can help manage requests between clients and backend services.

---

## 6. Integration Considerations

The system uses REST APIs for communication between the Flutter frontend and NestJS backend.

The NestJS backend communicates with the FastAPI AI service when AI-based personalization is required.

WebSockets are used through the NestJS Real-Time Gateway for real-time communication.

Redis supports caching and real-time/pub-sub requirements.

PostgreSQL is used as the main persistent database.

AWS Cognito manages authentication and authorization.

---

## 7. Architecture Decision Record (ADR)

### Decision

The selected FitFlow architecture uses:

- Flutter for frontend development
- NestJS for the main backend
- FastAPI for AI/ML functionality
- PostgreSQL for the primary database
- Redis for caching and real-time/pub-sub requirements
- AWS Cognito for authentication and authorization

### Reasons

This architecture separates the main application backend from AI/ML processing.

Flutter supports development for multiple platforms from a single codebase.

NestJS provides a structured backend architecture for the main application services.

FastAPI provides a separate service for AI and personalization features.

PostgreSQL provides the primary data storage.

Redis supports caching and real-time requirements.

AWS Cognito provides authentication and authorization.

### Alternatives Considered

Other technologies considered during the comparison included:

- React Native
- Kotlin Multiplatform
- Swift/SwiftUI
- FastAPI as the main backend
- Go
- MongoDB
- Firebase
- DynamoDB
- Firebase Authentication
- Auth0
- Supabase

### Consequences

This architecture introduces multiple services that need to be maintained and integrated.

However, separating the AI service from the main backend allows AI functionality to be developed and scaled independently.

The architecture also provides a clear separation between frontend, backend, AI processing, authentication, and data storage.
