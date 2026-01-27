# Welcome to StayMate Documentation

**StayMate** is a production-grade platform connecting tenants with landlords and compatible roommates. It leverages modern web technologies (Next.js, Spring Boot) and AI (Ollama) to create safe, verified, and compatible living arrangements.

## 🚀 Key Features

- **Property Management**: Landlords can list, manage, and track performance of properties.
- **Roommate Matching**: AI-powered matching based on lifestyle, habits, and budget (`95%` compatibility target).
- **Secure Booking**: Verified payments and booking requests.
- **Role-Based Dashboards**: tailored experiences for Guests, Tenants, Landlords, and Admins.

## 📚 Documentation Map

### 🚀 Getting Started
- **Project overview and goals**: Understand the core mission and features of StayMate.
- **Installation and setup**: Step-by-step specific instructions to clone and install dependencies.
- **Environment configuration**: Setting up `.env` files and required secrets.
- **First-time run instructions**: How to launch the backend and frontend locally.

### 🧭 User Guides
- **User registration & authentication**: Sign up, login, and profile verification flows.
- **Property browsing and booking**: Searching for rentals and sending booking requests.
- **Roommate finder and requests**: Browsing profiles and initiating connection requests.
- **Notifications and dashboards**: Managing alerts and viewing user-specific stats.

### 🏠 Owner Guides
- **Property listing management**: Creating, editing, and archiving property posts.
- **Vacancy & booking status logic**: Understanding how availability is calculated.
- **Inquiry & application handling**: Managing incoming tenant queries and applications.
- **Review management**: Responding to tenant reviews and ratings.

### 🧑🤝🧑 Roommate System
- **Roommate ad creation**: Specific steps to post a roommate finder profile.
- **Sending roommate requests**: How to connect with potential matches.
- **Responding to requests**: Accepting or rejecting incoming connection requests.
- **Status lifecycle**: Explanation of Pending, Approved, and Rejected states.

### 🛠️ Admin Guide
- **Admin dashboard overview**: High-level view of system health and metrics.
- **User and property moderation**: Tools for banning users or removing illegal listings.
- **Audit logs and overrides**: Tracking system changes and manual interventions.
- **Analytics and reports**: Generating platform usage reports.

### 🔌 API Reference
- **Authentication endpoints**: Login, register, and token management APIs.
- **Property, inquiry, application APIs**: Endpoints for managing real estate data.
- **Roommate request APIs**: Backend services for the roommate matching system.
- **Notification APIs**: Endpoints for fetching and marking notifications.

### 🗄️ Database & Models
- **Entity relationship overview**: Visual diagram of the database schema.
- **Key tables and fields**: Detailed breakdown of user, property, and request tables.
- **Status enums and constraints**: Allowed values for critical state columns.

### 🎨 Frontend Architecture
- **Component structure**: Organization of atomic components and pages.
- **State management**: How React Context and hooks handle app state.
- **Routing and protected pages**: Next.js App Router configuration and security.
- **UI/UX conventions**: Styling guidelines and component libraries.

### 🔔 Notifications System
- **Notification types**: List of all system alerts (Booking, Roommate, System).
- **Trigger conditions**: Events that cause a notification to differ.
- **In-app vs email notifications**: Delivery channels and logic.

### 🧪 Testing & QA
- **Manual test cases**: Scripted scenarios for manual verification.
- **Role-based test scenarios**: Specific flows for Tenants, Landlords, and Admins.
- **Edge case handling**: Testing user limits and error states.

### 🚀 Deployment & DevOps
- **Environment variables**: Production configuration reference.
- **Docker & CI/CD**: Containerization and automated deployment pipelines.
- **Production deployment steps**: Guide for deploying to AWS/Vercel.

## 🛠 Tech Stack

| Component | Technology | Description |
|-----------|------------|-------------|
| **Frontend** | Next.js 14 | React-based UI with Tailwind CSS. |
| **Backend** | Spring Boot 3.2 | Java-based REST API. |
| **Database** | MySQL 8.0 | Relational data persistence. |
| **Storage** | MinIO (S3) | Object storage for images & documents. |
| **AI** | Ollama (Llama 3) | Local LLM for matching logic. |
| **Testing** | JMeter | Performance and load testing. |

## 🤝 Contribution

We welcome contributions! Please check our [Contribution Guide](contribution/coding-standards.md) to get started.
