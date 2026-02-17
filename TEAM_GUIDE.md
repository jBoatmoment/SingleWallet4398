# Team Collaboration Guide

## 🎯 Suggested Team Split

### Backend Team (Members 1 & 2)

**Member 1: API Layer Lead**
- `controller/` - REST endpoints
- `dto/` - Request/response objects
- `exception/` - Error handling
- API documentation (Swagger)

**Member 2: Data & Business Logic Lead**
- `model/` - Database entities
- `repository/` - Data access
- `service/` - Business logic
- `db/migration/` - Database schemas

### Frontend Team (Members 3 & 4)

**Member 3: UI Components Lead**
- `frontend/src/components/` - Reusable components
- Styling and theming
- Component library setup
- Responsive design

**Member 4: Pages & Integration Lead**
- `frontend/src/pages/` - Application pages
- `frontend/src/services/` - API integration
- Routing setup
- State management

## 🔄 Git Workflow

### Branch Strategy
```
main (production-ready code)
├── develop (integration branch)
    ├── feature/wallet-api (Member 1)
    ├── feature/wallet-service (Member 2)
    ├── feature/wallet-ui (Member 3)
    └── feature/wallet-page (Member 4)
```

### Workflow Steps
1. **Create feature branch**: `git checkout -b feature/your-feature`
2. **Work on your feature**: Make commits regularly
3. **Push to remote**: `git push origin feature/your-feature`
4. **Create Pull Request**: To `develop` branch
5. **Code Review**: Team reviews the PR
6. **Merge**: After approval, merge to `develop`
7. **Testing**: Test on `develop` branch
8. **Release**: Merge `develop` to `main` when ready

### Commit Message Format
```
<type>: <subject>

<body>

Examples:
feat: add wallet creation endpoint
fix: resolve transaction calculation bug
docs: update API documentation
style: format code with prettier
refactor: simplify wallet service logic
test: add unit tests for wallet controller
```

## 📋 Development Checklist

### Before Starting a Feature
- [ ] Pull latest changes from `develop`
- [ ] Create a new feature branch
- [ ] Understand the requirements
- [ ] Check relevant README files

### During Development
- [ ] Write clean, documented code
- [ ] Follow naming conventions
- [ ] Add unit tests
- [ ] Commit frequently with clear messages
- [ ] Pull from `develop` regularly to stay updated

### Before Creating PR
- [ ] Test your code thoroughly
- [ ] Run all tests: `mvn test` (backend), `npm test` (frontend)
- [ ] Update documentation if needed
- [ ] Ensure no merge conflicts
- [ ] Write clear PR description

## 🗓️ Sprint Planning Template

### Week 1: Setup & Foundation
- **All**: Project setup, structure understanding
- **Member 1**: Setup Spring Web, create first controller
- **Member 2**: Setup database, create entities
- **Member 3**: Initialize frontend, create basic components
- **Member 4**: Setup routing, create page structure

### Week 2: Core Features
- **Member 1**: User authentication API
- **Member 2**: User and Wallet business logic
- **Member 3**: Login/Register components
- **Member 4**: Authentication flow, protected routes

### Week 3: Main Features
- **Member 1**: Wallet and transaction APIs
- **Member 2**: Transaction logic, validation
- **Member 3**: Wallet card, transaction list components
- **Member 4**: Dashboard page, wallet details page

### Week 4: Polish & Testing
- **All**: Integration testing, bug fixes, documentation

## 💬 Communication

### Daily Standup Questions
1. What did I complete yesterday?
2. What will I work on today?
3. Are there any blockers?

### Code Review Guidelines
- Be respectful and constructive
- Ask questions rather than demand changes
- Suggest improvements with examples
- Approve quickly if changes are good
- Test the changes if possible

## 🔧 Useful Commands

### Backend (Spring Boot)
```bash
mvn clean install          # Build project
mvn spring-boot:run        # Run application
mvn test                   # Run tests
mvn clean package          # Create JAR file
```

### Frontend
```bash
npm install                # Install dependencies
npm start                  # Start dev server
npm test                   # Run tests
npm run build              # Build for production
```

### Git
```bash
git status                 # Check status
git pull origin develop    # Pull latest changes
git checkout -b feature/x  # Create new branch
git add .                  # Stage changes
git commit -m "message"    # Commit changes
git push origin feature/x  # Push to remote
git log --oneline          # View commit history
```

## 📖 Learning Resources

### Spring Boot
- [Spring Boot Official Docs](https://spring.io/projects/spring-boot)
- [Baeldung Spring Tutorials](https://www.baeldung.com/spring-boot)

### Frontend
- [React Docs](https://react.dev/)
- [Vue.js Guide](https://vuejs.org/guide/)
- [MDN Web Docs](https://developer.mozilla.org/)

### Database
- [JPA/Hibernate Guide](https://www.baeldung.com/jpa-hibernate)
- [Flyway Documentation](https://flywaydb.org/documentation/)

## 🐛 Troubleshooting

### Backend won't start
- Check `application.properties` configuration
- Ensure database is running
- Check for port conflicts (8080)
- Run `mvn clean install`

### Frontend won't start
- Delete `node_modules` and `package-lock.json`
- Run `npm install` again
- Check for port conflicts (3000)
- Clear browser cache

### Merge Conflicts
1. Pull latest changes: `git pull origin develop`
2. Resolve conflicts in files
3. Mark as resolved: `git add .`
4. Complete merge: `git commit`

## 📞 Need Help?
- Check README files in each folder
- Ask in team chat
- Create a GitHub issue
- Schedule a team discussion
