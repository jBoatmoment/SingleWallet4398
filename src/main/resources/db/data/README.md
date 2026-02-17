# Database Seed Data

This folder contains SQL files for populating initial or test data.

## Purpose
Seed data files are used to:
- Populate reference/lookup tables
- Create test data for development
- Setup initial admin users
- Load sample data for demos

## File Organization
```
data/
├── 01_reference_data.sql       # Static reference data
├── 02_test_users.sql           # Test user accounts
├── 03_sample_wallets.sql       # Sample wallet data
└── dev/                        # Development-only data
    └── dev_test_data.sql
```

## Example Seed Data
```sql
-- 01_reference_data.sql
INSERT INTO currency_types (code, name, symbol) VALUES
('USD', 'US Dollar', '$'),
('EUR', 'Euro', '€'),
('GBP', 'British Pound', '£');

-- 02_test_users.sql
INSERT INTO users (username, email, password_hash) VALUES
('testuser1', 'test1@example.com', '$2a$10$...'),
('testuser2', 'test2@example.com', '$2a$10$...');

-- 03_sample_wallets.sql
INSERT INTO wallets (account_number, balance, user_id) VALUES
('ACC001', 1000.00, 1),
('ACC002', 2500.50, 1),
('ACC003', 500.00, 2);
```

## Usage

### Option 1: Via Flyway (Recommended)
Create a migration like `V99__seed_data.sql` that references these files or includes the INSERT statements.

### Option 2: Via application.properties
```properties
# Load data only in dev/test environments
spring.sql.init.mode=always
spring.sql.init.data-locations=classpath:db/data/01_reference_data.sql,classpath:db/data/02_test_users.sql
```

### Option 3: Profile-specific
```properties
# application-dev.properties
spring.sql.init.data-locations=classpath:db/data/dev/dev_test_data.sql
```

## Best Practices
- Separate production data from test data
- Use environment-specific profiles
- Don't commit sensitive data (passwords, keys)
- Use consistent IDs for test data
- Document the purpose of each seed file
