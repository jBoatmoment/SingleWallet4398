# SingleWallet Project Structure

This document outlines the organization of the SingleWallet project for easy collaboration among the team.

## 📁 Project Overview

```
SingleWallet/
├── src/main/java/com/GroupSix/SingleWallet/
│   ├── controller/          # REST API endpoints (Team Member 1)
│   ├── service/            # Business logic layer (Team Member 2)
│   ├── repository/         # Database access layer (Team Member 2)
│   ├── model/              # JPA entities/database models (Team Member 2)
│   ├── dto/                # Data Transfer Objects for API (Team Member 1)
│   ├── config/             # Spring configuration classes
│   ├── exception/          # Custom exceptions and error handling
│   └── SingleWalletApplication.java
│
├── src/main/resources/
│   ├── db/
│   │   ├── migration/      # Database migration scripts (Flyway/Liquibase)
│   │   └── data/           # Seed data and test data SQL files
│   ├── static/             # Simple frontend assets (HTML/CSS/JS)
│   │   ├── css/
│   │   ├── js/
│   │   └── images/
│   └── application.properties
│
├── frontend/               # Modern frontend (React/Vue/Angular) (Team Member 3 & 4)
│   ├── src/
│   │   ├── components/     # Reusable UI components
│   │   ├── pages/          # Page-level components
│   │   ├── services/       # API interaction services
│   │   └── utils/          # Utility functions
│   └── public/             # Public assets
│
└── pom.xml                 # Maven dependencies
```

## 🎯 Team Responsibilities Suggestion

### Team Member 1: API Layer
- **controller/** - Create REST endpoints
- **dto/** - Define request/response objects
- **exception/** - Handle API errors

### Team Member 2: Business & Data Layer
- **service/** - Implement business logic
- **repository/** - Database operations
- **model/** - Define entities
- **db/migration/** - Create database schemas

### Team Member 3 & 4: Frontend
- **frontend/src/components/** - Build UI components
- **frontend/src/pages/** - Create application pages
- **frontend/src/services/** - Connect to backend APIs
- **frontend/src/utils/** - Shared utilities

## 🔄 Typical Development Flow

1. **Define Data Model** (Member 2)
   - Create entity in `model/`
   - Create repository in `repository/`
   - Create migration in `db/migration/`

2. **Implement Business Logic** (Member 2)
   - Create service interface and implementation in `service/`

3. **Create API Endpoints** (Member 1)
   - Create DTO in `dto/`
   - Create controller in `controller/`

4. **Build Frontend** (Members 3 & 4)
   - Create service to call API in `frontend/src/services/`
   - Create components in `frontend/src/components/`
   - Create pages in `frontend/src/pages/`

## 📝 Best Practices

- **Use branches**: Each member works on feature branches
- **Keep layers separated**: Don't mix controller logic with service logic
- **Document APIs**: Add comments to controllers and DTOs
- **Write tests**: Add unit tests in `src/test/java/`
- **Commit often**: Small, focused commits are easier to review

## 🛠️ Next Steps

1. Add dependencies to `pom.xml`:
   - Spring Web (for REST APIs)
   - Spring Data JPA (for database)
   - Database driver (H2, PostgreSQL, MySQL)
   - Flyway or Liquibase (for migrations)
   
2. Configure `application.properties`:
   - Database connection
   - Server port
   - Application settings

3. Initialize frontend:
   - Run `npx create-react-app .` in frontend/ folder
   - Or `npm init vue@latest` for Vue
   - Or `ng new .` for Angular
